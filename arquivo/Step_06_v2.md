# 🚀 Step 06: PokéAgenda — Interatividade e Estado Reativo com `useState`

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica ( / Conceitual):** Domine o conceito central do React — o **Estado (`useState`)**: a memória interna de um componente. Aprenda a escutar cliques com `onClick`, alternar valores com o operador `!` (negação) e trocar imagem/texto/classe com o **Operador Ternário** no JSX.
> * **🛠️ Trilha Prática (Projeto Integrador):** Dê memória ao `<PokemonCard />`: um único estado (`isShiny`) e um botão **"⭐ Ver Shiny"** que alterna a imagem do Pokémon sem recarregar a página. (No final, um desafio extra planta a semente dos Favoritos do Step 10.)

---

### 🧩 1. O Problema Prático (Cenário  - Problem Statement)

**O Dilema do `querySelector` que Travou o React:**  
A equipe de produto pediu uma funcionalidade interativa: quando o usuário clicar em um botão no card, a foto deve alternar para a versão **Shiny** (brilhante/rara). O estagiário da **PokéAgenda** tentou resolver com o JavaScript antigo que já conhecia:

```js
document.querySelector('#foto-pikachu').src = 'shiny.png';
```

Funcionou por um segundo — e então o React redesenhou a tela e a imagem **voltou sozinha para a versão normal**. O clique parecia não fazer nada.

No React, **nós nunca mexemos na tela manualmente**. A tela é reflexo da memória do componente: mudou a memória (o **Estado**), o React redesenha a interface sozinho.

**A Pergunta-Chave :**  
> *Como podemos utilizar o Hook **`useState` do React** e o evento **`onClick`** para que a tela reaja instantaneamente ao clique do usuário e "lembre" se o card está na versão Shiny?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 O Hook `useState` — A Memória do Componente
* **O que é Estado:** é a "memória interna" de um componente. Quando o valor dessa memória muda, o React redesenha automaticamente a parte da tela que depende dela.
* **Dissecando a sintaxe, peça por peça:**
  ```text
  const [ isShiny , setIsShiny ] = useState( false );
        ────────   ───────────            ─────
          (1)          (2)                  (3)
  ```
  1. **`isShiny` (o valor):** variável que guarda o valor atual da memória (começa `false`).
  2. **`setIsShiny` (a função):** a ÚNICA forma de mudar a memória. Ela atualiza o valor **e avisa o React** que é hora de redesenhar.
  3. **`useState(false)` (o valor inicial):** define como a memória nasce, na primeira renderização.
* **Por isso é "destructuring":** `useState` devolve um par `[valor, função]`, e os colchetes `[]` desembalam as duas peças em variáveis com nomes que nós escolhemos.

  ```jsx
  import { useState } from 'react';

  export function MeuComponente() {
    const [isShiny, setIsShiny] = useState(false);
  }
  ```

#### 2.2 Escutando Cliques com `onClick`
* No React, passamos uma **função** para o atributo `onClick` (com `c` maiúsculo!):
  ```jsx
  <button onClick={() => setIsShiny(!isShiny)}>Alternar Shiny</button>
  ```
* **O operador `!` (negação)** inverte o booleano: se era `false`, vira `true`; se era `true`, vira `false`. O botão funciona como um **interruptor de luz**.

#### 2.3 Operador Ternário no JSX — A Escolha Visual
* O `if/else` não cabe dentro de `{}` (não devolve valor), então usamos o **ternário** `condicao ? seVerdadeiro : seFalso`:
  ```jsx
  // A imagem depende da memória:
  <img src={isShiny ? pokemon.shinyImage : pokemon.image} alt={pokemon.name} />

  // O texto do botão também:
  <button>{isShiny ? 'Ver Normal' : 'Ver Shiny'}</button>
  ```

#### 2.4 Classe Dinâmica — o Estilo Reage ao Estado
* O mesmo ternário pode ligar e desligar classes CSS:
  ```jsx
  <article className={`pokemon-card ${isShiny ? 'shiny' : ''}`}>
  ```
  * Quando `isShiny` é `true`, a classe extra `shiny` entra e o CSS `.pokemon-card.shiny` vale. Quando é `false`, entra **corda vazia** `''` e o card volta ao normal.

