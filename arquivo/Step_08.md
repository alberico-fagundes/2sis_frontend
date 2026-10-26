# 🚀 Step 08: PokéAgenda — O Buscador PokéAPI e Filtros por Tipo (Inputs Controlados)

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica ( / Conceitual):** Domine **Inputs Controlados** no React (`value` + `onChange`), o filtro dinâmico de arrays com **`.filter()`**, a padronização de busca com **`.toLowerCase()`** e a combinação de múltiplos critérios de filtragem.
> * **🛠️ Trilha Prática (Projeto Integrador):** Crie o componente `<PokemonFilters />` (barra de busca + botões por tipo) e ligue os novos estados ao `.filter()` da grade, para que o usuário encontre qualquer Pokémon instantaneamente.

---

### 🧩 1. O Problema Prático (Cenário  - Problem Statement)

**O Dilema da Rolagem Infinita para Achar um Pokémon:**  
Com a PokéAPI conectada e exibindo 151 Pokémons na tela, o Prof. Carvalho tentou usar o aplicativo para consultar o Pikachu durante uma pesquisa de campo. Ele teve que rolar a tela por vários segundos procurando card por card no meio de mais de cem Pokémons. Quando tentou filtrar apenas os Pokémons do tipo "Fogo", descobriu que não havia nenhuma ferramenta de busca ou filtro no site.

Exibir grandes coleções de dados sem ferramentas de busca degrada a usabilidade do produto.

**A Pergunta-Chave :**  
> *Como podemos utilizar **Inputs Controlados com `useState`** e o método **`.filter()` do JavaScript** para criar uma barra de pesquisa e botões de filtro por categoria que atualizam a grade de Pokémons em tempo real enquanto o usuário digita?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 O que são Inputs Controlados no React?
* **O Conceito:** Em HTML puro, o próprio `<input>` guarda o texto digitado. No React, o estado (`useState`) passa a ser o **dono da verdade**: a tela mostra o estado, e digitar atualiza o estado — um ciclo eterno.
* **Dissecando a dupla mágica:**
  ```jsx
  const [searchTerm, setSearchTerm] = useState('');

  <input
    value={searchTerm}                                  // 1. O valor na tela É o estado
    onChange={(e) => setSearchTerm(e.target.value)}     // 2. Digitar ATUALIZA o estado
  />
  ```
  * `e`: o objeto do evento de digitação. `e.target`: o `<input>` que disparou o evento. `e.target.value`: o texto que o usuário acabou de digitar.
* **O efeito dominó:** estado mudou ➜ o React re-executa a função do componente ➜ todo o `.filter()` é recalculado ➜ a grade redesenhada. É o `useState` do Step 06 trabalhando para a busca.

#### 2.2 Filtrando Listas em Tempo Real com `.filter()`
* **A esteira seletiva:** se o `.map()` (Step 05) TRANSFORMA cada item, o `.filter()` **SELECIONA** apenas os itens que passam num teste `true`/`false`:
  ```js
  const pokemonsFiltrados = pokemons.filter((pokemon) =>
    pokemon.name.toLowerCase().includes(searchTerm.toLowerCase())
  );
  ```
* **Por que `.toLowerCase()` dos dois lados?** Se o usuário digitar `"PIKACHU"` e o dado for `"Pikachu"`, a comparação direta falharia. Padronizamos os dois para minúsculas antes de comparar.
* **Busca também por número:** convertemos o `id` numérico para texto com `String()` e testamos com `.includes()`:
  ```js
  String(pokemon.id).includes(searchTerm)   // '25' dentro de 'Pikachu 25'
  ```

#### 2.3 Combinando Dois Critérios (Texto **E** Tipo)
* Filtros se somam com o operador lógico `&&`:
  ```js
  const bateComNome = pokemon.name.toLowerCase().includes(searchTerm.toLowerCase());
  const bateComTipo = selectedType === 'Todos' || pokemon.type === selectedType;
  return bateComNome && bateComTipo;
  ```
* O `'Todos' ||` é o "curinga": quando nenhum tipo está selecionado, esse critério vale para todos.

> [!TIP]
> **Estado derivado NÃO é estado:** `pokemonsFiltrados` é apenas uma variável recalculada a cada renderização. Não caia na tentação de criar `const [filtrados, setFiltrados] = useState(...)` — a fonte da verdade continua sendo `pokemons` + `searchTerm` + `selectedType`.

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Veja uma busca de contatos em tempo real — o esqueleto completo (componente + CSS + App) antes de você codar:

