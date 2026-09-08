# 🚀 Step 02: PokéAgenda — O Card Individual (<PokemonCard />), Props e Estilização Dinâmica

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Duração:** 50 Minutos  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica (PBL / Conceitual):** Compreenda o uso do HTML5 Semântico (`<article>`), Variáveis CSS (`:root`), Desestruturação JS e a passagem de **Props** no React.
> * **🛠️ Trilha Prática (Projeto Integrador):** Construa o componente Reutilizável `<PokemonCard />` em `src/PokemonCard.jsx` e aplique estilos dinâmicos com Variáveis CSS em `src/PokemonCard.css`.

---

### 🧩 1. O Problema Prático (Cenário PBL - Problem Statement)

**O Dilema das Cartas Hardcoded com Código Duplicado:**  
A equipe de desenvolvimento da **PokéAgenda** precisa desenhar a exibição dos Pokémons na tela. O estagiário tentou escrever o HTML e o CSS manualmente para cada um dos 151 Pokémons. Para o Charmander, ele criou um HTML fixo com fundo vermelho; para o Squirtle, copiou e colou as 30 linhas de HTML trocando apenas o nome e mudando a cor de fundo para azul manualmente no CSS. O arquivo `App.jsx` ficou com mais de 4.500 linhas de código duplicado, impossível de dar manutenção ou carregar dinamicamente vindo de uma API.

Escrever código fixo para cada item de uma lista torna a aplicação pesada, inflexível e inviável para produção.

**A Pergunta-Chave PBL:**  
> *Como podemos utilizar **Props no React**, **Desestruturação JS** e **Variáveis CSS (`:root`)** para criar um único componente `<PokemonCard />` capaz de renderizar qualquer Pokémon com suas cores e atributos específicos automaticamente?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 HTML5 Semântico: O Elemento `<article>` e Estrutura de Card
* **Tag `<article>`:** Representa uma composição independente e autônoma em um documento (ex: um post de blog, um produto de e-commerce ou um card de Pokémon).
* **Organização Interna do Card:**
  * `<header>` interno: Contém o número de identificação do Pokémon (`#001`, `#004`) e o nome.
  * `<figure>` e `<img>`: Encapsula a ilustração do Pokémon.
  * `<ul>` e `<li>`: Lista não ordenada para exibir as tags de tipos (ex: *Fogo*, *Voador*).

#### 2.2 CSS3 Moderno: Variáveis CSS (`:root`), Badges e Efeitos Hover 3D
* **Variáveis CSS (`Custom Properties`):** Permite armazenar valores de cores reutilizáveis no seletor `:root`.
  * Exemplo: `--type-fire: #ff421d; --type-water: #268bf7; --type-grass: #57b952;`.
* **Transições e Animações de Hover:** Uso de `transition: transform 0.3s ease, box-shadow 0.3s ease` para criar um efeito de elevação 3D ao passar o mouse (`transform: translateY(-8px)`).
* **Badges de Tipo:** Uso de `border-radius: 12px`, `padding: 0.25rem 0.75rem` e `text-transform: uppercase` para criar pílulas/etiquetas visuais marcantes.

#### 2.3 JavaScript ES6+: Desestruturação de Objetos e Manipulação de Strings
* **Desestruturação de Objetos (`Destructuring`):** Técnica para extrair propriedades de objetos diretamente em variáveis locais.
  * Exemplo: `const { name, id, types, image } = pokemon;`.
* **Capitalização de Strings:** Função em JS puro para transformar a primeira letra em maiúscula:
  * `const nomeFormatado = name.charAt(0).toUpperCase() + name.slice(1);`.
* **Formatação de Números (`padStart`):** Adiciona zeros à esquerda para formatar IDs (`String(4).padStart(3, '0')` vira `'004'`).

