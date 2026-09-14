# 🎮 Trilha Pokédex: Do Zero ao React com PBL

> **Metodologia:** Aprendizagem Baseada em Projetos (PBL) com desafios atômicos no estilo *freeCodeCamp* (Passo a Passo com Instruções Claras, Exemplos Sintéticos, Testes/Checklist de Aceite e Desafios Bônus).

---

# 🔴 MÓDULO 1: O Card Colecionável (HTML & CSS Puro)
> **Problema da Missão:** O Prof. Carvalho precisa de uma carta física/digital para exibir os Pokémons catalogados na região de Kanto. Vamos construir o protótipo visual do **Pikachu**.

---

## ⚡ Desafio 1.1: O Esqueleto Semântico (HTML5)

### 📖 Contexto
Em HTML, usamos tags semânticas para dar significado aos elementos da página. Um card de monstrinho é uma unidade de conteúdo independente, ideal para uma tag `<article>`.

### 💡 Exemplo Didático
```html
<article>
  <img src="avatar.png" alt="Avatar" />
  <h2>Nome do Personagem</h2>
  <p>#001</p>
</article>
```

### 📋 Instruções da Missão
1. Crie um container usando a tag `<article class="pokemon-card">`.
2. Adicione uma tag de imagem `<img>` com `src` apontando para o sprite do Pikachu: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/25.png`.
3. Adicione um atributo `alt="Pikachu"` na imagem.
4. Adicione um título `<h2>Pikachu</h2>`.
5. Adicione um parágrafo contendo o ID `#025`.
6. Adicione uma tag `<span>` com o texto `Elétrico` para o tipo.

### ✅ Testes & Critérios de Aceite
- [ ] O documento possui uma tag `<article class="pokemon-card">`.
- [ ] A tag `<img>` possui os atributos `src` e `alt` preenchidos.
- [ ] O nome do Pokémon está dentro de uma tag `<h2>`.
- [ ] O número `#025` e o tipo `Elétrico` estão presentes no corpo do card.

### 🌟 Desafio Bônus
* Adicione o atributo `loading="lazy"` na imagem para otimizar carregamento futuro.

---

## 🎨 Desafio 1.2: O Box Model e Cores Temáticas (CSS)

### 📖 Contexto
Todo elemento HTML é uma "caixa" retangular composta por **Margem (margin)**, **Borda (border)**, **Espaçamento Interno (padding)** e **Conteúdo**. Vamos transformar o esqueleto bruto em uma carta estilizada.

### 💡 Exemplo Didático
```css
.card {
  width: 260px;
  background-color: #f0f0f0;
  border-radius: 12px;
  padding: 16px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
```

### 📋 Instruções da Missão
1. No seu arquivo `style.css`, estilize a classe `.pokemon-card`.
2. Defina uma largura máxima de `240px` com `max-width`.
3. Aplique uma cor de fundo amarelo-claro `#FFF275` ou `#F7D02C`.
4. Arredonde as 4 pontas do card com `border-radius: 16px`.
5. Adicione `padding: 20px` para o conteúdo não colar nas bordas.
6. Centralize os textos com `text-align: center`.
7. Estilize a tag `.type-badge` (o span do tipo) com fundo escuro, texto branco, `border-radius: 20px` e `padding: 4px 12px`.

### ✅ Testes & Critérios de Aceite
- [ ] O card não ultrapassa `240px` de largura.
- [ ] O card possui cantos arredondados e preenchimento interno (`padding`).
- [ ] O texto e a imagem estão alinhados ao centro.
- [ ] O badge de tipo tem formato de "pílula" com fundo contrastante.

### 🌟 Desafio Bônus
* Adicione uma sombra suave com `box-shadow: 0 8px 16px rgba(0,0,0,0.15);`.

---

## 📐 Desafio 1.3: Organizando com Flexbox (Alinhamento & Distribuição)

### 📖 Contexto
Pokémons podem ter mais de um tipo (ex: Charizard é Fogo e Voador) e estatísticas. `display: flex` é a melhor ferramenta para alinhar itens em linha ou coluna de forma flexível.

### 💡 Exemplo Didático
```css
.badge-list {
  display: flex;
  justify-content: center; /* Alinha na horizontal */
  align-items: center;     /* Alinha na vertical */
  gap: 8px;                /* Espaço entre os itens */
}
```