> [!TIP]
> **Regra de Ouro do Estado:** NUNCA faça `isShiny = true` diretamente! Só a função atualizadora (`setIsShiny(true)`) avisa o React para redesenhar. Mudar a variável "por fora" é escrever numa memória fantasma.

> [!IMPORTANT]
> **Cada card, uma memória:** o Estado vive DENTRO de cada instância de componente. Se renderizamos 4 `<PokemonCard />`, existem 4 memória `isShiny` independentes — clicar em uma não afeta as vizinhas.

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Veja um card de produto com botão "Ativar Promoção" que **troca a imagem, o preço e a cor da borda** usando um único estado. Tudo (componente + CSS + uso no App) antes de você codar o Shiny:

#### 1. O Componente Interativo (`src/CardPromocao.jsx`):
```jsx
import { useState } from 'react';
import './CardPromocao.css';

export function CardPromocao() {
  const produto = {
    nome: 'Tênis Runner',
    imagemNormal: 'https://via.placeholder.com/150?text=Tenis+Normal',
    imagemPromo: 'https://via.placeholder.com/150?text=Tenis+Promocao',
    precoNormal: 299.9,
    precoPromo: 199.9
  };

  // 1. A memória: "este produto está em promoção?" (nasce false)
  const [emPromocao, setEmPromocao] = useState(false);

  return (
    // 4. Classe dinâmica: borda dourada só quando emPromocao = true
    <article className={`card-produto ${emPromocao ? 'promocao' : ''}`}>
      <figure>
        {/* 3. A imagem reage ao estado via ternário */}
        <img 
          src={emPromocao ? produto.imagemPromo : produto.imagemNormal} 
          alt={produto.nome} 
        />
      </figure>
      <h3>{produto.nome}</h3>
      <p className="preco">
        {emPromocao
          ? `R$ ${produto.precoPromo.toFixed(2)} 🏷️`
          : `R$ ${produto.precoNormal.toFixed(2)}`}
      </p>

      {/* 2. O interruptor: onClick inverte o booleano com ! */}
      <button className="btn-toggle" onClick={() => setEmPromocao(!emPromocao)}>
        {emPromocao ? 'Remover Promoção' : 'Ativar Promoção'}
      </button>
    </article>
  );
}
```

#### 2. O Estilo Reativo (`src/CardPromocao.css`):
```css
.card-produto {
  background: #ffffff;
  border: 2px solid #e2e8f0;
  border-radius: 12px;
  padding: 1rem;
  text-align: center;
  width: 220px;
  transition: border-color 0.2s, box-shadow 0.2s;
}

/* Só "acende" quando a classe promocao entra via ternário */
.card-produto.promocao {
  border-color: #f59e0b;
  box-shadow: 0 0 0 3px #fef3c7;
}

.btn-toggle {
  margin-top: 0.8rem;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 8px;
  background: #3b82f6;
  color: #ffffff;
  font-weight: 600;
  cursor: pointer;
}
```

#### 3. Como Usar no Componente Pai (`src/App.jsx`):
```jsx
import { Header } from './Header';
import { CardPromocao } from './CardPromocao';

export function App() {
  return (
    <div className="app-container">
      <Header />
      <main>
        <CardPromocao />
      </main>
    </div>
  );
}

export default App;
```

> [!TIP]
> **Conte os pedaços do padrão:** 1 memória (`useState`) + 1 interruptor (`onClick` com `!`) + 2 reações (ternário na imagem/texto e classe dinâmica). É exatamente isso que você fará no Pokémon.

---

### 🛠️ 4. Desafio Ativo (Mão na Massa)

Neste step **você não cria arquivos novos**: mexe em exatamente 3 arquivos já existentes, nesta ordem:

```text
src/pokemons.js  ➜  src/PokemonCard.jsx  ➜  src/PokemonCard.css
  (+1 campo de      (+1 estado +1 botão     (+estilo do botão
     dados)            reativo)              e do card shiny)
```

