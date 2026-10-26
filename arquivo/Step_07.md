# 🚀 Step 07: PokéAgenda — Conectando a PokéAPI no React (`useEffect` & `fetch`)

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica ( / Conceitual):** Entenda o consumo de APIs REST com **`fetch`**, o ciclo de vida de um componente React com o Hook **`useEffect`**, a criação de estados de carregamento (*Loading States*) e a **tradução de dados da API** para o nosso idioma.
> * **🛠️ Trilha Prática (Projeto Integrador):** Substitua o arquivo estático de dados pela **PokéAPI oficial**: o `<PokemonGrid />` passa a buscar e exibir automaticamente os 151 Pokémons reais da 1ª geração assim que o site abre.

---

### 🧩 1. O Problema Prático (Cenário  - Problem Statement)

**O Dilema da Lista Estática Limitada:**  
O Prof. Carvalho entrou em contato com a equipe da **PokéAgenda** com uma notícia importante: o laboratório descobriu que existem mais de 1000 Pokémons catalogados! O estagiário tentou digitar as informações de todos os 1000 Pokémons manualmente dentro do arquivo `pokemons.js`. Ele demorou 3 dias, errou o nome de vários Pokémons, não conseguiu baixar as fotos de todos e o arquivo ficou gigantesco e impossível de carregar.

Cadastrar dados manualmente quando existe uma base de dados oficial na nuvem é ineficiente e ultrapassado.

**A Pergunta-Chave :**  
> *Como podemos utilizar o **`fetch()` do JavaScript** e o Hook **`useEffect` do React** para conectar nosso aplicativo diretamente à **PokéAPI oficial** e carregar todos os Pokémons automaticamente assim que o site abrir?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 O que é uma API REST e a PokéAPI?
* **API (Interface de Programação de Aplicações):** Funciona como o "garçom" da internet. Você faz o pedido (requisição) e o servidor devolve os dados prontos em formato JSON.
* **PokéAPI (`pokeapi.co`):** É um banco de dados gratuito na nuvem que fornece informações completas sobre todos os Pokémons (nomes, fotos, tipos, habilidades e estatísticas).

#### 2.2 O Hook `useEffect` (Efeitos Colaterais no React)
* **Para que serve:** Executar código **fora da renderização** — como buscar dados na internet — assim que o componente nasce na tela (montagem) ou quando alguma variável específica muda.
* **Dissecando a sintaxe:**
  ```text
  useEffect( () => { buscaDados() } , [] );
  ────────┬────────                   ─┬─
          (1)                          (2)
  ```
  1. **A função do efeito:** o código que será executado (aqui, chamamos outra função `buscaDados()` porque o próprio callback não pode ser `async`).
  2. **O array de dependências:** decide QUANDO o efeito roda.
     * `[]` (vazio) ➜ roda **1 única vez**, quando o componente nasce.
     * `[variavel]` ➜ roda de novo sempre que `variavel` mudar.
     * **ausente** ➜ roda em TODA renderização (perigo de loop infinito!).

> [!IMPORTANT]
> **A armadilha do loop infinito:** dentro do `useEffect` nós atualizamos um estado (`setPokemons`). Estado atualizado ➜ nova renderização ➜ `useEffect` sem `[]` roda de novo ➜ atualiza o estado ➜ renderiza... milhares de requisições por segundo e o navegador trava. **O `[]` é o freio.**

#### 2.3 `fetch()` e Funções Assíncronas (`async / await`)
* A internet leva milissegundos (ou segundos!) para trazer a resposta. Usamos `async / await` para "esperar" a resposta **sem travar** o resto do site:
  ```js
  const response = await fetch('https://pokeapi.co/api/v2/pokemon/25');
  const data = await response.json(); // a resposta precisa ser convertida de texto JSON para objeto JS
  ```

#### 2.4 O Estado de Carregamento (*Loading State*)
* Enquanto os dados viajam da API até o navegador, devemos exibir uma mensagem agradável (*"🔴 Carregando Pokédex..."*) em vez de uma tela em branco. É a etiqueta de "aguarde" do garçom.