### 📋 Instruções da Missão
1. Crie uma `<div>` envolvendo os tipos do Pokémon com a classe `types-container`.
2. Adicione mais um tipo no HTML para teste (ex: `<span>Voador</span>`).
3. No CSS, aplique `display: flex` na classe `types-container`.
4. Centralize os badges na horizontal com `justify-content: center`.
5. Crie um espaçamento entre os badges usando `gap: 8px`.
6. Crie um cabeçalho `.card-header` contendo o Nome e o Número do Pokémon e aplique `justify-content: space-between` para empurrar o nome para a esquerda e o número para a direita.

### ✅ Testes & Critérios de Aceite
- [ ] A classe `types-container` utiliza `display: flex`.
- [ ] Os badges de tipo ficam lado a lado horizontalmente com espaçamento via `gap`.
- [ ] O cabeçalho possui o nome alinhado à esquerda e o número à direita via `justify-content: space-between`.

### 🌟 Desafio Bônus
* Adicione um efeito de elevação `:hover` no card: `transform: translateY(-6px); transition: transform 0.2s ease;`.

---

# 🟡 MÓDULO 2: O Card Interativo (JavaScript e DOM)
> **Problema da Missão:** O protótipo visual precisa responder a interações do usuário. Vamos permitir alternar entre a forma padrão e a forma Shiny (brilhante), além de filtrar um catálogo local.

---

## 🖱️ Desafio 2.1: Capturando Elementos e Eventos de Clique

### 📖 Contexto
Para alterar a tela via JS, precisamos de 3 passos:
1. **Selecionar** o elemento na tela (`document.querySelector`).
2. **Ouvir** a ação do usuário (`addEventListener`).
3. **Modificar** o atributo ou texto (`element.src` ou `element.textContent`).

### 💡 Exemplo Didático
```javascript
const btn = document.querySelector('#meu-botao');
const foto = document.querySelector('#minha-foto');

btn.addEventListener('click', () => {
  foto.src = 'nova-imagem.png';
});
```

### 📋 Instruções da Missão
1. Adicione um `<button id="btn-shiny">Ver Shiny</button>` abaixo do card no HTML.
2. Adicione um `id="pokemon-img"` na imagem do Pikachu.
3. No seu `script.js`, selecione o botão e a imagem.
4. Ao clicar no botão, se a imagem atual for a normal, troque para o sprite shiny: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/shiny/25.png`.
5. Alterne o texto do botão para "Ver Normal" quando o shiny estiver ativo.

### ✅ Testes & Critérios de Aceite
- [ ] O botão possui um ouvinte de evento de clique (`click`).
- [ ] Clicar no botão altera o `src` da imagem para a versão shiny.
- [ ] Clicar novamente restaura a imagem normal.
- [ ] O texto do botão reflete a ação disponível ("Ver Shiny" <-> "Ver Normal").

### 🌟 Desafio Bônus
* Adicione uma classe CSS `.shiny-glow` no card para acender uma borda dourada quando shiny estiver ativo.

---

## 📜 Desafio 2.2: Catálogo Dinâmico e Filtro de Busca (Arrays e Loops)

### 📖 Contexto
Em vez de escrever 10 cards na mão no HTML, guardamos os dados em uma lista de objetos (Array) e geramos o HTML dinamicamente com Template Literals (crases `` ` ``).

### 💡 Exemplo Didático
```javascript
const frutas = ['Maçã', 'Banana', 'Uva'];
const container = document.querySelector('#lista');

frutas.forEach(fruta => {
  container.innerHTML += `<p>${fruta}</p>`;
});
```

### 📋 Instruções da Missão
1. Crie um array no JS com 4 pokémons:
   ```javascript
   const pokedex = [
     { id: 1, name: 'Bulbasaur', type: 'Grass', img: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/1.png' },
     { id: 4, name: 'Charmander', type: 'Fire', img: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/4.png' },
     { id: 7, name: 'Squirtle', type: 'Water', img: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/7.png' },
     { id: 25, name: 'Pikachu', type: 'Electric', img: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/25.png' }
   ];
   ```
2. Crie uma função `renderCards(lista)` que limpa uma `<div id="pokedex-grid">` e insere os cards usando `.forEach()` ou `.map()`.
3. Adicione um campo de texto `<input id="search-input" placeholder="Buscar Pokémon..." />`.
4. Ouça o evento `input` do campo de texto e filtre a lista usando `.filter()`, re-renderizando a tela em tempo real.