#### `src/BuscadorContatos.jsx`:
```jsx
import { useState } from 'react';
import './BuscadorContatos.css';

export function BuscadorContatos() {
  const contatos = ['Ana Silva', 'Bruno Souza', 'Carlos Eduardo', 'Diana Lima'];
  const [busca, setBusca] = useState('');

  // Recalculado a cada digitação — estado derivado, sem useState!
  const contatosFiltrados = contatos.filter((nome) =>
    nome.toLowerCase().includes(busca.toLowerCase())
  );

  return (
    <section className="agenda-container">
      <input
        className="agenda-input"
        type="text"
        placeholder="🔍 Buscar contato..."
        value={busca}
        onChange={(e) => setBusca(e.target.value)}
      />

      <ul className="agenda-lista">
        {contatosFiltrados.map((nome) => (
          // key = o próprio nome (dado único), NUNCA o index (Regra de Ouro do Step 05!)
          <li key={nome}>{nome}</li>
        ))}
      </ul>

      {contatosFiltrados.length === 0 && (
        <p className="agenda-vazia">Nenhum contato encontrado 😕</p>
      )}
    </section>
  );
}
```

#### `src/BuscadorContatos.css`:
```css
.agenda-container {
  max-width: 400px;
  margin: 2rem auto;
}

.agenda-input {
  width: 100%;
  padding: 0.75rem 1rem;
  border: 2px solid #cbd5e1;
  border-radius: 999px;
  font-size: 1rem;
}

.agenda-lista {
  list-style: none;
  padding: 0;
  display: grid;
  gap: 0.5rem;
  margin-top: 1rem;
}

.agenda-lista li {
  background: #ffffff;
  border-radius: 8px;
  padding: 0.75rem 1rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}

.agenda-vazia {
  text-align: center;
  color: #64748b;
}
```

#### Uso no `src/App.jsx`:
```jsx
import { Header } from './Header';
import { BuscadorContatos } from './BuscadorContatos';

export function App() {
  return (
    <div className="app-container">
      <Header />
      <BuscadorContatos />
    </div>
  );
}

export default App;
```

---

### 🛠️ 4. Desafio Ativo (Mão na Massa)

São **3 arquivos**: 2 novos (`PokemonFilters.jsx` + `.css`) e 1 reescrito por inteiro (`PokemonGrid.jsx`).

```text
src/PokemonFilters.jsx  ➜  recebe estado do Grid e exibe input+botões
src/PokemonGrid.jsx     ➜  DONO dos estados searchTerm e selectedType (aplica o .filter())
```

1. **Criar o painel de filtros (`src/PokemonFilters.jsx`):**
   ```jsx
   import './PokemonFilters.css';

   // Componente "burro": não guarda estado próprio, só lê e dispara setters que vêm do Pai
   export function PokemonFilters({ searchTerm, setSearchTerm, selectedType, setSelectedType }) {
     const tipos = ['Todos', 'Planta', 'Fogo', 'Agua', 'Eletrico', 'Normal', 'Veneno', 'Psiquico'];

     return (
       <section className="filters-container">
         <div className="search-box">
           <input
             type="text"
             placeholder="🔍 Buscar Pokémon por nome ou ID..."
             value={searchTerm}
             onChange={(e) => setSearchTerm(e.target.value)}
           />
         </div>

         <div className="type-buttons">
           {tipos.map((tipo) => (
             <button
               key={tipo}
               className={`btn-type btn-${tipo.toLowerCase()} ${selectedType === tipo ? 'ativo' : ''}`}
               onClick={() => setSelectedType(tipo)}
             >
               {tipo}
             </button>
           ))}
         </div>
       </section>
     );
   }
   ```

