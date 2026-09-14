# 🚀 Step 03: PokéAgenda — Dinamizando o Card com Props e JavaScript ES6

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica (PBL / Conceitual):** Domine a passagem de **Props** no React, Objetos Literais e **Desestruturação em JS ES6**, além de interpolação no JSX com chaves `{}`.
> * **🛠️ Trilha Prática (Projeto Integrador):** Transforme o componente estático `<PokemonCard />` em um componente 100% dinâmico e reutilizável para renderizar qualquer Pokémon da franquia.

---

### 🧩 1. O Problema Prático (Cenário PBL - Problem Statement)

**O Dilema dos 150 Arquivos Duplicados:**  
Com o card do Charmander pronto e aprovado, o coordenador da **PokéAgenda** pediu para adicionar o Squirtle, o Bulbasaur, o Pikachu e todos os outros 150 Pokémons. O estagiário começou a criar 150 arquivos diferentes (`CharmanderCard.jsx`, `SquirtleCard.jsx`, `BulbasaurCard.jsx`...), copiando e colando a mesma estrutura HTML e mudando apenas os textos e imagens manualmente. O projeto ficou gigantesco, pesado e impossível de gerenciar.

Duplicar arquivos e estruturas inteiras para mudar apenas dados viola o princípio fundamental do desenvolvimento moderno: **DRY** (*Don't Repeat Yourself* / Não Se Repita).

**A Pergunta-Chave PBL:**  
> *Como podemos utilizar as **Props do React** e a **Desestruturação de JavaScript ES6** para que um **único componente `<PokemonCard />`** seja capaz de exibir qualquer Pokémon passando apenas suas informações como parâmetro?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 O que são Props no React?
* **Propriedades (Props):** São argumentos/parâmetros que passamos para os componentes React, exatamente como passamos atributos para tags HTML (ex: `<img src="..." />`).
* **Fluxo Unidirecional de Dados:** As props sempre viajam do componente Pai (quem chama) para o componente Filho (quem recebe).
* **Imutabilidade:** As props são **somente leitura** (*read-only*). O componente filho as recebe para exibir na tela, nunca para alterá-las diretamente.

#### 2.2 JavaScript ES6+: Objetos Literais e Desestruturação (`Destructuring`)
* **Objeto Pokémon:** Agrupa os dados de um elemento em uma única variável:
  ```js
  const charmander = {
    id: "#004",
    name: "Charmander",
    type: "Fogo",
    image: "https://.../4.png"
  };
  ```
* **Desestruturação:** Permite extrair propriedades de um objeto diretamente em variáveis locais simples:
  ```js
  // Em vez de: pokemon.name, pokemon.id, pokemon.type
  const { id, name, type, image } = pokemon;
  ```

#### 2.3 Interpolação no JSX com Chaves `{}`
* No JSX, qualquer código colocado dentro de chaves `{}` é executado como JavaScript puro.
* **Textos Dinâmicos:** `<h2>{name}</h2>` exibe o nome contido na variável.
* **Atributos Dinâmicos:** `<img src={image} alt={`Foto do ${name}`} />`.
* **Classes Dinâmicas:** `className={`type-badge type-${type.toLowerCase()}`}` atribui automaticamente a classe correspondente ao tipo do Pokémon.

> [!TIP]
> **Dica de Mercado:** Você pode desestruturar a prop diretamente no parâmetro da função do componente: `export function PokemonCard({ pokemon }) { ... }`. Isso deixa o código muito mais limpo e legível!

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Veja como um componente de Produto recebe dados dinâmicos via Props:

#### Exemplo de Componente React (`src/CardProduto.jsx`):
```jsx
import './CardProduto.css';

// Recebe a prop "produto" e desestrutura suas propriedades
export function CardProduto({ produto }) {
  const { nome, preco, categoria, imagem } = produto;

  return (
    <article className="produto-card">
      <header className="produto-cabecalho">
        <h3>{nome}</h3>
        <span className="produto-preco">R$ {preco.toFixed(2)}</span>
      </header>

      <figure className="produto-imagem">
        <img src={imagem} alt={`Foto do produto ${nome}`} />
      </figure>

      {/* Classe dinâmica baseada na categoria */}
      <span className={`produto-badge badge-${categoria.toLowerCase()}`}>
        {categoria}
      </span>
    </article>
  );
}
```

#### Exemplo de Uso no Componente Pai (`src/App.jsx`):
```jsx
import { CardProduto } from './CardProduto';

export function App() {
  const tenis = {
    nome: "Tênis Runner",
    preco: 299.90,
    categoria: "Calcados",
    imagem: "https://via.placeholder.com/150"
  };

  const camiseta = {
    nome: "Camiseta DryFit",
    preco: 79.90,
    categoria: "Vestuario",
    imagem: "https://via.placeholder.com/150"
  };

  return (
    <div className="loja-container">
      {/* Reutilizando o mesmo componente com dados diferentes! */}
      <CardProduto produto={tenis} />
      <CardProduto produto={camiseta} />
    </div>
  );
}
```

---

### 🛠️ 4. Desafio Ativo (Mão na Massa)

Como desenvolvedor Frontend na PokéAgenda, sua missão é transformar o `<PokemonCard />` em um componente dinâmico inteligente:

1. **Atualizar `src/PokemonCard.jsx` para receber Props:**
   * Altere a declaração da função para aceitar a prop `{ pokemon }`:
     `export function PokemonCard({ pokemon })`
   * No início da função, desestruture o objeto:
     `const { id, name, type, image } = pokemon;`
   * Substitua os textos e links estáticos do JSX pelas variáveis dinâmicas:
     * `<span className="pokemon-id">{id}</span>`
     * `<h2 className="pokemon-name">{name}</h2>`
     * `<img src={image} alt={`Ilustração do ${name}`} />`
     * `<li className={`type-badge type-${type.toLowerCase()}`}>{type}</li>`
2. **Adicionar Estilos para Outros Tipos (`src/PokemonCard.css`):**
   * Adicione as classes de cores dos principais tipos no seu CSS:
     ```css
     .type-fogo { background-color: #ff421d; color: #ffffff; }
     .type-agua { background-color: #268bf7; color: #ffffff; }
     .type-planta { background-color: #57b952; color: #ffffff; }
     .type-eletrico { background-color: #fbc02d; color: #333333; }
     ```
3. **Alimentar e Reutilizar no `src/App.jsx`:**
   * Abra `src/App.jsx`.
   * Crie os objetos de teste antes do retorno da função:
     ```jsx
     const charmander = {
       id: "#004",
       name: "Charmander",
       type: "Fogo",
       image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/4.png"
     };

     const squirtle = {
       id: "#007",
       name: "Squirtle",
       type: "Agua",
       image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/7.png"
     };

     const bulbasaur = {
       id: "#001",
       name: "Bulbasaur",
       type: "Planta",
       image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/1.png"
     };
     ```
   * Renderize os três cards no JSX:
     ```jsx
     <div className="cards-grid">
       <PokemonCard pokemon={charmander} />
       <PokemonCard pokemon={squirtle} />
       <PokemonCard pokemon={bulbasaur} />
     </div>
     ```

---

### 🧪 5. Teste de Validação

1. Salve os arquivos e abra o navegador (`http://localhost:5173`).
2. Verifique se os **três Pokémons diferentes** (Charmander, Squirtle e Bulbasaur) aparecem na tela lado a lado.
3. Confirme se as cores das etiquetas de tipo mudaram dinamicamente (Vermelho para Fogo, Azul para Água, Verde para Planta).
4. Note que você utilizou **um único arquivo de componente** (`PokemonCard.jsx`) para renderizar todos eles!

---

### ❓ 6. Quiz de Fixação (6 Questões de Múltipla Escolha)

#### Q1. No React, o que são Props?
- (A) São comandos do banco de dados para salvar informações no servidor.
- (B) São propriedades passadas de um componente Pai para um Filho para exibir dados dinâmicos.
- (C) São métodos de segurança do navegador contra vírus.
- (D) São extensões instaladas no VS Code.

> **Gabarito Comentado:** **(B)** Props funcionam como os argumentos de uma função, permitindo enviar informações do componente que chama para o componente que renderiza.

#### Q2. Qual recurso do JavaScript ES6 permite extrair propriedades de um objeto de forma direta (ex: `const { id, name } = pokemon;`)?
- (A) Desestruturação de Objetos (*Destructuring*)
- (B) JSON Stringify
- (C) Método `concat()`
- (D) Laço `while`

> **Gabarito Comentado:** **(A)** A desestruturação permite desembalar propriedades de objetos em variáveis locais simples.

#### Q3. No JSX, qual caractere usamos para injetar e executar expressões JavaScript dentro da marcação visual?
- (A) Parênteses `()`
- (B) Colchetes `[]`
- (C) Chaves `{}`
- (D) Aspas duplas `""`

> **Gabarito Comentado:** **(C)** As chaves `{}` indicam ao JSX que o conteúdo interno deve ser avaliado como código JavaScript.

#### Q4. Qual das alternativas abaixo representa corretamente a passagem de uma prop chamada `pokemon` para o componente `<PokemonCard />`?
- (A) `<PokemonCard pokemon={charmander} />`
- (B) `<PokemonCard -> charmander />`
- (C) `<PokemonCard: charmander>`
- (D) `<PokemonCard (charmander) />`

> **Gabarito Comentado:** **(A)** As props são passadas no padrão `nomeDaProp={valor}` semelhante a atributos HTML.

#### Q5. No React, o que acontece se o componente filho tentar alterar o valor de uma prop recebida?
- (A) O componente pai atualiza instantaneamente.
- (B) O React não permite, pois Props são somente leitura (*read-only*).
- (C) O navegador recarrega a página.
- (D) A prop é convertida em string.

> **Gabarito Comentado:** **(B)** Props são estritamente imutáveis no componente que as recebe, garantindo previsibilidade no fluxo de dados.

#### Q6. Qual é a principal vantagem de usar Props em vez de duplicar componentes?
- (A) O site carrega em resolução 4K.
- (B) Reutilização de código: um único componente pode renderizar centenas de itens diferentes sem duplicar arquivos.
- (C) Elimina a necessidade de usar HTML e CSS.
- (D) Permite criar sites sem navegador.

> **Gabarito Comentado:** **(B)** Props viabilizam a reutilização máxima de templates e componentes na interface.

---

### 📝 7. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Dinamização de Interfaces e Passagem de Props em React. Uso de objetos literais e desestruturação em JS ES6, interpolação de dados dinâmicos com chaves no JSX, classes dinâmicas e reutilização do componente PokemonCard para múltiplos registros."*
