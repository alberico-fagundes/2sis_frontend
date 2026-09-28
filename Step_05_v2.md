# 🚀 Step 05: PokéAgenda — Renderização Automática de Listas (`.map()`, `key` e CSS Grid)

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica ( / Conceitual):** Domine a renderização dinâmica de listas no React com o método **`.map()`**, a obrigatoriedade da **prop `key`** e o layout responsivo com **CSS Grid** (`repeat`, `auto-fill`, `minmax`).
> * **🛠️ Trilha Prática (Projeto Integrador):** Crie a base de dados `src/pokemons.js` e o componente `<PokemonGrid />`, que transforma o array de Pokémons em uma grade automática e responsiva de cards.

---

### 🧩 1. O Problema Prático (Cenário  - Problem Statement)

**O Dilema do Copia e Cola no `App.jsx`:**  
No Step 03, conquistamos as Props e renderizamos três cards manualmente:

```jsx
<PokemonCard pokemon={charmander} />
<PokemonCard pokemon={squirtle} />
<PokemonCard pokemon={bulbasaur} />
```

O coordenador da **PokéAgenda** então pediu a coleção completa: os 151 Pokémons da primeira geração. O estagiário tentou escrever a tag `<PokemonCard pokemon={...} />` **151 vezes**, linha por linha, e criou 151 variáveis de dados no `App.jsx`. O arquivo passou de 600 linhas, ficou ilegível, e qualquer mudança na estrutura da lista exigiria editar 151 linhas à mão.

Temos um **array de dados** e queremos um **array de cards** — isso é exatamente o trabalho de uma linha de produção, e o JavaScript já inventou essa máquina: o `.map()`.

**A Pergunta-Chave :**  
> *Como podemos utilizar o método **`.map()` do JavaScript**, a **prop `key` do React** e o **CSS Grid** para transformar automaticamente um Array de dados em uma grade de cards responsiva?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 O Método `.map()` — A Esteira de Transformação
* **A analogia:** imagine uma esteira de fábrica. Você entra com 3 frutas cruas de um lado, e sai 3 frutas embaladas do outro. A esteira aplica **a mesma regra** em cada item, e o resultado **tem a mesma quantidade** de itens da entrada.
* **No código:** o `.map()` percorre cada item de um array, aplica uma transformação e retorna um **novo array** com os resultados:
  ```js
  const nomes = ["Pikachu", "Charmander", "Squirtle"];

  const titulos = nomes.map((nome) => <h2>{nome}</h2>);
  // Resultado: [<h2>Pikachu</h2>, <h2>Charmander</h2>, <h2>Squirtle</h2>]
  ```
* **No JSX:** tudo que estiver dentro de chaves `{}` é JavaScript puro. Se colocarmos um `.map()` dentro de `{}`, o React recebe um array de elementos e renderiza todos eles:
  ```jsx
  <div>
    {nomes.map((nome) => (
      <h2>{nome}</h2>
    ))}
  </div>
  ```

#### 2.2 A Prop `key` — O RG de Cada Card
* **O que é:** um atributo especial e **obrigatório** que acompanha cada elemento criado dentro de um `.map()`:
  ```jsx
  <PokemonCard key={pokemon.id} pokemon={pokemon} />
  ```
* **Por que o React exige:** o `key` funciona como um "RG" único de cada card. Quando a lista muda (um item é adicionado, removido ou reordenado), é a `key` que diz ao React **qual** card específico precisa ser atualizado — sem redesenhar a tela inteira. Isso garante performance e comportamento correto.
* **O que NUNCA usar como `key`:** o índice do array (`index`). A posição "3" muda quando a lista é filtrada ou reordenada; o `id` do dado nunca muda.

  ```jsx
  <PokemonCard key={pokemon.id} ... />  // ✅ ID real do Pokémon
  <PokemonCard key={index} ... />       // ❌ posição na lista
  ```

#### 2.3 CSS Grid: A Grade que Se Adapta Sozinha
* **`display: grid`:** transforma o contêiner em uma grade bidimensional (linhas e colunas).
* **A linha mágica da responsividade — disseque com calma:**
  ```text
  grid-template-columns: repeat( auto-fill , minmax(220px, 1fr) );
                         ──────   ────────   ──────────────────
                           (1)      (2)              (3)
  ```
  1. **`repeat()`:** "repita a definição de coluna quantas vezes couber".
  2. **`auto-fill`:** calcule automaticamente **quantas colunas cabem** na largura atual da tela.
  3. **`minmax(220px, 1fr)`:** cada coluna tem **mínimo 220px** e **máximo o espaço restante dividido igualmente** (`1fr`).
* **Resultado:** em um monitor largo cabem 4 colunas; no celular, 1. Sem nenhuma media query!
* **`gap: 1.5rem`:** espaçamento uniforme entre linhas e colunas, sem precisar de margens manuais nos cards.

> [!TIP]
> **Qual extensão usar: `.js` ou `.jsx`?** Regra simples: se o arquivo **tem tags JSX**, use `.jsx` (`PokemonGrid.jsx`). Se o arquivo tem **apenas dados e lógica**, use `.js` (`pokemons.js` guarda só um array de objetos, sem nenhuma tag!).

