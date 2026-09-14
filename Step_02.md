# 🚀 Step 02: PokéAgenda — Estrutura Semântica do Card (<PokemonCard /> Estático) & CSS Moderno

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica (PBL / Conceitual):** Estude a anatomia semântica de um Card com HTML5 (`<article>`, `<figure>`, `<ul>`/`<li>`), estilização moderna com CSS (Bordas, Sombras e Efeito Hover).
> * **🛠️ Trilha Prática (Projeto Integrador):** Construa o componente visual estático `<PokemonCard />` em `src/PokemonCard.jsx` e crie sua folha de estilos em `src/PokemonCard.css`.

---

### 🧩 1. O Problema Prático (Cenário PBL - Problem Statement)

**O Dilema do Card Feito Apenas com Divs Genéricas:**  
A equipe de design da **PokéAgenda** entregou a maquete visual dos cards de Pokémon. O estagiário tentou desenhar o card usando mais de 10 tags `<div>` aninhadas (`<div><div><div>...</div></div></div>`), sem nenhuma semântica HTML. Quando a página foi testada em um leitor de tela para pessoas com deficiência visual, o navegador não entendeu onde começava ou terminava o card, e o código CSS ficou confuso e difícil de entender.

A ausência de tags semânticas prejudica a acessibilidade, o SEO e a legibilidade do código.

**A Pergunta-Chave PBL:**  
> *Como podemos utilizar o **HTML5 Semântico (`<article>`, `<figure>`, `<ul>`)** e o **CSS Moderno (Flexbox, Badges e Hover)** para construir a estrutura visual do nosso card de Pokémon de forma limpa, elegante e acessível?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 HTML5 Semântico: A Anatomia de um Card
* **Tag `<article>`:** Representa uma unidade de conteúdo independente e autocontida (como um post, um produto ou um card colecionável de Pokémon).
* **Tag `<header>` Interno:** Cabeçalho do próprio card, ideal para acomodar o número do Pokémon e seu nome.
* **Tag `<figure>` e `<img>`:** Acomoda a ilustração oficial com seu respectivo atributo `alt`.
* **Tag `<ul>` e `<li>`:** Representa a lista de categorias/tipos (ex: Fogo, Água, Planta), ideal para estruturar as "pílulas" (*badges*).

#### 2.2 CSS3 Moderno: Efeito Card, Sombras e Elevação Hover
* **Formato de Cartão:** Uso de `background-color: #ffffff`, `border-radius: 16px` (cantos arredondados) e `padding: 1.5rem` para dar respiro interno.
* **Profundidade com `box-shadow`:** Aplicação de sombras suaves (`box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08)`) para destacar o card do fundo da tela.
* **Animação ao Passar o Mouse (`:hover`):** Uso de `transition: transform 0.2s ease` combinado com `transform: translateY(-6px)` para criar a sensação de que o card "flutua" quando o usuário passa o cursor.

#### 2.3 Badges Visuais (Etiquetas de Tipo)
* **Pílulas com CSS:** Elementos `<span>` ou `<li>` com `display: inline-block`, `border-radius: 20px`, `padding: 0.25rem 0.75rem`, texto em caixa alta (`text-transform: uppercase`) e fonte em negrito.

> [!TIP]
> **Dica de Construção:** Antes de nos preocuparmos com dados dinâmicos de 150 Pokémons, os profissionais de frontend sempre constroem o **protótipo estático perfeito** de um único item. Uma vez aprovado o visual, nós o tornamos dinâmico!

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Veja como estruturar o layout estático de um cartão de usuário antes de conectá-lo a dados reais:

#### Exemplo de Componente React (`src/PerfilDev.jsx`):
```jsx
import './PerfilDev.css';

export function PerfilDev() {
  return (
    // Tag semântica article encapsulando o cartão
    <article className="perfil-card">
      <header className="perfil-cabecalho">
        <span className="perfil-id">#DEV01</span>
        <h2 className="perfil-nome">Alex Silva</h2>
      </header>

      <figure className="perfil-foto-conteiner">
        <img 
          src="https://via.placeholder.com/120" 
          alt="Foto de perfil de Alex Silva" 
        />
      </figure>

      <ul className="perfil-skills">
        <li className="skill-badge skill-react">React</li>
        <li className="skill-badge skill-css">CSS</li>
      </ul>
    </article>
  );
}
```

#### Exemplo de Estilo CSS (`src/PerfilDev.css`):
```css
.perfil-card {
  background-color: #ffffff;
  border-radius: 16px;
  padding: 1.5rem;
  width: 220px;
  text-align: center;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.perfil-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
}

.perfil-skills {
  list-style: none;
  padding: 0;
  display: flex;
  gap: 0.5rem;
  justify-content: center;
}

.skill-badge {
  font-size: 0.75rem;
  font-weight: bold;
  padding: 0.25rem 0.75rem;
  border-radius: 12px;
  background-color: #e2e8f0;
  color: #334155;
}
```

---

### 🛠️ 4. Desafio Ativo (Mão na Massa)