### ✅ Testes & Critérios de Aceite
- [ ] A página inicial renderiza os 4 pokémons do array sem HTML duplicado fixo.
- [ ] Digitar "char" no input filtra a lista e exibe apenas o Charmander.
- [ ] Apagar o texto da busca faz todos os 4 Pokémons reaparecerem.

### 🌟 Desafio Bônus
* Aplique CSS Grid no container `.pokedex-grid`: `display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 16px;`.

---

# 🟢 MÓDULO 3: Conexão com o Mundo Real (JS Assíncrono & PokéAPI)
> **Problema da Missão:** O Prof. Carvalho descobriu que existem mais de 1000 Pokémons. Não dá para cadastrar tudo num array estático. Vamos consumir dados em tempo real da internet via **PokéAPI**.

---

## 🌐 Desafio 3.1: A Primeira Requisição (Fetch e Async/Await)

### 📖 Contexto
Dados de servidores levam tempo para viajar pela rede. Usamos funções assíncronas (`async/await`) e `fetch()` para esperar a resposta sem travar o navegador.

### 💡 Exemplo Didático
```javascript
async function buscarDado() {
  const resposta = await fetch('https://api.exemplo.com/item');
  const dados = await resposta.json();
  console.log(dados);
}
```

### 📋 Instruções da Missão
1. Crie uma função assíncrona chamada `getPokemonData(nomeOuId)`.
2. Faça uma requisição para a URL: `https://pokeapi.co/api/v2/pokemon/${nomeOuId}`.
3. Converta a resposta para JSON usando `await response.json()`.
4. Exiba no console os seguintes campos retornados:
   * `dados.name` (Nome)
   * `dados.id` (Número)
   * `dados.sprites.front_default` (URL da foto)
   * `dados.types[0].type.name` (Tipo primário)

### ✅ Testes & Critérios de Aceite
- [ ] A função `getPokemonData` é declarada com a palavra-chave `async`.
- [ ] O comando `fetch()` é chamado com a URL da PokéAPI correta.
- [ ] O JSON é extraído corretamente com `await .json()`.
- [ ] Ao executar `getPokemonData('ditto')`, os dados do Ditto aparecem no console.

### 🌟 Desafio Bônus
* Envolva a busca em um bloco `try / catch` para capturar caso o usuário digite um Pokémon inexistente (ex: erro 404).

---

## 🔍 Desafio 3.2: O Buscador PokéAPI em Tempo Real

### 📖 Contexto
Agora vamos conectar o `input` de busca diretamente com a PokéAPI. Quando o usuário enviar o formulário, buscaremos o Pokémon na internet e atualizaremos a tela.

### 💡 Exemplo Didático
```javascript
form.addEventListener('submit', async (e) => {
  e.preventDefault(); // Evita recarregar a página!
  const valor = input.value;
  // Chama a API e atualiza a tela
});
```

### 📋 Instruções da Missão
1. Crie um formulário `<form id="search-form">` com input e botão "Pesquisar".
2. Intercepte o envio com `form.addEventListener('submit', ...)`.
3. Não esqueça de invocar `event.preventDefault()`.
4. Pegue o valor digitado, converta para minúsculas com `.toLowerCase().trim()`.
5. Chame `getPokemonData()` e injete os dados recebidos dentro do card na tela.
6. Enquanto espera o retorno, exiba uma mensagem "Buscando na Pokédex..." na tela.

### ✅ Testes & Critérios de Aceite
- [ ] A página não recarrega ao enviar o formulário.
- [ ] Digitar "mewtwo" ou "150" e clicar em buscar atualiza o card com os dados do Mewtwo.
- [ ] Letras maiúsculas digitadas pelo usuário não quebram a busca na API.
- [ ] Pokémons inexistentes exibem mensagem de alerta na interface: "Pokémon não encontrado!".

### 🌟 Desafio Bônus
* Toque o grito de áudio do Pokémon usando `new Audio(dados.cries.latest).play()`.

---

## 🧗 Desafio 3.3: A Dor do Gerenciamento Manual de Estado (Transição)

### 📖 Contexto
O Prof. Carvalho quer uma lista com paginação (botões "Próximos 20" e "20 Anteriores"). 

### 💡 O Problema Sentido na Prática
* Ao carregar 20 pokémons via API, você precisa fazer 20 fetches secundários, controlar `offset = 0`, limpar a DOM com `innerHTML = ''`, recriar os elementos, reatachar eventos nos botões de shiny de cada card...
* O código começa a ficar gigante, frágil e desorganizado ("código espaguete").