#### 2.5 Traduzindo a API para o Nosso Projeto
* A PokéAPI devolve os tipos em inglês e em minúsculo (`"fire"`, `"water"`), mas nossos cards (Steps 03/05) usam badges com classes `.type-fogo`, `.type-agua`...
* **A solução:** um pequeno **dicionário de tradução** (objeto chave ➜ valor) durante o mapeamento dos dados:
  ```js
  const tiposPT = { fire: 'Fogo', water: 'Agua', grass: 'Planta', electric: 'Eletrico' };
  const type = tiposPT[pokeDetails.types[0].type.name] ?? 'Normal';
  //                        'fire'                ➜ 'Fogo'
  ```
* *(Mantemos os nomes sem acento — `Agua`, `Eletrico` — de propósito: eles precisam bater exatamente com as classes CSS que você criou no Step 03.)*

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Veja um componente que busca usuários de uma API pública de testes — o MESMO esqueleto que você usará (efeito + estado + loading), fora do domínio Pokémon:

#### `src/ListaUsuarios.jsx`:
```jsx
import { useState, useEffect } from 'react';
import './ListaUsuarios.css';

export function ListaUsuarios() {
  const [usuarios, setUsuarios] = useState([]);
  const [carregando, setCarregando] = useState(true);

  useEffect(() => {
    async function carregarDados() {
      try {
        // 1. Busca os dados na API externa
        const resposta = await fetch('https://jsonplaceholder.typicode.com/users');
        // 2. Converte o texto JSON em objeto JavaScript
        const dados = await resposta.json();
        // 3. Salva no estado
        setUsuarios(dados);
      } catch (erro) {
        console.error('Falha ao carregar usuários:', erro);
      } finally {
        // 4. Em qualquer resultado (sucesso ou erro), desliga o carregamento
        setCarregando(false);
      }
    }

    carregarDados();
  }, []); // roda 1 vez ao abrir a tela

  if (carregando) {
    return <h2 className="aviso">🔄 Carregando dados da internet...</h2>;
  }

  return (
    <ul className="lista-usuarios">
      {usuarios.map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

#### `src/ListaUsuarios.css`:
```css
.lista-usuarios {
  list-style: none;
  padding: 0;
  display: grid;
  gap: 0.5rem;
  max-width: 400px;
  margin: 2rem auto;
}

.lista-usuarios li {
  background: #ffffff;
  border-radius: 8px;
  padding: 0.75rem 1rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}
```

#### Uso no `src/App.jsx` (como qualquer componente):
```jsx
import { Header } from './Header';
import { ListaUsuarios } from './ListaUsuarios';

export function App() {
  return (
    <div className="app-container">
      <Header />
      <ListaUsuarios />
    </div>
  );
}