2. **Estilizar o painel (`src/PokemonFilters.css`):**
   ```css
   .filters-container {
     max-width: 1200px;
     margin: 0 auto;
     padding: 1.5rem 2rem 0;
     display: flex;
     flex-direction: column;
     gap: 1rem;
   }

   .search-box input {
     width: 100%;
     padding: 0.8rem 1.25rem;
     border: 2px solid #cbd5e1;
     border-radius: 999px;
     font-size: 1rem;
   }

   .search-box input:focus-visible {
     outline: 3px solid #38bdf8;
     outline-offset: 2px;
   }

   .type-buttons {
     display: flex;
     flex-wrap: wrap;
     gap: 0.5rem;
     justify-content: center;
   }

   .btn-type {
     border: 2px solid transparent;
     border-radius: 999px;
     padding: 0.4rem 1rem;
     font-weight: 600;
     font-size: 0.85rem;
     cursor: pointer;
     background: #e2e8f0;
     color: #334155;
     transition: transform 0.15s, filter 0.15s;
   }

   .btn-type:hover { transform: translateY(-2px); filter: brightness(0.95); }

   /* Anel branco marca o filtro selecionado (classe vem do ternário no JSX) */
   .btn-type.ativo {
     border-color: #ffffff;
     box-shadow: 0 0 0 2px #0f172a;
   }

   /* Cores por tipo (sem acento, batendo com as classes do Step 03/07) */
   .btn-todos     { background: #cbd5e1; }
   .btn-planta    { background: #57b952; color: #ffffff; }
   .btn-fogo      { background: #ff421d; color: #ffffff; }
   .btn-agua      { background: #268bf7; color: #ffffff; }
   .btn-eletrico  { background: #fbc02d; color: #333333; }
   .btn-normal    { background: #a8a878; color: #ffffff; }
   .btn-veneno    { background: #9f52c8; color: #ffffff; }
   .btn-psiquico  { background: #f59785; color: #ffffff; }
   ```

3. **Reescrever `src/PokemonGrid.jsx` — o arquivo final completo:**
   ```jsx
   import { useState, useEffect } from 'react';
   import { PokemonCard } from './PokemonCard';
   import { PokemonFilters } from './PokemonFilters';
   import './PokemonGrid.css';

   const tiposPT = {
     normal: 'Normal', fire: 'Fogo', water: 'Agua', electric: 'Eletrico',
     grass: 'Planta', ice: 'Gelo', fighting: 'Lutador', poison: 'Veneno',
     ground: 'Solo', flying: 'Voador', psychic: 'Psiquico', bug: 'Inseto',
     rock: 'Pedra', ghost: 'Fantasma', dragon: 'Dragao'
   };

   export function PokemonGrid() {
     const [pokemons, setPokemons] = useState([]);
     const [isLoading, setIsLoading] = useState(true);

     // NOVO: os dois controles da busca (o Grid é o DONO desses estados)
     const [searchTerm, setSearchTerm] = useState('');
     const [selectedType, setSelectedType] = useState('Todos');

     useEffect(() => {
       async function fetchPokemons() {
         try {
           const response = await fetch('https://pokeapi.co/api/v2/pokemon?limit=151');
           const data = await response.json();

           const detailedPokemons = await Promise.all(
             data.results.map(async (item) => {
               const pokeRes = await fetch(item.url);
               const pokeDetails = await pokeRes.json();

               return {
                 id: pokeDetails.id,
                 name: pokeDetails.name.charAt(0).toUpperCase() + pokeDetails.name.slice(1),
                 type: tiposPT[pokeDetails.types[0].type.name] ?? 'Normal',
                 types: pokeDetails.types.map((t) => tiposPT[t.type.name] ?? t.type.name),
                 image: pokeDetails.sprites.other['official-artwork'].front_default,
                 shinyImage: pokeDetails.sprites.other['official-artwork'].front_shiny
               };
             })
           );

           setPokemons(detailedPokemons);
         } catch (error) {
           console.error('Erro ao buscar Pokémons:', error);
         } finally {
           setIsLoading(false);
         }
       }

       fetchPokemons();
     }, []);

     // NOVO: estado derivado — recalculado a cada tecla digitada ou clique em botão
     const pokemonsFiltrados = pokemons.filter((pokemon) => {
       const matchesSearch =
         pokemon.name.toLowerCase().includes(searchTerm.toLowerCase()) ||
         String(pokemon.id).includes(searchTerm);

       const matchesType =
         selectedType === 'Todos' || pokemon.type === selectedType;

       return matchesSearch && matchesType;
     });

     if (isLoading) {
       return (
         <div className="loading-container">
           <h2>🔴 Carregando Pokédex Oficial...</h2>
           <p>Buscando os 151 Pokémons na PokéAPI...</p>
         </div>
       );
     }

     return (
       <section className="pokedex-body">
         {/* O painel recebe estado + setters do Pai (fluxo pai ➜ filho das Props do Step 03) */}
         <PokemonFilters
           searchTerm={searchTerm}
           setSearchTerm={setSearchTerm}
           selectedType={selectedType}
           setSelectedType={setSelectedType}
         />

         {pokemonsFiltrados.length === 0 ? (
           <h3 className="no-results">❌ Nenhum Pokémon encontrado!</h3>
         ) : (
           <main className="pokemon-grid">
             {pokemonsFiltrados.map((pokemon) => (
               <PokemonCard key={pokemon.id} pokemon={pokemon} />
             ))}
           </main>
         )}
       </section>
     );
   }
   ```

