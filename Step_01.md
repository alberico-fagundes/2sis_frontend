# 🚀 Step 01: PokéAgenda — Estrutura Semântica e Cabeçalho Reutilizável (<Header />)

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Duração:** 50 Minutos  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica (PBL / Conceitual):** Estude a fundação de HTML5 Semântico, CSS Flexbox, Módulos ES6 e Componentes Funcionais do React nesta documentação.
> * **🛠️ Trilha Prática (Projeto Integrador):** Aplique estes conceitos construindo o componente isolado `<Header />` dentro da sua aplicação React (`src/Header.jsx`).

---

### 🧩 1. O Problema Prático (Cenário PBL - Problem Statement)

**O Dilema do Cabeçalho Copiado e Colado em Múltiplas Páginas:**  
A equipe da **PokéAgenda** precisa criar o aplicativo da enciclopédia Pokémon. O designer entregou a marca oficial e o layout do topo. O estagiário tentou criar 5 páginas HTML diferentes (Início, Busca, Tipos, Favoritos e Sobre) e copiou o código do cabeçalho em todas elas. Quando a coordenação pediu para mudar a cor do cabeçalho e atualizar a imagem da logo, o estagiário teve que abrir e alterar arquivo por arquivo. Ele errou o caminho da imagem em dois deles, quebrando o layout do site.

No desenvolvimento web clássico com HTML puro, a repetição de código dificulta a manutenção e gera inconsistências visuais.

**A Pergunta-Chave PBL:**  
> *Como podemos utilizar o **HTML5 Semântico**, **CSS Flexbox** e os **Componentes Funcionais do React** para criar um cabeçalho `<Header />` modular, reutilizável e de fácil manutenção?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 HTML5 Semântico & Acessibilidade Web (`<header>`, `<figure>`, `alt`)
* **Tag `<header>`:** Representa o cabeçalho de uma página ou seção de conteúdo. Utilizar `<header>` em vez de uma `<div>` genérica informa aos leitores de tela e motores de busca (SEO) a real intenção daquele bloco visual.
* **Tag `<figure>` e `<img>`:** A tag `<figure>` encapsula mídias independentes. A tag `<img>` exige o uso do atributo `alt` (texto alternativo), fundamental para a acessibilidade de pessoas com deficiência visual e caso a imagem falhe ao carregar.
* **Hierarquia de Títulos (`<h1>` a `<h6>`):** Deve existir apenas um `<h1>` principal por página para indicar o tema central da aplicação.

#### 2.2 CSS3 Moderno: Flexbox & Layout Responsivo
* **Display Flex (`display: flex`):** Transforma o elemento pai em um contêiner flexível, organizando seus filhos em linha ou coluna.
* **Alinhamento e Distribuição:**
  * `justify-content: space-between;` — Empurra os elementos para as extremidades opostas do contêiner.
  * `align-items: center;` — Alinha verticalmente os elementos no centro do eixo secundário.
* **Estilização Visual:** Uso de `box-shadow` para profundidade, `padding` para espaçamento interno e `background: linear-gradient()` para criar fundos com gradiente de cores.

#### 2.3 JavaScript ES6+: Módulos, Arrow Functions e Imports/Exports
* **Exportação Nomeada (*Named Export*):** Permite exportar funções e variáveis do arquivo usando `export function Nome() {}`.
* **Importação (`import`):** Permite trazer componentes de outros arquivos usando `import { Nome } from './Nome'`.
* **Arrow Functions vs. Functions Padrão:** O React aceita funções declarativas tradicionais (`function Header() {}`) ou Arrow Functions (`const Header = () => {}`).

#### 2.4 React: Componentes Funcionais, JSX e `className`
* **Componentes Funcionais:** Funções JavaScript que retornam elementos visuais em sintaxe JSX.
* **Regra da Inicial Maiúscula:** No React, todo componente **deve obrigatoriamente** começar com letra maiúscula (ex: `Header`, não `header`). Nomes em minúsculo são interpretados como tags HTML nativas.
* **JSX vs. HTML:** Em JSX, usamos **`className`** em vez de `class` porque `class` é uma palavra reservada da linguagem JavaScript.

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Veja como estruturar um componente de cabeçalho modular usando a integração de HTML5, CSS3, JS ES6 e React:

#### Exemplo de Componente React (`src/Banner.jsx`):
```jsx
// Importação de módulos e estilos (JS ES6)
import './Banner.css';

// Componente Funcional com Exportação Nomeada
export function Banner() {
  return (
    // HTML5 Semântico com atributos JSX (className)
    <header className="banner-conteiner">
      <figure className="banner-logo">
        <img 
          src="https://via.placeholder.com/150" 
          alt="Logotipo da Aplicação" 
        />
      </figure>
      <p className="banner-subtitulo">Sua plataforma modular</p>
    </header>
  );
}
```

#### Exemplo de Estilo CSS (`src/Banner.css`):
```css
/* CSS Flexbox e Gradientes */
.banner-conteiner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background: linear-gradient(135deg, #ee1515, #b30000);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.banner-subtitulo {
  color: #ffffff;
  font-size: 1rem;
  font-weight: 600;
}
```

---

### 🛠️ 4. Desafio Ativo PBL (Mão na Massa - 30 Minutos)

Como desenvolvedor Frontend na equipe da PokéAgenda, sua missão é criar o componente `<Header />` oficial da aplicação:

