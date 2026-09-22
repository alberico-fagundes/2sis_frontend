# 🚀 Step 05: PokéAgenda — Grid Responsivo e Renderização de Listas (`.map()` e `key`)

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica ( / Conceitual):** Domine a renderização dinâmica de listas em React com o método `.map()`, a obrigatoriedade da prop `key`, e a criação de layouts responsivos com **CSS Grid Layout** (`repeat(auto-fill)`).
> * **🛠️ Trilha Prática ():** Construa a estrutura de dados em `src/pokemons.js` e o componente de grade `<PokemonGrid />` para exibir múltiplos Pokémons de forma automática e responsiva.

---

### 🧩 1. O Problema Prático (Cenário  - Problem Statement)

**O Dilema do Copia e Cola Repetitivo no `App.jsx`:**  
No passo anterior, conseguimos usar Props para renderizar o Charmander, o Squirtle e o Bulbasaur. Porém, o estagiário da **PokéAgenda** tentou adicionar os 151 Pokémons da primeira geração escrevendo a tag `<PokemonCard pokemon={...} />` linha por linha 151 vezes dentro do arquivo `App.jsx`. O código ficou gigante, poluído, com mais de 300 linhas, e se precisarmos mudar a estrutura da lista, teremos que alterar linha por linha manualmente.

Escrever tags manualmente para cada item de uma coleção viola a automação do desenvolvimento moderno.

**A Pergunta-Chave :**  
> *Como podemos utilizar o método **`.map()` do JavaScript** e a **Prop `key` do React** junto com o **CSS Grid** para transformar um Array de dados em uma grade de cards bonita, responsiva e 100% automática?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 O Método `.map()` do JavaScript ES6
* **O que faz o `.map()`:** É um método de arrays que percorre cada item de uma lista, aplica uma transformação e retorna um **novo array** com os resultados.
* **Transformando Dados em JSX:** No React, usamos o `.map()` para converter uma lista de objetos de dados (ex: dados de Pokémons) em uma lista de elementos visuais JSX (`<PokemonCard />`).
  ```js
  // Exemplo de transformação simples
  const nomes = ["Pikachu", "Charmander", "Squirtle"];
  const elementosJSX = nomes.map(nome => <h2>{nome}</h2>);
  ```

#### 2.2 A Regra da Prop `key` no React
* **O que é a `key`:** É um atributo especial e obrigatório que você **deve** passar quando renderiza elementos em uma lista (ex: `key={pokemon.id}`).
* **Por que o React exige a `key`:** A `key` funciona como um "RG" ou "CPF" único para cada card. Ela ajuda o React a saber exatamente qual item mudou, foi adicionado ou removido, garantindo alta performance na atualização da tela.
* **O que NUNCA usar como `key`:** Evite usar o índice do array (`index`). Sempre prefira o `id` único do próprio dado.

#### 2.3 Diferença Essencial: Quando usar `.js` vs `.jsx`?
* **Arquivos `.js` (JavaScript Puro):** Usados para arquivos que contêm **apenas dados ou funções de lógica**, SEM NENHUMA TAG HTML/JSX (ex: `src/pokemons.js` com a lista de Pokémons).
* **Arquivos `.jsx` (Componentes React):** Usados para arquivos que **retornam interface visual com tags HTML/JSX** (ex: `src/PokemonCard.jsx` e `src/PokemonGrid.jsx`).

> [!NOTE]
> **Dica de Organização:** O arquivo `pokemons.js` é uma **base de dados mockada (simulada)**. Como ele possui apenas um Array de Objetos JavaScript puro `[{ id: 1, name: 'Bulbasaur' }]`, ele deve usar a extensão `.js`!

#### 2.4 CSS3 Moderno: CSS Grid Layout Responsivo
* **Display Grid (`display: grid`):** Transforma o contêiner em uma grade bidimensional (linhas e colunas).
* **`grid-template-columns: repeat(auto-fill, minmax(220px, 1fr))`:**
  * `repeat()`: Repete a criação de colunas automaticamente.
  * `auto-fill`: Preenche o espaço disponível com quantas colunas couberem na tela.
  * `minmax(220px, 1fr)`: Garante que cada card meça no mínimo `220px` e no máximo se expanda igualmente (`1fr`).
* **Propriedade `gap`:** Define o espaçamento uniforme entre os cards na grade sem precisar de margens manuais.

> [!TIP]
> **Regra de Ouro da Lista:** Toda vez que você abrir um `.map()` dentro do JSX, o primeiro elemento retornado dentro do parênteses **deve obrigatoriamente** ter a prop `key` preenchida com um valor único!

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Veja como renderizar uma lista de filmes usando `.map()` e CSS Grid:

