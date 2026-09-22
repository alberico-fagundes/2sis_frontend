# 🚀 Step 06: PokéAgenda — Interatividade e Estado Reativo com `useState`

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica ( / Conceitual):** Domine o conceito central do React — o **Estado (`useState`)**, escuta de eventos de clique com `onClick`, e alternância de dados com **Operadores Ternários** no JSX.
> * **🛠️ Trilha Prática (Projeto Integrador):** Adicione interatividade ao componente `<PokemonCard />`, permitindo ao usuário alternar entre a versão Normal/Shiny do Pokémon e marcar Pokémons como Favoritos (❤️).

---

### 🧩 1. O Problema Prático (Cenário  - Problem Statement)

**O Dilema do `querySelector` que Travou o React:**  
A equipe de produto pediu uma funcionalidade interativa: quando o usuário clicar em um botão no card do Pokémon, a foto deve alternar para a versão **Shiny** (brilhante/rara). O estagiário da **PokéAgenda** tentou resolver isso usando o JavaScript antigo: criou um `document.querySelector('#foto-pikachu').src = 'shiny.png'`. Porém, quando o React atualizou a tela, a alteração manual do estagiário desapareceu e a imagem antiga voltou.

No React, nunca alteramos a tela mexendo na DOM manualmente (`querySelector`). O React possui seu próprio mecanismo de memória chamado **Estado**.

**A Pergunta-Chave :**  
> *Como podemos utilizar o Hook **`useState` do React** e o evento **`onClick`** para que a tela reaja instantaneamente às ações do usuário e lembre se o card está na versão Shiny ou Favoritado?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 O que é o Hook `useState`?
* **O Conceito de Estado:** O estado é a "memória interna" de um componente. Quando o valor do estado muda, o React redesenha automaticamente a parte da tela que depende daquela informação.
* **Sintaxe do `useState`:**
  ```js
  import { useState } from 'react';

  // [ valorAtual, funcaoParaAtualizar ] = useState( valorInicial );
  const [isShiny, setIsShiny] = useState(false);
  ```
  1. `isShiny`: Variável que guarda o valor atual (ex: `false`).
  2. `setIsShiny`: Função especial usada para mudar o valor da variável.
  3. `useState(false)`: Define que a memória começa como `false`.

#### 2.2 Escutando Eventos com `onClick` no JSX
* No React, capturamos cliques de botão passando uma função para o atributo `onClick`:
  ```jsx
  <button onClick={() => setIsShiny(!isShiny)}>
    Alternar Shiny
  </button>
  ```
* O operador `!` (Negação) inverte o valor booleano: se era `false`, vira `true`; se era `true`, vira `false`.

#### 2.3 Operador Ternário no JSX (`condicao ? valorSeVerdadeiro : valorSeFalso`)
* Usado para alternar conteúdos ou imagens no JSX de forma simples:
  ```jsx
  // Exemplo de alternância de imagem
  <img src={isShiny ? pokemon.shinyImage : pokemon.image} alt={pokemon.name} />

  // Exemplo de alternância de texto
  <button>{isShiny ? "Ver Normal" : "Ver Shiny"}</button>
  ```

> [!TIP]
> **Regra de Ouro do Estado:** Nunca faça `isShiny = true` diretamente! Sempre use a função atualizadora `setIsShiny(true)`. Só ela avisa o React que é hora de redesenhar a tela!

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Veja como um componente de Botão de Curtida gerencia seu estado com `useState`:

#### Exemplo de Componente React (`src/BotaoCurtir.jsx`):
```jsx
import { useState } from 'react';
import './BotaoCurtir.css';

export function BotaoCurtir() {
  // Estado para controlar se o post foi curtido
  const [curtido, setCurtido] = useState(false);

  return (
    <button 
      className={`btn-curtir ${curtido ? 'ativo' : ''}`}
      onClick={() => setCurtido(!curtido)}
    >
      {curtido ? '❤️ Curtido' : '🤍 Curtir'}
    </button>
  );
}
```

---

### 🛠️ 4. Desafio Ativo (Mão na Massa)

Sua missão na PokéAgenda é tornar os cards interativos adicionando o modo Shiny e o botão de Favorito:

1. **Atualizar o arquivo `src/pokemons.js`:**
   * Adicione a propriedade `shinyImage` em cada Pokémon no seu array de dados:
     ```js
     {
       id: 25,
       name: "Pikachu",
       type: "Eletrico",
       image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png",
       shinyImage: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/shiny/25.png"
     }
     ```