#### 2.4 React: Passagem e Recebimento de Props
* **O que são Props (Propriedades)?** São os "argumentos" que passamos para os componentes React, semelhantes aos atributos de tags HTML. Permitem tornar os componentes dinâmicos e reutilizáveis.
* **Fluxo Unidirecional de Dados:** No React, as props fluem do componente Pai (ex: `App`) para o componente Filho (ex: `PokemonCard`). As props são **somente leitura** (*read-only*).

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Veja como criar um componente reutilizável que recebe dados via **Props** e aplica estilos dinâmicos:

#### Exemplo de Componente React (`src/CartaoProduto.jsx`):
```jsx
import './CartaoProduto.css';

// Recebendo e desestruturando props no próprio parâmetro da função
export function CartaoProduto({ produto }) {
  // Desestruturação das propriedades do objeto produto
  const { nome, preco, categoria, imagem } = produto;

  return (
    <article className={`cartao-item categoria-${categoria.toLowerCase()}`}>
      <header className="cartao-cabecalho">
        <h3>{nome}</h3>
        <span className="cartao-preco">R$ {preco.toFixed(2)}</span>
      </header>

      <figure className="cartao-imagem-conteiner">
        <img src={imagem} alt={`Fotografia do produto ${nome}`} />
      </figure>

      <span className="cartao-badge">{categoria}</span>
    </article>
  );
}
```

#### Exemplo de CSS com Variáveis (`src/CartaoProduto.css`):
```css
/* Declaração de Variáveis de Cores Globais */
:root {
  --cor-eletronicos: #2563eb;
  --cor-vestuario: #db2777;
  --cor-fundo-card: #ffffff;
}

.cartao-item {
  background-color: var(--cor-fundo-card);
  border-radius: 16px;
  padding: 1.5rem;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease;
}

.cartao-item:hover {
  transform: translateY(-6px);
}

.categoria-eletronicos .cartao-badge {
  background-color: var(--cor-eletronicos);
  color: #ffffff;
}
```

---

### 🛠️ 4. Desafio Ativo PBL (Mão na Massa - 30 Minutos)

Como desenvolvedor Frontend na PokéAgenda, sua missão é criar o componente `<PokemonCard />`:

1. **Criar os arquivos:**
   * Crie o arquivo `src/PokemonCard.jsx` e o arquivo `src/PokemonCard.css`.
2. **Definir o componente funcional `<PokemonCard />`:**
   * Crie a função `PokemonCard` aceitando a prop `{ pokemon }`.
   * Faça a desestruturação do objeto `pokemon` extraindo: `id`, `name`, `types`, `image`.
   * Formate o id com 3 dígitos (ex: `#004`) usando `String(id).padStart(3, '0')`.
   * Formate o nome com a primeira letra maiúscula.
3. **Construir a estrutura HTML5 Semântica no JSX:**
   * Uma tag `<article className="pokemon-card">`.
   * Um `<header>` com o número (`<span className="pokemon-id">`) e o nome (`<h2 className="pokemon-name">`).
   * Uma `<figure>` contendo a imagem do Pokémon (`<img src={image} alt={`Imagem do Pokémon ${name}`} />`).
   * Uma lista `<ul className="pokemon-types">` renderizando cada tipo dentro de um `<li className={`type-badge type-${tipo}`}>`.
4. **Configurar as Variáveis CSS (`PokemonCard.css`):**
   * No `:root`, declare as cores oficiais dos principais tipos:
     `--fire: #ff421d; --water: #268bf7; --grass: #57b952; --electric: #fbc02d; --poison: #a552cc;`.
   * Estilize o card com fundo claro, bordas arredondadas (`border-radius: 16px`), sombra leve e efeito de elevação no hover (`transform: translateY(-8px)`).
   * Estilize as pílulas de tipo (`type-badge`) aplicando a cor de fundo correspondente a cada classe de tipo (ex: `.type-fire { background-color: var(--fire); }`).
5. **Testar a renderização reutilizável no `App.jsx`:**
   * No `App.jsx`, crie dois objetos mockados de teste (`charmanderMock` e `squirtleMock`).
   * Renderize duas tags do componente passando as props: `<PokemonCard pokemon={charmanderMock} />` e `<PokemonCard pokemon={squirtleMock} />`.