#### Exemplo de Componente React (`src/GaleriaFilmes.jsx`):
```jsx
import './GaleriaFilmes.css';

export function GaleriaFilmes() {
  const filmes = [
    { id: 101, titulo: "Matrix", ano: 1999 },
    { id: 102, titulo: "Interstellar", ano: 2014 },
    { id: 103, titulo: "Inception", ano: 2010 }
  ];

  return (
    <main className="filmes-grid">
      {/* O .map percorre o array e retorna um elemento JSX para cada item */}
      {filmes.map((filme) => (
        <div key={filme.id} className="filme-card">
          <h3>{filme.titulo}</h3>
          <p>Lançamento: {filme.ano}</p>
        </div>
      ))}
    </main>
  );
}
```

#### Exemplo de Estilo CSS (`src/GaleriaFilmes.css`):
```css
/* Grade responsiva que se adapta do celular ao monitor */
.filmes-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 1.5rem;
  padding: 2rem;
}
```

---

### 🛠️ 4. Desafio Ativo (Mão na Massa)

Sua missão na equipe da PokéAgenda é organizar os dados em um arquivo de dados separado e criar a grade de Pokémons automática:

1. **Criar a base de dados (`src/pokemons.js`):**
   * Crie o arquivo `src/pokemons.js` e exporte um array com pelo menos 6 Pokémons:
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
       },
       {
         id: 39,
         name: "Jigglypuff",
         type: "Fada",
         image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/39.png"
       },
       {
         id: 94,
         name: "Gengar",
         type: "Fantasma",
         image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/94.png"
       }
     ];
     ```

2. **Criar o componente de grade (`src/PokemonGrid.jsx`):**
   * Crie o arquivo `src/PokemonGrid.jsx`.
   * Importe o `PokemonCard` e o array `pokemonsIniciais`.
   * Retorne uma tag `<main className="pokemon-grid">`.
   * Use `.map()` no array para renderizar cada `<PokemonCard key={pokemon.id} pokemon={pokemon} />`.

3. **Estilizar a grade (`src/PokemonGrid.css`):**
   * Crie o arquivo `src/PokemonGrid.css` e importe no topo do `PokemonGrid.jsx`.
   * Aplique `display: grid;`, `grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));`, `gap: 1.5rem;` e `max-width: 1200px; margin: 0 auto;`.

4. **Atualizar o `App.jsx`:**
   * Importe o `<PokemonGrid />` e renderize-o entre o `<Header />` e o `<Footer />`.

---

### 🧪 5. Teste de Validação

1. Abra o navegador (`http://localhost:5173`).
2. Confirme que todos os 6 Pokémons aparecem organizados em uma grade bonita.
3. Redimensione a janela do navegador (ou simule tela de celular no `F12`) e observe os cards se reorganizarem automaticamente de 4 colunas para 2 e depois para 1 coluna.
4. Abra o Console do Navegador (`F12 -> Console`) e verifique que **NENHUM aviso em amarelo** sobre *"Warning: Each child in a list should have a unique 'key' prop"* está sendo exibido.

---

### ❓ 6. Quiz de Fixação (6 Questões de Múltipla Escolha)

#### Q1. Qual método do JavaScript é o mais recomendado para transformar um Array de dados em uma lista de elementos visuais JSX no React?
- (A) `.filter()`
- (B) `.map()`
- (C) `.push()`
- (D) `.forEach()`




#### Q2. Por que o React exige o uso da prop `key` ao renderizar listas?
- (A) Para definir a cor de fundo do card.
- (B) Para permitir que o leitor de tela leia o código em inglês.
- (C) Para identificar univocamente cada elemento e otimizar a atualização da interface.
- (D) Para salvar a lista no banco de dados.



#### Q3. O que deve ser preferencialmente utilizado como valor para a prop `key` em uma lista de Pokémons?
- (A) Um texto aleatório.
- (B) O nome da cor do card.
- (C) O `id` único de cada Pokémon vindo dos dados.
- (D) A palavra "key".



#### Q4. No CSS Grid, qual regra permite criar colunas que se adaptam e dobram automaticamente conforme a largura da tela do dispositivo?
- (A) `grid-template-columns: 200px 200px 200px;`
- (B) `grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));`
- (C) `display: block;`
- (D) `flex-direction: column;`




#### Q5. Em um componente React, o que acontece se esquecermos de passar a prop `key` dentro do `.map()`?
- (A) O computador desliga.
- (B) A aplicação funciona, mas o React exibe um aviso (Warning) no console sobre perda de performance e rastreamento.
- (C) O CSS para de funcionar.
- (D) A lista fica invisível.




#### Q6. Qual é o papel da propriedade `gap` no CSS Grid?
- (A) Definir a transparência da imagem.
- (B) Criar um espaçamento uniforme entre os elementos da grade.
- (C) Aumentar o tamanho do texto.
- (D) Mudar a cor da borda.



---