1. **Criar o arquivo do componente:**
   * Dentro da pasta `src/`, crie o arquivo `Header.jsx`.
2. **Construir o componente funcional `<Header />`:**
   * Crie e exporte (usando *named export*) a função `Header`.
   * Retorne a estrutura HTML5 Semântica contendo:
     * Uma tag `<header>` com a classe `pokedex-header`.
     * Uma tag `<figure>` contendo uma tag `<img>` com o logo oficial da PokéAPI:
       `src="https://raw.githubusercontent.com/PokeAPI/media/master/logo/pokeapi_256.png"` e `alt="Logotipo Oficial PokéAPI"`.
     * Um elemento `<p>` com a classe `pokedex-subtitulo` contendo o texto: *"Sua Enciclopédia Pokémon Interativa"*.
3. **Estilizar o cabeçalho (`Header.css`):**
   * Crie o arquivo `Header.css` na pasta `src/` e importe-o no topo de `Header.jsx`.
   * Use **Flexbox** (`display: flex`, `justify-content: space-between`, `align-items: center`).
   * Aplique um fundo vermelho característico de Pokédex (`#dc2626` ou gradiente vermelho), texto em branco (`#ffffff`) e um espaçamento interno (`padding: 1rem 2rem`).
4. **Renderizar no `App.jsx`:**
   * Abra o arquivo `src/App.jsx`.
   * Importe o componente `<Header />`.
   * Insira a tag `<Header />` dentro do retorno principal do `App`.

---

### 🧪 5. Teste de Validação (5 Minutos)

1. No terminal do projeto, execute `npm run dev` e acesse o endereço fornecido (ex: `http://localhost:5173`).
2. Abra o navegador e verifique se o cabeçalho vermelho aparece no topo da tela com a logo da PokéAPI alinhada à esquerda/centro e o subtítulo visível.
3. Abra as Ferramentas do Desenvolvedor (`F12`), inspecione a imagem e confirme se o atributo `alt="Logotipo Oficial PokéAPI"` está presente no HTML gerado.

---

### ❓ 6. Quiz de Fixação PBL (6 Questões de Múltipla Escolha)

#### Q1. Qual tag de HTML5 Semântico é a mais adequada para encapsular o bloco superior de navegação e identidade de uma página web?
- (A) `<div>`
- (B) `<section>`
- (C) `<header>`
- (D) `<article>`

> **Gabarito Comentado:** **(C)** A tag `<header>` é a especificação semântica do HTML5 para representar cabeçalhos de páginas ou seções.

#### Q2. Por que no React usamos `className` em vez de `class` para definir classes CSS nos elementos JSX?
- (A) Porque `className` carrega os estilos mais rápido.
- (B) Porque a palavra `class` é uma palavra reservada da linguagem JavaScript para declaração de classes de objetos.
- (C) Porque `class` só funciona em arquivos HTML puros e o React proíbe CSS.
- (D) Não há diferença, ambos funcionam exatamente da mesma forma em JSX.

> **Gabarito Comentado:** **(B)** Como o JSX é uma extensão do JavaScript, palavras reservadas da linguagem como `class` e `for` são substituídas por `className` e `htmlFor`.

#### Q3. Qual propriedade do CSS Flexbox é responsável por distribuir os elementos filhos nas extremidades opostas do contêiner pai?
- (A) `align-items: center;`
- (B) `flex-direction: column;`
- (C) `justify-content: space-between;`
- (D) `display: grid;`

> **Gabarito Comentado:** **(C)** A propriedade `justify-content: space-between` alinha o primeiro elemento no início, o último no fim e distribui o espaço restante entre os intermediários.

#### Q4. No React, qual é a regra obrigatória em relação ao nome de um Componente Funcional?
- (A) O nome deve obrigatoriamente começar com letra maiúscula (PascalCase).
- (B) O nome deve estar em letras minúsculas e separado por hífen.
- (C) O nome precisa ter a palavra `Component` no final.
- (D) O nome do componente deve ter no máximo 5 caracteres.

> **Gabarito Comentado:** **(A)** Componentes React precisam começar com letra maiúscula (ex: `Header`) para que o JSX saiba diferenciá-los de tags HTML nativas em minúsculo (ex: `header`, `div`).

#### Q5. Qual das opções abaixo demonstra corretamente uma exportação nomeada (*Named Export*) de um componente React?
- (A) `export default Header;`
- (B) `export function Header() { return <header></header>; }`
- (C) `module.exports = Header;`
- (D) `import { Header } from './Header';`

> **Gabarito Comentado:** **(B)** A sintaxe `export function Nome() {}` é a forma padrão de exportação nomeada no ES6.

#### Q6. Qual é a função principal do atributo `alt` na tag `<img>` do HTML5?
- (A) Aumentar a resolução da imagem na tela.
- (B) Mudar a cor de fundo da página se a imagem for transparente.
- (C) Prover acessibilidade para leitores de tela e texto alternativo caso a imagem não possa ser carregada.
- (D) Definir a largura da imagem em pixels.

> **Gabarito Comentado:** **(C)** O atributo `alt` garante acessibilidade para usuários com deficiência visual e atua como texto de contingência caso ocorra falha de carregamento da imagem.

---

### 📝 7. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Introdução à Componentização em React e Estrutura Semântica. Construção de componentes funcionais, sintaxe JSX, uso do atributo className, módulos JS ES6 (export/import) e estilização de cabeçalhos com HTML5 Semântico e CSS Flexbox."*