---

### 🧪 5. Teste de Validação (5 Minutos)

1. Salve todos os arquivos e abra a página no navegador (`http://localhost:5173`).
2. Verifique se dois cards diferentes (Charmander e Squirtle) aparecem na tela reutilizando o mesmo componente `<PokemonCard />`.
3. Passe o mouse sobre os cards e confirme se ambos sobem suavemente com o efeito hover 3D.
4. Verifique se a pílula do Charmander está vermelha/fogo e a do Squirtle azul/água.

---

### ❓ 6. Quiz de Fixação PBL (6 Questões de Múltipla Escolha)

#### Q1. Qual tag do HTML5 Semântico é a mais recomendada para estruturar um card isolado e independente de informação (como um card de Pokémon)?
- (A) `<div>`
- (B) `<section>`
- (C) `<article>`
- (D) `<aside>`

> **Gabarito Comentado:** **(C)** O elemento `<article>` representa um bloco autônomo e reutilizável de conteúdo dentro de uma aplicação.

#### Q2. O que são Props no React e para que elas servem?
- (A) São comandos do banco de dados para salvar informações.
- (B) São argumentos/propriedades passados de um componente pai para um filho para tornar a interface dinâmica.
- (C) São arquivos CSS especiais que só rodam em servidores Node.js.
- (D) São funções que impedem o navegador de recarregar a página.

> **Gabarito Comentado:** **(B)** Props permitem enviar dados do componente Pai para o Filho, viabilizando a reutilização de componentes com informações diferentes.

#### Q3. Como declaramos e consumimos uma Variável CSS nativa (`Custom Property`) corretamente?
- (A) Declaração: `$cor: #ff0000;` | Uso: `color: $cor;`
- (B) Declaração: `--cor-principal: #ff0000;` | Uso: `color: var(--cor-principal);`
- (C) Declaração: `let cor = #ff0000;` | Uso: `color: get(cor);`
- (D) Declaração: `@cor-principal: #ff0000;` | Uso: `color: @cor-principal;`

> **Gabarito Comentado:** **(B)** Variáveis CSS nativas começam com dois hífens (`--nome`) e são consumidas pela função `var(--nome)`.

#### Q4. Qual recurso do JavaScript ES6 permite extrair propriedades de um objeto de forma simples e direta em variáveis locais?
- (A) Loop `for...in`
- (B) Desestruturação de Objetos (`Destructuring`)
- (C) Método `JSON.parse()`
- (D) Operador de igualdade estrita (`===`)

> **Gabarito Comentado:** **(B)** A desestruturação (ex: `const { id, name } = pokemon;`) extrai propriedades de objetos sem necessidade de repetição de código.

#### Q5. Qual instrução do JavaScript transforma o número `7` na string `'007'` com preenchimento de zeros à esquerda?
- (A) `String(7).padStart(3, '0')`
- (B) `Math.floor(7, 3)`
- (C) `Number(7).toFixed('000')`
- (D) `Array(7).push('00')`

> **Gabarito Comentado:** **(A)** O método `.padStart(tamanho, caractere)` preenche o início da string até atingir o comprimento desejado.

#### Q6. No React, o que acontece se tentarmos modificar diretamente o valor de uma Prop dentro do componente filho que a recebeu?
- (A) O valor é alterado com sucesso no componente pai também.
- (B) O React gera um erro de execução, pois Props são estritamente de apenas leitura (*read-only*).
- (C) O CSS da página é deletado automaticamente.
- (D) A propriedade vira uma variável global do sistema.

> **Gabarito Comentado:** **(B)** No React vigora o fluxo unidirecional de dados; props são imutáveis/read-only no componente que as recebe.

---

### 📝 7. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Reutilização de Componentes e Passagem de Props em React. Estruturação semântica com tag article, estilização dinâmica com Variáveis CSS (:root), desestruturação de objetos JS ES6 e criação do componente reusável PokemonCard."*