> [!TIP]
> **Regra de Ouro da Lista:** toda vez que você abrir um `.map()` dentro do JSX, o primeiro elemento retornado **deve** ter a prop `key` com um valor único. Sem `key`, o React exibe um warning amarelo no console.

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Veja uma estante de livros sendo montada automaticamente a partir de um array. **Este exemplo mostra TUDO: o componente, o CSS e o `App.jsx` final usando a peça** — antes de você codar o seu:

#### 1. O Componente de Grade (`src/GaleriaLivros.jsx`):
```jsx
import './GaleriaLivros.css';

export function GaleriaLivros() {
  // Dados de exemplo dentro do próprio componente (no nosso desafio,
  // os Pokémons morarão em um arquivo separado — você verá o porquê já já!)
  const livros = [
    { id: 1, titulo: 'Dom Casmurro', autor: 'Machado de Assis' },
    { id: 2, titulo: 'O Hobbit', autor: 'J.R.R. Tolkien' },
    { id: 3, titulo: '1984', autor: 'George Orwell' },
    { id: 4, titulo: 'Fahrenheit 451', autor: 'Ray Bradbury' }
  ];

  return (
    <section className="galeria-grid">
      {/* A esteira: para CADA livro, nasce um <article> */}
      {livros.map((livro) => (
        <article key={livro.id} className="livro-card">
          <h3>{livro.titulo}</h3>
          <p>{livro.autor}</p>
        </article>
      ))}
    </section>
  );
}
```

#### 2. O Estilo da Grade (`src/GaleriaLivros.css`):
```css
.galeria-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
  gap: 1.5rem;
  padding: 2rem;
}

.livro-card {
  background: #ffffff;
  border-radius: 12px;
  padding: 1rem;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease;
}

.livro-card:hover {
  transform: translateY(-4px);
}
```

#### 3. Como Importar e Usar no Arquivo Principal (`src/App.jsx`):
```jsx
// PASSO 1: importe a nova peça
import { Header } from './Header';
import { Footer } from './Footer';
import { GaleriaLivros } from './GaleriaLivros';

// PASSO 2: monte a tela
export function App() {
  return (
    <div className="app-container">
      <Header />
      <GaleriaLivros />
      <Footer />
    </div>
  );
}

export default App;
```

> [!IMPORTANT]
> **Por que os Pokémons terão um arquivo de dados separado?** No Step 07 vamos conectar a PokéAgenda à **PokéAPI** (a fonte oficial dos 151 Pokémons na nuvem). Se os dados estiverem espalhados dentro dos componentes, teremos que caçá-los para substituí-los. Guardando tudo em um único arquivo `src/pokemons.js`, a troca futura será rápida e segura.

---

### 🛠️ 4. Desafio Ativo (Mão na Massa)

Sua missão na equipe da PokéAgenda é montar a linha de produção de cards. São **3 arquivos novos**, cada um com uma responsabilidade única:

```text
src/pokemons.js  ➜  src/PokemonGrid.jsx  ➜  src/App.jsx
   (os dados)        (a esteira .map())      (a tela final)
```

1. **Criar a base de dados (`src/pokemons.js`):**
   * Crie o arquivo `src/pokemons.js` (extensão `.js`, pois só há dados, sem JSX).
   * Exporte um array com 4 Pokémons usando *named export*:
     ```js
     export const pokemonsIniciais = [
       {
         id: 1,
         name: "Bulbasaur",
         type: "Planta",
         image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/1.png"
       },
       {
         id: 4,
         name: "Charmander",
         type: "Fogo",
         image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/4.png"
       },
       {
         id: 7,
         name: "Squirtle",
         type: "Agua",
         image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/7.png"
       },
       {
         id: 25,
         name: "Pikachu",
         type: "Eletrico",
         image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png"
       }
     ];
     ```

2. **Criar a esteira de produção (`src/PokemonGrid.jsx`):**
   * Crie o arquivo `src/PokemonGrid.jsx`.
   * Importe o `<PokemonCard />`, o array `pokemonsIniciais` e o CSS da grade.
   * Retorne um `<main className="pokemon-grid">` com o `.map()` que gera os cards **com `key`**:
     ```jsx
     import { PokemonCard } from './PokemonCard';
     import { pokemonsIniciais } from './pokemons';
     import './PokemonGrid.css';

     export function PokemonGrid() {
       return (
         <main className="pokemon-grid">
           {pokemonsIniciais.map((pokemon) => (
             <PokemonCard key={pokemon.id} pokemon={pokemon} />
           ))}
         </main>
       );
     }
     ```

3. **Estilizar a grade (`src/PokemonGrid.css`):**
   * Crie o arquivo `src/PokemonGrid.css` (já importado no passo 2).
   * Aplique a grade autossustentável e centralize o conteúdo:
     ```css
     .pokemon-grid {
       display: grid;
       grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
       gap: 1.5rem;
       padding: 2rem;
       max-width: 1200px;
       margin: 0 auto;
     }
     ```