export default App;
```

> [!TIP]
> **O padrão "3 estados + 1 efeito":** dados (`usuarios`), carregamento (`carregando`) e o `useEffect([], )` que liga um ao outro. Você repetirá exatamente esse desenho no Pokémon — só trocará a URL e o mapeamento.

---

### 🛠️ 4. Desafio Ativo (Mão na Massa)

Sua missão é conectar o `<PokemonGrid />` à PokéAPI. **Apenas 1 arquivo muda** (`src/PokemonGrid.jsx`) e ele será **substituído por inteiro** ao final — nada de remendar pedacinhos:

1. **Remova a dependência dos dados estáticos:**
   * Apague a linha `import { pokemonsIniciais } from './pokemons';`.
   * *(Mantenha o arquivo `pokemons.js` no projeto: ele é nosso "plano B" caso a API caia na prova/falta energia.)*

2. **Reescreva `src/PokemonGrid.jsx` com o arquivo final completo:**
   ```jsx
   import { useState, useEffect } from 'react';
   import { PokemonCard } from './PokemonCard';
   import './PokemonGrid.css';

   // Dicionário de tradução dos tipos (PokéAPI em inglês ➜ nossas classes CSS)
   const tiposPT = {
     normal: 'Normal', fire: 'Fogo', water: 'Agua', electric: 'Eletrico',
     grass: 'Planta', ice: 'Gelo', fighting: 'Lutador', poison: 'Veneno',
     ground: 'Solo', flying: 'Voador', psychic: 'Psiquico', bug: 'Inseto',
     rock: 'Pedra', ghost: 'Fantasma', dragon: 'Dragao'
   };

   export function PokemonGrid() {
     // 1. O estado dos dados (agora a "esteira" não puxa de pokemons.js, e sim da API)
     const [pokemons, setPokemons] = useState([]);
     const [isLoading, setIsLoading] = useState(true);

     // 2. O efeito que roda UMA vez quando o componente nasce
     useEffect(() => {
       async function fetchPokemons() {
         try {
           // 2.1 Busca o índice dos 151 Pokémons da 1ª geração
           const response = await fetch('https://pokeapi.co/api/v2/pokemon?limit=151');
           const data = await response.json();

           // 2.2 Para CADA item do índice, busca os detalhes (foto e tipo)
           const detailedPokemons = await Promise.all(
             data.results.map(async (item) => {
               const pokeRes = await fetch(item.url);
               const pokeDetails = await pokeRes.json();

               return {
                 id: pokeDetails.id,
                 // Capitaliza o nome: 'pikachu' ➜ 'Pikachu'
                 name: pokeDetails.name.charAt(0).toUpperCase() + pokeDetails.name.slice(1),
                 // Tipo principal TRADUZIDO para bater com as classes CSS do Step 03
                 type: tiposPT[pokeDetails.types[0].type.name] ?? 'Normal',
                 types: pokeDetails.types.map(t => tiposPT[t.type.name] ?? t.type.name),
                 image: pokeDetails.sprites.other['official-artwork'].front_default,
                 shinyImage: pokeDetails.sprites.other['official-artwork'].front_shiny
               };
             })
           );

           // 2.3 Salva a lista no estado
           setPokemons(detailedPokemons);
         } catch (error) {
           console.error('Erro ao buscar Pokémons:', error);
         } finally {
           setIsLoading(false);
         }
       }

       fetchPokemons();
     }, []); // o freio do loop infinito

     // 3. Tela de carregamento enquanto a "esteira" enche
     if (isLoading) {
       return (
         <div className="loading-container">
           <h2>🔴 Carregando Pokédex Oficial...</h2>
           <p>Buscando os 151 Pokémons na PokéAPI...</p>
         </div>
       );
     }

     // 4. A grade (idêntica à do Step 05, agora alimentada pela API)
     return (
       <main className="pokemon-grid">
         {pokemons.map((pokemon) => (
           <PokemonCard key={pokemon.id} pokemon={pokemon} />
         ))}
       </main>
     );
   }
   ```

3. **Adicione um estilo fofinho ao aviso de carregamento (`src/PokemonGrid.css`):**
   ```css
   .loading-container {
     text-align: center;
     padding: 4rem 2rem;
     color: #334155;
   }
   ```

4. **Pinte os tipos novos (`src/PokemonCard.css`) — adicione ao final:**
   * Os 4 Pokémons dos Steps 03/05 usavam Planta/Fogo/Água/Elétrico, que já têm cor. A coleção completa de Kanto traz tipos que ainda **não têm classe CSS** — sem elas, as badges aparecem sem cor:
     ```css
     .type-normal    { background-color: #a8a878; color: #ffffff; }
     .type-veneno    { background-color: #9f52c8; color: #ffffff; }
     .type-psiquico  { background-color: #f59785; color: #ffffff; }
     .type-gelo      { background-color: #68c8ee; color: #ffffff; }
     .type-pedra     { background-color: #c8b878; color: #ffffff; }
     .type-fantasma  { background-color: #6a6aa8; color: #ffffff; }
     .type-voador    { background-color: #a8a8f8; color: #333333; }
     .type-inseto    { background-color: #a8b828; color: #ffffff; }
     .type-dragao    { background-color: #7038f8; color: #ffffff; }
     .type-lutador   { background-color: #c82878; color: #ffffff; }
     .type-solo      { background-color: #d8bc78; color: #333333; }
     ```

5. **Nada mais muda:** o `App.jsx` (Step 05) e o `PokemonCard.jsx` (Step 06) continuam iguais. A mágica é que agora o array `pokemons` tem a **mesma shape** dos dados antigos (`id`, `name`, `type`, `image`...) — e ainda traz o `shinyImage` de brinde da API!

> [!TIP]
> **Rede lenta da escola?** São 152 requisições (1 do índice + 151 de detalhes). Se demorar demais, troque temporariamente `limit=151` por `limit=30`. O resto do código não muda nada.

---

### 🧪 5. Teste de Validação

1. Abra o navegador (`http://localhost:5173`) e recarregue com `F5`.
2. A tela deve exibir primeiro **"🔴 Carregando Pokédex Oficial..."** e depois se preencher sozinha com os **151 Pokémons reais** de Kanto (Bulbasaur, Ivysaur, Venusaur, Charmander...).
3. Confirme que as **badges de tipo continuam coloridas** (Fogo vermelho, Água azul, Planta verde...) — a tradução funcionou!
4. Clique em **"⭐ Ver Shiny"** em qualquer Pokémon recém-carregado: o Step 06 continua funcionando com dados reais.
5. Abra o Console (`F12`) e confirme que não há erros vermelhos nem warnings de `key`.

---

### ❓ 6. Quiz de Fixação (6 Questões de Múltipla Escolha)

#### Q1. O que é uma API REST?
- (A) Um programa antivírus do Windows.
- (B) Uma marca de computador.
- (C) Um serviço web que fornece dados estruturados (geralmente JSON) para que diferentes aplicações possam consumi-los.
- (D) Um arquivo de imagem PNG.

> **Gabarito Comentado:** **(C)** APIs funcionam como pontes de dados entre servidores e aplicativos cliente.

#### Q2. Qual é a função do Hook `useEffect` quando passado com um array de dependências vazio `[]`?
- (A) Executar uma animação 3D na tela.
- (B) Executar um bloco de código apenas 1 vez, assim que o componente é montado/carregado na tela.
- (C) Reiniciar o computador do usuário.
- (D) Apagar os dados do banco de dados.

> **Gabarito Comentado:** **(B)** O array de dependências vazio `[]` garante que o efeito colateral (como buscar dados na API) rode uma única vez no nascimento do componente.

#### Q3. O que acontece se você esquecer de colocar o array de dependências `[]` no final do `useEffect` ao fazer um `fetch()`?
- (A) O `fetch()` é cancelado.
- (B) O efeito entra em um loop infinito de requisições, travando o navegador e consumindo banda.
- (C) A imagem fica em preto e branco.
- (D) Nada, o código funciona igual.

> **Gabarito Comentado:** **(B)** Sem o array de dependências, o `useEffect` executa a cada nova renderização — e como a busca atualiza um estado, gera um loop infinito.

#### Q4. Para que serve a instrução `await` antes do comando `fetch()` em uma função assíncrona?
- (A) Para forçar o download do arquivo em formato ZIP.
- (B) Para pausar a execução daquela linha até que o servidor da API responda com os dados solicitados.
- (C) Para acelerar a velocidade da internet.
- (D) Para esconder o endereço do site.

> **Gabarito Comentado:** **(B)** O `await` aguarda a promessa (`Promise`) da requisição de rede ser resolvida antes de avançar para a próxima instrução.

#### Q5. Por que é uma boa prática manter um estado `isLoading` durante requisições de API?
- (A) Para dar feedback visual ao usuário de que os dados estão sendo buscados, evitando a sensação de tela travada.
- (B) Porque o React exige para compilar.
- (C) Para economizar energia da bateria do celular.
- (D) Para mudar a cor do texto para azul.

> **Gabarito Comentado:** **(A)** Exibir um indicador de carregamento melhora drasticamente a experiência do usuário (UX).

#### Q6. No nosso código, para que serve o objeto `tiposPT = { fire: 'Fogo', ... }`?
- (A) Para criptografar os dados da PokéAPI.
- (B) Para traduzir os tipos em inglês vindos da API para os nomes que batem com as classes CSS dos nossos cards.
- (C) Para ordenar os Pokémons por tipo.
- (D) Para esconder os tipos dos Pokémons lendários.

> **Gabarito Comentado:** **(B)** A API devolve `'fire'`; nossas badges esperam `.type-fogo`. O dicionário converte um no outro com acesso por chave (`tiposPT[nomeEmIngles]`).

---

### 📝 7. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Consumo de APIs REST e Hooks Assíncronos em React. Utilização do método fetch(), funções assíncronas (async/await), parsing de dados em JSON, gerenciamento do ciclo de vida de componentes com useEffect e array de dependências, paralelismo com Promise.all, estados de carregamento (Loading States) e normalização de dados externos (tradução de tipos) com dicionários JavaScript."*