### 📋 Instruções da Missão
1. Implemente uma variável global `let offset = 0;`.
2. Ao clicar no botão "Próximos 20", incremente `offset += 20` e recarregue a lista.
3. Observe como sincronizar as variáveis, os botões e a DOM dá trabalho manual.
4. **Reflexão:** *"E se existisse uma biblioteca onde a gente só cuida dos dados (estado) e a interface se atualiza sozinha?"* -> **Bem-vindo ao React!**

---

# 🔵 MÓDULO 4: A Era Moderna (Componentização com React)
> **Problema da Missão:** Reescrever a Pokédex usando React, tornando o código modular, legível, manutenível e reativo.

---

## ⚛️ Desafio 4.1: O Primeiro Componente (Transformando HTML em JSX)

### 📖 Contexto
Em React, quebramos a interface em blocos chamados **Componentes**. O JSX permite escrever sintaxe parecida com HTML dentro do JavaScript, com pequenas diferenças:
* `class` vira `className`.
* Tags auto-fechadas precisam de barra final: `<img />`, `<input />`.

### 💡 Exemplo Didático
```jsx
// src/components/PokemonCard.jsx
export function PokemonCard() {
  return (
    <article className="pokemon-card">
      <img 
        src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/25.png" 
        alt="Pikachu" 
      />
      <h2>Pikachu</h2>
      <span className="badge">Elétrico</span>
    </article>
  );
}
```

### 📋 Instruções da Missão
1. Crie o arquivo `src/components/PokemonCard.jsx`.
2. Crie e exporte a função `PokemonCard`.
3. Cole a estrutura do card feita no Módulo 1 adaptando para JSX (`className` e `<img />`).
4. No arquivo `src/App.jsx`, importe o `PokemonCard` e renderize 3 cards na tela para ver a reutilização.

### ✅ Testes & Critérios de Aceite
- [ ] O componente `PokemonCard` está em seu próprio arquivo na pasta `components/`.
- [ ] Todo atributo `class` foi substituído por `className`.
- [ ] O componente é importado e renderizado com sucesso dentro de `App.jsx`.

### 🌟 Desafio Bônus
* Isole o CSS do card criando `PokemonCard.module.css` e importando como `import styles from './PokemonCard.module.css'`.

---

## 🧩 Desafio 4.2: Componentes Dinâmicos com Props e Listas (`.map`)

### 📖 Contexto
**Props** são como argumentos de uma função: permitem passar dados diferentes para o mesmo componente. Para renderizar listas, usamos o método `.map()` do JS com uma `key` única.

### 💡 Exemplo Didático
```jsx
export function PokemonCard({ name, id, image, type }) {
  return (
    <article className="pokemon-card">
      <img src={image} alt={name} />
      <h2>{name}</h2>
      <p>#{id}</p>
      <span className="badge">{type}</span>
    </article>
  );
}
```

### 📋 Instruções da Missão
1. Atualize o `PokemonCard` para receber as propriedades: `{ name, id, image, type }` via desestruturação.
2. Substitua os valores fixos do JSX pelas variáveis entre chaves `{name}`, `{id}`, `{image}`, `{type}`.
3. Em `App.jsx`, crie uma lista de Pokémons e renderize com `.map()`:
   ```jsx
   const pokemonList = [
     { id: 1, name: 'Bulbasaur', type: 'Planta', image: '...' },
     { id: 4, name: 'Charmander', type: 'Fogo', image: '...' },
     { id: 7, name: 'Squirtle', type: 'Água', image: '...' },
   ];
   ```
4. Adicione obrigatoriamente a propriedade `key={pokemon.id}` na tag `<PokemonCard />`.

### ✅ Testes & Critérios de Aceite
- [ ] O componente `PokemonCard` não possui mais textos fixos; usa props.
- [ ] A renderização da lista utiliza o método `.map()`.
- [ ] Cada elemento retornado na lista possui uma `key` única.

### 🌟 Desafio Bônus
* Se o Pokémon tiver mais de um tipo (array `types: ['Fogo', 'Voador']`), renderize os badges com um `.map()` secundário dentro do card.

---

## ⚡ Desafio 4.3: Estado Reativo com `useState`