1. **Alimentar os dados (`src/pokemons.js`):**
   * Adicione o campo `shinyImage` em **cada** Pokémon do array.
   * **O padrão do link:** é o mesmo URL da imagem normal, apenas inserindo `/shiny` antes do número:
     ```js
     // Normal: .../official-artwork/25.png
     // Shiny:  .../official-artwork/shiny/25.png
     ```
   * Exemplo completo do Pikachu (repita a lógica para Bulbasaur, Charmander e Squirtle):
     ```js
     {
       id: 25,
       name: "Pikachu",
       type: "Eletrico",
       image: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png",
       shinyImage: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/shiny/25.png"
     }
     ```

2. **Dar memória e botão ao card (`src/PokemonCard.jsx`) — o arquivo final:**
   ```jsx
   import { useState } from 'react';
   import './PokemonCard.css';

   export function PokemonCard({ pokemon }) {
     const { id, name, type, image, shinyImage } = pokemon;

     // NOVO: a memória deste card ("está exibindo o shiny?")
     const [isShiny, setIsShiny] = useState(false);

     return (
       // Classe dinâmica: borda dourada quando isShiny = true
       <article className={`pokemon-card ${isShiny ? 'shiny' : ''}`}>
         <header className="card-header">
           <span className="pokemon-id">{`#${String(id).padStart(3, '0')}`}</span>
           <h2 className="pokemon-name">{name}</h2>
         </header>

         <figure className="pokemon-image-container">
           {/* Ternário decide a imagem a partir do ESTADO */}
           <img 
             src={isShiny ? shinyImage : image} 
             alt={`Ilustração ${isShiny ? 'shiny' : 'normal'} de ${name}`} 
           />
         </figure>

         <ul className="pokemon-types">
           <li className={`type-badge type-${type.toLowerCase()}`}>{type}</li>
         </ul>

         {/* NOVO: rodapé de ações com o interruptor Shiny */}
         <footer className="card-acoes">
           <button 
             className="btn-shiny" 
             onClick={() => setIsShiny(!isShiny)}
           >
             {isShiny ? '✨ Ver Normal' : '⭐ Ver Shiny'}
           </button>
         </footer>
       </article>
     );
   }
   ```
   * Se você optou por não fazer o "Toque Visual" do Step 05, mantenha o `<span className="pokemon-id">` como estava — nada mais muda.

3. **Estilizar a interatividade (`src/PokemonCard.css`) — adicione ao final do arquivo:**
   ```css
   /* Rodapé de ações */
   .card-acoes {
     border-top: 1px solid #f1f5f9;
     display: flex;
     justify-content: center;
     padding: 0.8rem 1rem 1rem;
   }

   /* Botão interruptor */
   .btn-shiny {
     border: none;
     border-radius: 20px;
     background: linear-gradient(135deg, #f59e0b, #d97706);
     color: #ffffff;
     font-weight: 600;
     font-size: 0.85rem;
     padding: 0.5rem 1rem;
     cursor: pointer;
     transition: transform 0.15s, box-shadow 0.15s;
   }
   .btn-shiny:hover {
     transform: scale(1.05);
     box-shadow: 0 4px 12px rgba(245, 158, 11, 0.4);
   }

   /* Feedback dourado no card inteiro quando isShiny = true */
   .pokemon-card.shiny {
     border: 2px solid #f59e0b;
     box-shadow: 0 0 0 3px #fef3c7;
   }
   ```

4. **🌟 Desafio Extra (opcional) — o coração de Favorito:**
   * Agora que você domina **um** estado, treine a criação de um **segundo** estado independente no mesmo card:
     ```jsx
     const [isFavorite, setIsFavorite] = useState(false);

     <button 
       className="btn-favorito"
       onClick={() => setIsFavorite(!isFavorite)}
       aria-label="Favoritar Pokémon"
     >
       {isFavorite ? '❤️' : '🤍'}
     </button>
     ```
   * Faça a borda do card também reagir: `className={`pokemon-card ${isShiny ? 'shiny' : ''} ${isFavorite ? 'favoritado' : ''}`}`.
   * Guarde essa habilidade: no **Step 10** os favoritos deixarão de ser "esquecidos a cada F5" e serão persistidos no `localStorage`.

---

### 🧪 5. Teste de Validação

1. Salve os arquivos e abra `http://localhost:5173`.
2. Clique em **"⭐ Ver Shiny"** no Pikachu: a imagem deve trocar para a versão dourada **instantaneamente, sem recarregar a página**, e o botão deve virar **"✨ Ver Normal"**.
3. Clique novamente e confirme que o card volta ao estado original (imagem normal, sem borda dourada).
4. Ative o Shiny em UM card e confirme que **os outros permanecem normais** — cada `<PokemonCard />` possui sua própria memória `useState`.
5. Abra o Console (`F12`) e confirme que não há nenhum erro vermelho.
6. (Fez o extra?) Clique no 🤍 e confirme que ele vira ❤️ apenas no card clicado.

---

### ❓ 6. Quiz de Fixação (6 Questões de Múltipla Escolha)

#### Q1. O que é o Hook `useState` no React?
- (A) Uma função para conectar o site ao banco de dados MySQL.
- (B) Um recurso que permite aos componentes criar e gerenciar sua própria memória interna e redesenhar a tela quando ela muda.
- (C) Um comando do CSS para arredondar cantos de imagens.
- (D) Um plugin do VS Code.

> **Gabarito Comentado:** **(B)** O `useState` é o hook fundamental do React para gerenciar estado reativo em componentes funcionais.

#### Q2. Dada a declaração `const [isShiny, setIsShiny] = useState(false);`, qual é o papel de `setIsShiny`?
- (A) É a variável que guarda o nome do Pokémon.
- (B) É a função responsável por atualizar o valor de `isShiny` e avisar o React para redesenhar o componente.
- (C) É o estilo CSS do botão.
- (D) É uma tag HTML.

> **Gabarito Comentado:** **(B)** O segundo elemento retornado pelo `useState` é sempre a função atualizadora do estado.

#### Q3. Por que não devemos usar `document.querySelector` para alterar textos ou imagens no React?
- (A) Porque o JavaScript antigo foi proibido na internet.
- (B) Porque o React gerencia sua própria DOM Virtual e sobrescreverá qualquer mudança manual feita fora do fluxo de Estado.
- (C) Porque isso consome toda a memória RAM do computador.
- (D) Porque o `querySelector` só funciona no Internet Explorer.

> **Gabarito Comentado:** **(B)** O React controla a interface via Estado; alterações diretas na DOM passam por cima da DOM Virtual e são perdidas nas re-renderizações.

#### Q4. Qual expressão em JSX utiliza o Operador Ternário para alternar entre as opções "Sim" e "Não" baseado na variável `ativo`?
- (A) `{if ativo then "Sim" else "Não"}`
- (B) `{ativo ? "Sim" : "Não"}`
- (C) `{ativo == "Sim" && "Não"}`
- (D) `{switch(ativo) "Sim" : "Não"}`

> **Gabarito Comentado:** **(B)** O operador ternário em JSX segue a estrutura `condicao ? seVerdadeiro : seFalso`.

#### Q5. Como invertemos o valor de um estado booleano (ex: de `false` para `true`) dentro da função `onClick`?
- (A) `onClick={() => setIsShiny(!isShiny)}`
- (B) `onClick={isShiny = true}`
- (C) `onClick={delete isShiny}`
- (D) `onClick={() => isShiny + 1}`

> **Gabarito Comentado:** **(A)** Passar `!isShiny` para a função atualizadora inverte o valor booleano atual da memória do componente e dispara o redesenho.

#### Q6. Em uma grade com 4 cards de Pokémons, o que acontece se o usuário clicar no botão Shiny de um único card?
- (A) Todos os 4 cards mudam para a versão shiny ao mesmo tempo.
- (B) Apenas o card clicado altera sua imagem, pois cada componente filho possui sua própria instância isolada de `useState`.
- (C) O navegador fecha.
- (D) A página recarrega automaticamente.

> **Gabarito Comentado:** **(B)** Cada componente renderizado mantém seu próprio estado independente dos demais — o estado é local à instância.

---

### 📝 7. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Gerenciamento de Estado Reativo e Interatividade com React Hooks. Utilização do hook useState (memória do componente), escuta de eventos de clique (onClick), inversão de booleanos com o operador de negação, condicionais com operador ternário no JSX, classes CSS dinâmicas e isolamento de estado por instância de componente."*