4. **Renderizar no `App.jsx` — o arquivo final fica exatamente assim:**
   * Remova os objetos `charmander`, `squirtle` e `bulbasaur` e as três tags `<PokemonCard />` criadas no Step 03 (a grade agora faz esse trabalho).
   ```jsx
   import { Header } from './Header';
   import { Footer } from './Footer';
   import { PokemonGrid } from './PokemonGrid';

   export function App() {
     return (
       <div className="app-container">
         <Header />
         <PokemonGrid />
         <Footer />
       </div>
     );
   }

   export default App;
   ```

5. **(Toque Visual Opcional) Resgatando o "#004":**
   * No Step 03 o número era o texto `"#004`; agora o `id` é o número `4` (necessário para a `key` e para a PokéAPI do Step 07).
   * Para o card exibir `#004` novamente, troque, dentro de `src/PokemonCard.jsx`:
     ```jsx
     <span className="pokemon-id">{id}</span>
     ```
     por:
     ```jsx
     <span className="pokemon-id">{`#${String(id).padStart(3, '0')}`}</span>
     ```
   * `String(id)` converte o número em texto e `padStart(3, '0')` completa com zeros à esquerda até ter 3 dígitos (`1` vira `001`).

---

### 🧪 5. Teste de Validação

1. No terminal, execute `npm run dev` e abra `http://localhost:5173`.
2. Confirme que os **4 Pokémons** aparecem lado a lado em uma grade (nenhum card foi escrito à mão!).
3. Redimensione a janela do navegador (ou simule um celular no `F12`): os cards devem se reorganizar sozinhos de 4 ➜ 2 ➜ 1 coluna.
4. Abra o Console do Navegador (`F12` ➜ Console) e confirme que **NÃO existe** o aviso amarelo *"Warning: Each child in a list should have a unique 'key' prop"*.
5. Inspecione a grade (`F12` ➜ Elements) e confirme o `<main class="pokemon-grid">` com `display: grid` no painel de estilos.

---

### ❓ 6. Quiz de Fixação (6 Questões de Múltipla Escolha)

#### Q1. Qual método do JavaScript é o mais recomendado para transformar um Array de dados em uma lista de elementos visuais JSX no React?
- (A) `.filter()`
- (B) `.map()`
- (C) `.push()`
- (D) `.forEach()`

> **Gabarito Comentado:** **(B)** O método `.map()` percorre o array e retorna um novo array com a transformação JSX de cada elemento.

#### Q2. Por que o React exige o uso da prop `key` ao renderizar listas?
- (A) Para definir a cor de fundo do card.
- (B) Para permitir que o leitor de tela leia o código em inglês.
- (C) Para identificar univocamente cada elemento e otimizar a atualização da interface.
- (D) Para salvar a lista no banco de dados.

> **Gabarito Comentado:** **(C)** A prop `key` funciona como um identificador único que permite ao React rastrear quais itens mudaram ou foram removidos com alta performance.

#### Q3. O que deve ser preferencialmente utilizado como valor para a prop `key` em uma lista de Pokémons?
- (A) Um texto aleatório.
- (B) O índice do array (`index`).
- (C) O `id` único de cada Pokémon vindo dos dados.
- (D) A palavra "key".

> **Gabarito Comentado:** **(C)** O `id` único do objeto de dados é o valor ideal para a `key` porque não muda durante a execução do aplicativo — diferente da posição do item na lista.

#### Q4. No CSS Grid, qual regra permite criar colunas que se adaptam e dobram automaticamente conforme a largura da tela do dispositivo?
- (A) `grid-template-columns: 200px 200px 200px;`
- (B) `grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));`
- (C) `display: block;`
- (D) `flex-direction: column;`

> **Gabarito Comentado:** **(B)** A combinação de `repeat(auto-fill, minmax(...))` cria um grid 100% responsivo sem a necessidade de media queries complexas.

#### Q5. Em um componente React, o que acontece se esquecermos de passar a prop `key` dentro do `.map()`?
- (A) O computador desliga.
- (B) A aplicação funciona, mas o React exibe um aviso (Warning) no console sobre perda de performance e rastreamento.
- (C) O CSS para de funcionar.
- (D) A lista fica invisível.

> **Gabarito Comentado:** **(B)** O React ainda tenta renderizar, mas emite um alerta no console avisando sobre problemas potenciais de reconstrução da DOM.

#### Q6. Qual é o papel da propriedade `gap` no CSS Grid?
- (A) Definir a transparência da imagem.
- (B) Criar um espaçamento uniforme entre os elementos da grade.
- (C) Aumentar o tamanho do texto.
- (D) Mudar a cor da borda.

> **Gabarito Comentado:** **(B)** A propriedade `gap` define a distância entre colunas e linhas do grid de forma limpa e moderna, sem margens manuais.

---

### 📝 7. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Renderização Dinâmica de Listas em React e Layouts Responsivos. Uso do método JS ES6 .map() para iteração de arrays de objetos, obrigatoriedade e importância da prop key para reconciliação da DOM virtual, separação de dados em módulo .js e estilização de grades adaptáveis com CSS Grid Layout (repeat, auto-fill e minmax)."*