Como desenvolvedor Frontend na equipe da PokéAgenda, sua missão é criar a estrutura visual do protótipo estático do `<PokemonCard />`:

1. **Criar os arquivos:**
   * Crie o arquivo `src/PokemonCard.jsx`.
   * Crie o arquivo `src/PokemonCard.css`.
2. **Construir o componente em `src/PokemonCard.jsx`:**
   * Importe o `PokemonCard.css` no topo.
   * Crie e exporte a função `PokemonCard`.
   * Retorne a estrutura HTML5 Semântica com os dados iniciais do **Charmander**:
     * Um `<article className="pokemon-card">`.
     * Um `<header className="card-header">` com `<span className="pokemon-id">#004</span>` e `<h2 className="pokemon-name">Charmander</h2>`.
     * Uma `<figure className="pokemon-image-container">` contendo `<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/4.png" alt="Ilustração do Charmander" />`.
     * Uma lista `<ul className="pokemon-types">` contendo um `<li className="type-badge type-fire">Fogo</li>`.
3. **Estilizar o Card (`src/PokemonCard.css`):**
   * Defina para `.pokemon-card`: largura fixa (ex: `220px`), fundo branco (`#ffffff`), cantos arredondados (`border-radius: 16px`), sombra leve e efeito `:hover` com `transform: translateY(-6px)`.
   * Remova as bolinhas padrão da lista (`list-style: none; padding: 0;`).
   * Estilize `.type-badge` como uma pílula com bordas arredondadas e texto em negrito.
   * Adicione a classe `.type-fire` com `background-color: #ff421d; color: #ffffff;`.
4. **Renderizar no `App.jsx`:**
   * Importe `<PokemonCard />` em `src/App.jsx`.
   * Insira a tag `<PokemonCard />` dentro do retorno do componente `App`.

---

### 🧪 5. Teste de Validação

1. Abra o navegador (`http://localhost:5173`).
2. Verifique se o card do Charmander aparece com imagem nítida, número, nome e a etiqueta vermelha de "Fogo".
3. Passe o mouse sobre o card e confirme se ele realiza a animação suave de elevação (`hover`).
4. Abra o inspecionar elemento (`F12`) e confirme a presença das tags semânticas `<article>`, `<header>` e `<figure>`.

---

### ❓ 6. Quiz de Fixação (6 Questões de Múltipla Escolha)

#### Q1. Qual elemento semântico do HTML5 é o mais indicado para encapsular um card independente e reutilizável de conteúdo?
- (A) `<div>`
- (B) `<article>`
- (C) `<aside>`
- (D) `<span>`

> **Gabarito Comentado:** **(B)** A tag `<article>` é a especificação do HTML5 para blocos de conteúdo autocontidos e independentes.

#### Q2. Qual propriedade CSS é utilizada para arredondar os cantos de uma caixa/card?
- (A) `corner-style`
- (B) `border-radius`
- (C) `box-round`
- (D) `transform: round()`

> **Gabarito Comentado:** **(B)** `border-radius` define o raio de curvatura dos vértices de um elemento.

#### Q3. Para que serve a pseudo-classe `:hover` no CSS?
- (A) Para esconder o elemento quando a página é carregada.
- (B) Para disparar estilos visuais quando o cursor do mouse passa por cima do elemento.
- (C) Para mudar a cor do texto apenas ao imprimir a página.
- (D) Para deletar o elemento do DOM.

> **Gabarito Comentado:** **(B)** O seletor `:hover` é acionado quando o usuário posiciona o ponteiro do mouse sobre o elemento.

#### Q4. Qual tag HTML deve ser utilizada para agrupar uma lista não ordenada de itens (como tags ou tipos)?
- (A) `<ol>`
- (B) `<ul>`
- (C) `<table>`
- (D) `<select>`

> **Gabarito Comentado:** **(B)** A tag `<ul>` (*Unordered List*) agrupa itens marcados por tópicos (`<li>`).

#### Q5. Por que os desenvolvedores criam protótipos visuais estáticos antes de adicionar lógica dinâmica no React?
- (A) Porque o React não permite escrever lógica diretamente.
- (B) Para validar primeiro o design, a semântica e a responsividade da interface de forma isolada.
- (C) Porque navegadores não suportam HTML dinâmico.
- (D) Para aumentar o tamanho final do arquivo.

> **Gabarito Comentado:** **(B)** Construir o protótipo estático garante que a estrutura visual e os estilos estejam consolidados antes de integrar dados dinâmicos.

#### Q6. Como removemos os marcadores de ponto padrão de uma lista `<ul>` no CSS?
- (A) `list-style: none;`
- (B) `remove-dots: true;`
- (C) `text-decoration: none;`
- (D) `display: hidden;`

> **Gabarito Comentado:** **(A)** A regra `list-style: none` retira os marcadores padrão da lista.

---

### 📝 7. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Estruturação Semântica de Interfaces e Estilização de Cards. Uso das tags HTML5 article, figure e ul/li no React, estilização com CSS moderno (border-radius, box-shadow e pseudo-classe hover) e construção do protótipo do componente PokemonCard."*