4. **Complementos de estilo (`src/PokemonGrid.css`) — adicione ao final:**
   ```css
   .no-results {
     text-align: center;
     color: #64748b;
     padding: 3rem 1rem;
   }
   ```

> [!TIP]
> **"Mas esperar função dentro de prop?"** Sim! Props viajam do pai para o filho (Step 03), e funções também são valores. O `<PokemonFilters />` segura o **controle** (input/botões) e entrega o resultado para cima; o `<PokemonGrid />` guarda a **decisão** (os estados). É o padrão *componente filho burro, pai inteligente*.

---

### 🧪 5. Teste de Validação

1. Abra o navegador (`http://localhost:5173`) e aguarde os 151 Pokémons carregarem.
2. Digite `"char"` na barra de pesquisa: a grade atualiza instantaneamente exibindo só Charmander, Charmeleon e Charizard.
3. Digite `"PIKACHU"` em MAIÚSCULO: o Pikachu aparece (o `.toLowerCase()` dos dois lados salvou o dia).
4. Apague a busca e clique no botão **"Fogo"**: apenas Pokémons do tipo Fogo permanecem.
5. Agora digite `"gligar"` com o botão "Fogo" ativo: os dois critérios se combinam.
6. Digite um nome inexistente (`"xyz123"`): deve aparecer **"❌ Nenhum Pokémon encontrado!"**.
7. Clique em **"Todos"** e confirme que a lista completa volta.

---

### ❓ 6. Quiz de Fixação (6 Questões de Múltipla Escolha)

#### Q1. O que é um Input Controlado no React?
- (A) Um campo de texto travado que não deixa o usuário digitar.
- (B) Um campo HTML cujo valor é mantido e controlado por um Estado (`useState`) do React.
- (C) Um botão com senha de segurança.
- (D) Um formulário enviado por e-mail.

> **Gabarito Comentado:** **(B)** Inputs controlados sincronizam o valor visível do campo com o estado interno do React a cada caractere digitado.

#### Q2. Como capturamos o texto exato que o usuário digitou dentro do evento `onChange` de um `<input>`?
- (A) `event.text`
- (B) `event.target.value`
- (C) `event.click.data`
- (D) `document.getValue()`

> **Gabarito Comentado:** **(B)** `event.target.value` acessa o valor atual do elemento HTML que disparou o evento.

#### Q3. Qual método do JavaScript converte o texto em minúsculas para que "PIKACHU" e "pikachu" funcionem igual na busca?
- (A) `.toUpperCase()`
- (B) `.toLowerCase()`
- (C) `.trim()`
- (D) `.slice()`

> **Gabarito Comentado:** **(B)** O `.toLowerCase()` padroniza os textos em minúsculas antes da comparação.

#### Q4. Qual é o objetivo do método `.filter()` ao realizar buscas em uma lista de objetos no React?
- (A) Excluir permanentemente os dados do banco de dados.
- (B) Retornar um novo array contendo apenas os elementos que satisfazem a condição de busca.
- (C) Ordenar os dados em ordem alfabética.
- (D) Mudar a cor dos cards.

> **Gabarito Comentado:** **(B)** O `.filter()` gera uma nova lista contendo apenas os itens que passam no teste lógico.

#### Q5. Como verificamos se uma string contém um pedaço de texto (ex: "Charmander" contém "char")?
- (A) `"Charmander".includes("char")`
- (B) `"Charmander" == "char"`
- (C) `"Charmander".has("char")`
- (D) `"Charmander".find("char")`

> **Gabarito Comentado:** **(A)** `.includes()` retorna `true` se a substring for encontrada.

#### Q6. Por que NÃO criamos um `useState` para guardar `pokemonsFiltrados`?
- (A) Porque `.filter()` não funciona dentro de estados.
- (B) Porque ele é um estado derivado: recalculado automaticamente a cada renderização a partir de `pokemons`, `searchTerm` e `selectedType`, que são a fonte da verdade.
- (C) Porque o React proíbe variáveis sem useState.
- (D) Para economizar memória armazenando a lista original duas vezes.

> **Gabarito Comentado:** **(B)** Guardar uma "cópia filtrada" em estado criaria duas fontes da verdade dessincronizadas. Estado derivado é computado, não armazenado.

---

### 📝 7. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Formulários e Inputs Controlados em React. Manipulação do evento onChange com e.target.value, filtragem de coleções em tempo real com .filter(), padronização de strings com .toLowerCase() e .includes(), combinação de critérios de busca, estados derivados (dado x cálculo) e o padrão pai-inteligente/filho-burro com passagem de setters via props."*