2. **Adicionar os Estados no `<PokemonCard.jsx>`:**
   * Abra `src/PokemonCard.jsx` e importe o `useState`:
     ```jsx
     import { useState } from 'react';
     import './PokemonCard.css';
     ```
   * Crie dois estados dentro da função do componente:
     ```jsx
     const [isShiny, setIsShiny] = useState(false);
     const [isFavorite, setIsFavorite] = useState(false);
     ```

3. **Atualizar a imagem e botões de ação:**
   * No `src` da tag `<img>`, use a imagem shiny se `isShiny` for verdadeiro:
     ```jsx
     <img 
       src={isShiny && pokemon.shinyImage ? pokemon.shinyImage : pokemon.image} 
       alt={pokemon.name} 
     />
     ```
   * Adicione um rodapé de ações no card com dois botões:
     ```jsx
     <footer className="card-acoes">
       <button 
         className="btn-shiny" 
         onClick={() => setIsShiny(!isShiny)}
       >
         {isShiny ? '✨ Ver Normal' : '⭐ Ver Shiny'}
       </button>

       <button 
         className={`btn-favorito ${isFavorite ? 'favoritado' : ''}`}
         onClick={() => setIsFavorite(!isFavorite)}
       >
         {isFavorite ? '❤️' : '🤍'}
       </button>
     </footer>
     ```

4. **Estilizar a interatividade (`src/PokemonCard.css`):**
   * Adicione uma borda dourada quando o card for marcado como favorito ou shiny.

---

### 🧪 5. Teste de Validação

1. Abra o navegador (`http://localhost:5173`).
2. Clique no botão **"⭐ Ver Shiny"** de um dos Pokémons (ex: Pikachu). Verifique se a imagem muda instantaneamente para a versão dourada/brilhante sem recarregar a página!
3. Clique no botão de coração **🤍**. Confirme que ele altera para **❤️** e que apenas aquele card específico foi afetado, sem interferir nos outros cards ao lado.
4. Clique novamente e confirme que os botões voltam ao estado original (normal e desfavoritado).

---

### ❓ 6. Quiz de Fixação (6 Questões de Múltipla Escolha)

#### Q1. O que é o Hook `useState` no React?
- (A) Uma função para conectar o site ao banco de dados MySQL.
- (B) Um recurso que permite aos componentes criar e gerenciar sua própria memória interna e redesenhar a tela quando ela muda.
- (C) Um comando do CSS para arredondar cantos de imagens.
- (D) Um plugin do VS Code.

#### Q2. Dada a declaração `const [isShiny, setIsShiny] = useState(false);`, qual é o papel de `setIsShiny`?
- (A) É a variável que guarda o nome do Pokémon.
- (B) É a função responsável por atualizar o valor de `isShiny` e avisar o React para redesenhar o componente.
- (C) É o estilo CSS do botão.
- (D) É uma tag HTML.


#### Q3. Por que não devemos usar `document.querySelector` para alterar textos ou imagens no React?
- (A) Porque o JavaScript antigo foi proibido na internet.
- (B) Porque o React gerencia sua própria DOM Virtual e sobrescreverá qualquer mudança manual feita fora do fluxo de Estado.
- (C) Porque isso consome toda a memória RAM do computador.
- (D) Porque o `querySelector` só funciona no Internet Explorer.



#### Q4. Qual expressão em JSX utiliza o Operador Ternário para alternar entre as opções "Sim" e "Não" baseado na variável `ativo`?
- (A) `{if ativo then "Sim" else "Não"}`
- (B) `{ativo ? "Sim" : "Não"}`
- (C) `{ativo == "Sim" && "Não"}`
- (D) `{switch(ativo) "Sim" : "Não"}`


#### Q5. Como invertemos o valor de um estado booleano (ex: de `false` para `true`) dentro da função `onClick`?
- (A) `onClick={() => setIsShiny(!isShiny)}`
- (B) `onClick={isShiny = true}`
- (C) `onClick={delete isShiny}`
- (D) `onClick={() => isShiny + 1}`



#### Q6. Em uma lista com 6 cards de Pokémons, o que acontece se o usuário clicar no botão de favoritar de um único card?
- (A) Todos os 6 cards ficam favoritados ao mesmo tempo.
- (B) Apenas o card clicado altera seu estado interno, pois cada componente filho possui sua própria instância isolada de `useState`.
- (C) O navegador fecha.
- (D) A página recarrega automaticamente.


---