### 📖 Contexto
No React, não alteramos a tela mexendo na DOM (`document.querySelector`). Nós alteramos o **Estado (`useState`)**, e o React redesenha a tela automaticamente onde for necessário!

### 💡 Exemplo Didático
```jsx
import { useState } from 'react';

export function Contador() {
  const [contador, setContador] = useState(0);

  return (
    <button onClick={() => setContador(contador + 1)}>
      Cliques: {contador}
    </button>
  );
}
```

### 📋 Instruções da Missão
1. No componente `PokemonCard`, importe `useState`.
2. Crie um estado para controlar se a carta é shiny: `const [isShiny, setIsShiny] = useState(false);`.
3. Adicione um botão "Alternar Shiny" com evento `onClick={() => setIsShiny(!isShiny)}`.
4. No `src` da imagem, use um operador ternário: `src={isShiny ? shinyImg : normalImg}`.
5. Crie um segundo estado `const [isFavorite, setIsFavorite] = useState(false);` e um botão de coração `❤️ / 🤍`.

### ✅ Testes & Critérios de Aceite
- [ ] O hook `useState` é utilizado para controlar os estados do componente.
- [ ] Clicar no botão altera o estado `isShiny` e a imagem muda instantaneamente sem recarregar a página.
- [ ] O botão de favorito altera entre coração preenchido e vazio reativamente.

### 🌟 Desafio Bônus
* Adicione um `<input>` de busca no `App.jsx` ligado a um estado `searchTerm` que filtra a lista de pokémons na tela em tempo real.

---

## 🌐 Desafio 4.4: Conectando a PokéAPI no React (`useEffect`)

### 📖 Contexto
Para executar efeitos colaterais (como buscar dados em uma API externa) assim que o componente nasce na tela, usamos o hook **`useEffect`**.

### 💡 Exemplo Didático
```jsx
import { useState, useEffect } from 'react';

export function App() {
  const [dados, setDados] = useState([]);

  useEffect(() => {
    fetch('https://api.exemplo.com/itens')
      .then(res => res.json())
      .then(info => setDados(info));
  }, []); // [] significa: execute apenas 1 vez ao abrir a tela
}
```

### 📋 Instruções da Missão
1. No `App.jsx`, crie dois estados:
   * `const [pokemons, setPokemons] = useState([]);`
   * `const [loading, setLoading] = useState(true);`
2. Crie um `useEffect` com array de dependências vazio `[]`.
3. Dentro do efeito, busque os 20 primeiros pokémons na PokéAPI (`https://pokeapi.co/api/v2/pokemon?limit=20`).
4. Para cada item da lista, busque os detalhes (foto, tipo, id) e salve o resultado no estado `setPokemons`.
5. Ao terminar a busca, defina `setLoading(false)`.
6. Na renderização, se `loading` for verdadeiro, exiba `<h1>Carregando Pokédex...</h1>`. Caso contrário, renderize os cards.

### ✅ Testes & Critérios de Aceite
- [ ] O hook `useEffect` é utilizado com array de dependências vazio `[]`.
- [ ] Há um indicador visual de carregamento (`loading`) enquanto a API responde.
- [ ] A grade de cards é preenchida automaticamente com dados reais da PokéAPI assim que o site abre.

### 🌟 Desafio Bônus
* Adicione um botão "Carregar Mais" no rodapé que incrementa o limite e anexa mais 20 Pokémons à lista existente.

---

# 🏆 Projeto Final: Pokédex Capstone (Entrega Final)

### 🎯 Problema do Projeto
Você deve entregar o sistema completo da Pokédex para o Laboratório de Pesquisas de Kanto.

### 📋 Checklist de Funcionalidades Obrigatórias:
- [ ] **Interface Moderna:** Grid responsivo com Flexbox/CSS Grid que se adapta a celulares e computadores.
- [ ] **Consumo de API:** Lista alimentada dinamicamente via PokéAPI utilizando `useEffect`.
- [ ] **Busca em Tempo Real:** Campo de pesquisa controlado (`useState`) filtrando por nome ou número.
- [ ] **Filtros por Categoria:** Botões com os tipos de Pokémon (Fogo, Água, Planta, Elétrico) para filtrar a lista.
- [ ] **Favoritos com Persistência:** Salvar os IDs dos Pokémons favoritados no `localStorage` para não perder ao recarregar a página.
- [ ] **Deploy Público:** Projeto publicado e acessível publicamente via Vercel ou Netlify.
