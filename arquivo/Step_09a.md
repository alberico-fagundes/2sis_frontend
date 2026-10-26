# 🚀 Step 09a: PokéAgenda — Ficha de Detalhes: O Modal e a Abertura por Clique

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica ( / Conceitual):** Aprenda o padrão de **Modal** (janela flutuante com `position: fixed`), **Renderização Condicional** com `&&` e `null`, estado "selecionado" com `useState(null)` e o conceito de **Propagação de Eventos (bubbling)** com `stopPropagation()`.
> * **🛠️ Trilha Prática (Projeto Integrador):** Enriqueça a busca de dados da PokéAPI (altura, peso, habilidades, tipos) e crie o `<PokemonModal />`: a ficha de detalhes que abre ao clicar em qualquer card e fecha no ✖ ou na área escura.

*(Este step está dividido em 09a e 09b: primeiro fazemos o modal **abrir e fechar com dados reais**; no Step 09b ele ganha as **abas de Estatísticas e Golpes**. Um conceito por step, sempre!)*

---

### 🧩 1. O Problema Prático (Cenário  - Problem Statement)

**O Dilema do Card Gigante:**  
O Prof. Carvalho quer consultar dados completos de cada Pokémon — altura, peso, habilidades e todos os tipos — mas o card da grade é pequeno e limpo. O estagiário tentou resolver "inchando" o `<PokemonCard />`: adicionou parágrafos e mais parágrafos dentro dele. Resultado: a grade virou um mosaico de textos cortados, os cards perderam o efeito hover, e a responsividade do CSS Grid quebrou.

Nem toda informação merece morar no card. **O card é o convite; a ficha completa é outra tela.** A solução padrão de mercado chama-se **Modal**: uma janela flutuante que nasce sobre a página quando o usuário pede detalhes.

**A Pergunta-Chave :**  
> *Como podemos usar o React (`useState` + renderização condicional com `&&`) para criar um `<PokemonModal />` que abre ao clicar em um card, mostra os detalhes daquele Pokémon específico e fecha com um clique?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 O que é um Modal (Janela Modal)?
* **Conceito:** É uma camada que "flutua" SOBRE a página, bloqueando a interação com o fundo até ser fechada. É como erguer uma ficha de papel sobre a mesa: a mesa continua lá, mas sua atenção está na ficha.
* **Anatomia CSS obrigatória:**
  * **Overlay** (a área escura): `position: fixed` cobrindo 100% da tela + fundo `rgba(0, 0, 0, 0.6)` + `z-index` alto.
  * **Container** (a ficha branca): também `position: fixed`, centralizado, com `z-index` maior que o overlay.
* **No React**, o modal não é "criado" nem "destruído" manualmente: ele simplesmente **existe no JSX quando há um Pokémon selecionado**, e **deixa de existir** quando não há.

#### 2.2 Renderização Condicional com `&&` e `null`
* O operador `&&` no JSX lê-se: *"mostre o lado direito SOMENTE SE o lado esquerdo for verdadeiro"*:
  ```jsx
  {selectedPokemon && <PokemonModal pokemon={selectedPokemon} />}
  ```
  * `selectedPokemon` é `null` ➜ a expressão inteira é `null` ➜ o React **não desenha nada**.
  * `selectedPokemon` é um objeto ➜ o modal aparece.
* **`useState(null)` — o padrão "selecionado":** para "qual item da lista está aberto agora?", o valor inicial é `null` (coisa nenhuma). Clicar em um card ➜ `setSelectedPokemon(pokemon)`. Fechar ➜ `setSelectedPokemon(null)`.

  ```jsx
  const [selectedPokemon, setSelectedPokemon] = useState(null); // nasce vazio
  ```

#### 2.3 Propagação de Eventos (Bubbling) e `stopPropagation()`
* **O clique viaja de dentro para fora.** Ao clicar no botão "Ver Shiny" (neto), o evento "sobe" para o rodapé (filho) e depois para o `<article>` do card (pai). Se o pai tem `onClick` para abrir o modal, ele abriria acidentalmente.
* **A solução:** dentro do handler do filho, avisamos que a viagem termina ali:
  ```jsx
  onClick={(e) => { e.stopPropagation(); /* ação local */ }}
  ```
* É o "não bate na porta do vizinho" do JavaScript.

> [!TIP]
> **Regra do componente "ficha":** o modal recebe `pokemon` (os dados para exibir) e `onClose` (a função que o pai usa para dizer "pode sumir"). Ele NÃO guarda lista, NÃO busca API e NÃO decide sozinho o que mostrar — quem manda é o pai.

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Veja o padrão "lista ➜ clique ➜ ficha flutuante" fora do domínio Pokémon, já completo (componente + CSS + App):

#### `src/AgendaTelefonica.jsx`:
```jsx
import { useState } from 'react';
import './AgendaTelefonica.css';

export function AgendaTelefonica() {
  const contatos = [
    { id: 1, nome: 'Dentista', telefone: '(11) 4002-8922' },
    { id: 2, nome: 'Encanador', telefone: '(11) 3333-1234' }
  ];

  // O padrão "selecionado": null = nada aberto
  const [contatoSelecionado, setContatoSelecionado] = useState(null);

  return (
    <section>
      <ul className="agenda">
        {contatos.map((contato) => (
          <li
            key={contato.id}
            className="agenda-item"
            onClick={() => setContatoSelecionado(contato)}
          >
            👤 {contato.nome}
          </li>
        ))}
      </ul>

      {/* && decide: com null, nada é desenhado; com objeto, a ficha aparece */}
      {contatoSelecionado && (
        <div className="modal-overlay" onClick={() => setContatoSelecionado(null)}>
          <div className="modal-ficha" onClick={(e) => e.stopPropagation()}>
            <h3>{contatoSelecionado.nome}</h3>
            <p>📞 {contatoSelecionado.telefone}</p>
            <button onClick={() => setContatoSelecionado(null)}>Fechar</button>
          </div>
        </div>
      )}
    </section>
  );
}
```

#### `src/AgendaTelefonica.css`:
```css
.agenda { list-style: none; padding: 0; display: grid; gap: 0.5rem; max-width: 400px; margin: 2rem auto; }
.agenda-item { background: #fff; padding: 1rem; border-radius: 8px; cursor: pointer; box-shadow: 0 2px 8px rgba(0,0,0,0.08); }

.modal-overlay {
  position: fixed;            /* flutua sobre a página inteira */
  inset: 0;                   /* cobre todos os cantos (top/right/bottom/left = 0) */
  background: rgba(0, 0, 0, 0.6);
  display: grid;
  place-items: center;
  z-index: 100;
}

.modal-ficha {
  background: #fff;
  border-radius: 16px;
  padding: 2rem;
  min-width: 260px;
  text-align: center;
}
```

#### Uso no `src/App.jsx`:
```jsx
import { AgendaTelefonica } from './AgendaTelefonica';

export function App() {
  return (
    <div className="app-container">
      <AgendaTelefonica />
    </div>
  );
}

export default App;
```

> [!TIP]
> **Conte as 3 peças do padrão modal:** (1) estado `selecionado` no pai, (2) `{selecionado && <camadas/>}` no JSX, (3) `stopPropagation()` no container para o clique de fechar SÓ na área escura. Você vai repetir as três agora.

---

### 🛠️ 4. Desafio Ativo (Mão na Massa)

```text
src/PokemonGrid.jsx   ➜ ganha estado selectedPokemon + dados mais ricos da API
src/PokemonCard.jsx   ➜ ganha onClick (abrir) + stopPropagation (não abrir à toa)
src/PokemonModal.jsx  ➜ NOVO: a ficha de detalhes
src/PokemonModal.css  ➜ NOVO: overlay, banner colorido por tipo
```

1. **Reescreva `src/PokemonGrid.jsx` — arquivo final completo:**
   ```jsx
   import { useState, useEffect } from 'react';
   import { PokemonCard } from './PokemonCard';
   import { PokemonFilters } from './PokemonFilters';
   import { PokemonModal } from './PokemonModal';
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
     const [searchTerm, setSearchTerm] = useState('');
     const [selectedType, setSelectedType] = useState('Todos');

     // NOVO: o padrão "selecionado" — null = nenhum modal aberto
     const [selectedPokemon, setSelectedPokemon] = useState(null);

     useEffect(() => {
       async function fetchPokemons() {
         try {
           const response = await fetch('https://pokeapi.co/api/v2/pokemon?limit=151');
           const data = await response.json();

           const detailedPokemons = await Promise.all(
             data.results.map(async (item) => {
               const pokeRes = await fetch(item.url);
               const pokeDetails = await pokeRes.json();

               // Helper: acha a estatística PELO NOME (mais seguro que stats[0], stats[1]...)
               const getStat = (nome) =>
                 pokeDetails.stats.find((s) => s.stat.name === nome)?.base_stat ?? 0;

               return {
                 id: pokeDetails.id,
                 name: pokeDetails.name.charAt(0).toUpperCase() + pokeDetails.name.slice(1),
                 type: tiposPT[pokeDetails.types[0].type.name] ?? 'Normal',
                 types: pokeDetails.types.map((t) => tiposPT[t.type.name] ?? t.type.name),
                 image: pokeDetails.sprites.other['official-artwork'].front_default,
                 shinyImage: pokeDetails.sprites.other['official-artwork'].front_shiny,
                 // NOVO: dados da ficha — a API devolve decímetros e hectogramas,
                 // então dividimos por 10 para obter metros e quilos
                 height: pokeDetails.height / 10,
                 weight: pokeDetails.weight / 10,
                 abilities: pokeDetails.abilities.map((a) => a.ability.name),
                 moves: pokeDetails.moves.slice(0, 20).map((m) => m.move.name),
                 stats: {
                   hp: getStat('hp'),
                   attack: getStat('attack'),
                   defense: getStat('defense'),
                   specialAttack: getStat('special-attack'),
                   specialDefense: getStat('special-defense'),
                   speed: getStat('speed')
                 }
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

     const pokemonsFiltrados = pokemons.filter((pokemon) => {
       const matchesSearch =
         pokemon.name.toLowerCase().includes(searchTerm.toLowerCase()) ||
         String(pokemon.id).includes(searchTerm);
       const matchesType = selectedType === 'Todos' || pokemon.type === selectedType;
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
               <PokemonCard
                 key={pokemon.id}
                 pokemon={pokemon}
                 onSeeDetails={() => setSelectedPokemon(pokemon)}  // NOVO: entrega a "abertura" ao card
               />
             ))}
           </main>
         )}

         {/* NOVO: o && — só existe modal se houver selecionado */}
         {selectedPokemon && (
           <PokemonModal
             pokemon={selectedPokemon}
             onClose={() => setSelectedPokemon(null)}
           />
         )}
       </section>
     );
   }
   ```

2. **Atualize o `src/PokemonCard.jsx` — arquivo final completo:**
   ```jsx
   import { useState } from 'react';
   import './PokemonCard.css';

   export function PokemonCard({ pokemon, onSeeDetails }) {
     const { id, name, type, image, shinyImage } = pokemon;
     const [isShiny, setIsShiny] = useState(false);

     return (
       // O card inteiro virou um convite: clicar abre a ficha (onSeeDetails)
       <article
         className={`pokemon-card ${isShiny ? 'shiny' : ''}`}
         onClick={onSeeDetails}
       >
         <header className="card-header">
           <span className="pokemon-id">{`#${String(id).padStart(3, '0')}`}</span>
           <h2 className="pokemon-name">{name}</h2>
         </header>

         <figure className="pokemon-image-container">
           <img
             src={isShiny ? shinyImage : image}
             alt={`Ilustração ${isShiny ? 'shiny' : 'normal'} de ${name}`}
           />
         </figure>

         <ul className="pokemon-types">
           <li className={`type-badge type-${type.toLowerCase()}`}>{type}</li>
         </ul>

         {/* IMPORTANTE: onClick={onSeeDetails} NÃO vai aqui no rodapé!
             Sem stopPropagation, clicar em "Ver Shiny" tambem abriria o modal,
             porque o clique "sobe" dos filhos para o pai (bubbling). */}
         <footer className="card-acoes" onClick={(e) => e.stopPropagation()}>
           <button className="btn-shiny" onClick={() => setIsShiny(!isShiny)}>
             {isShiny ? '✨ Ver Normal' : '⭐ Ver Shiny'}
           </button>
         </footer>
       </article>
     );
   }
   ```
   * Ah, e garanta o sinal visual de clicável no `src/PokemonCard.css`:
     ```css
     .pokemon-card { cursor: pointer; }
     ```
   * *(Fez o Desafio Extra do Step 06? Mantenha o botão de coração e o estado `isFavorite` no seu card — o `stopPropagation()` do `<footer>` já protege os dois botões. No Step 10 esse botão será substituído pela versão persistente.)*

3. **Criar o componente da ficha (`src/PokemonModal.jsx`):**
   ```jsx
   import './PokemonModal.css';

   export function PokemonModal({ pokemon, onClose }) {
     const { id, name, types, image, height, weight, abilities } = pokemon;

     return (
       // Overlay: clique AQUI fecha (é o "fora da ficha")
       <div className="modal-overlay" onClick={onClose}>
         {/* Container: o stopPropagation impede o clique de "vazar" para o overlay */}
         <div className="modal-container" onClick={(e) => e.stopPropagation()}>
           <button className="btn-close-modal" onClick={onClose} aria-label="Fechar ficha">
             ✖
           </button>

           {/* Banner com a cor do tipo principal (classes .bg-type-* no CSS) */}
           <header className={`modal-banner bg-type-${types[0].toLowerCase()}`}>
             <span className="modal-pokemon-number">{`#${String(id).padStart(3, '0')}`}</span>
             <h2 className="modal-pokemon-name">{name}</h2>
             <figure className="modal-pokemon-image-box">
               <img src={image} alt={`Ilustração oficial de ${name}`} />
             </figure>
           </header>

           {/* Badges de TODOS os tipos (o card mostrava só o principal) */}
           <ul className="modal-types">
             {types.map((tipo) => (
               <li key={tipo} className={`type-badge type-${tipo.toLowerCase()}`}>
                 {tipo}
               </li>
             ))}
           </ul>

           <section className="modal-info">
             <p><strong>Altura:</strong> {height} m</p>
             <p><strong>Peso:</strong> {weight} kg</p>
             <p><strong>Habilidades:</strong> {abilities.join(', ')}</p>
           </section>
         </div>
       </div>
     );
   }
   ```

4. **Estilizar o modal (`src/PokemonModal.css`):**
   ```css
   .modal-overlay {
     position: fixed;
     inset: 0;
     background: rgba(15, 23, 42, 0.65);
     display: grid;
     place-items: center;
     z-index: 100;
     padding: 1rem;
   }

   .modal-container {
     position: relative;
     background: #ffffff;
     border-radius: 20px;
     width: min(420px, 100%);
     max-height: 90vh;
     overflow-y: auto;
     box-shadow: 0 24px 64px rgba(0, 0, 0, 0.35);
     padding-bottom: 1.5rem;
   }

   .btn-close-modal {
     position: absolute;
     top: 0.75rem;
     right: 0.75rem;
     width: 2rem;
     height: 2rem;
     border: none;
     border-radius: 50%;
     background: rgba(255, 255, 255, 0.9);
     color: #0f172a;
     font-size: 0.9rem;
     cursor: pointer;
     z-index: 2;
   }

   .modal-banner {
     display: grid;
     justify-items: center;
     gap: 0.25rem;
     padding: 1.25rem 1rem 0.5rem;
     color: #ffffff;
     border-radius: 20px 20px 0 0;
   }

   .modal-pokemon-number { font-weight: 700; opacity: 0.85; }
   .modal-pokemon-name { margin: 0; text-transform: capitalize; font-size: 1.6rem; }
   .modal-pokemon-image-box img { width: 160px; height: 160px; object-fit: contain; }

   .modal-types {
     list-style: none;
     display: flex;
     justify-content: center;
     gap: 0.5rem;
     padding: 1rem 0 0;
     margin: 0;
   }

   .modal-info {
     max-width: 300px;
     margin: 1rem auto 0;
     padding: 0 1.5rem;
     color: #334155;
   }

   /* Banner colorido por tipo (mesmas cores das badges dos Steps 03/08) */
   .bg-type-planta    { background: linear-gradient(135deg, #57b952, #3e8e41); }
   .bg-type-fogo      { background: linear-gradient(135deg, #ff421d, #c62828); }
   .bg-type-agua      { background: linear-gradient(135deg, #268bf7, #1565c0); }
   .bg-type-eletrico  { background: linear-gradient(135deg, #fbc02d, #f57f17); }
   .bg-type-normal    { background: linear-gradient(135deg, #a8a878, #787860); }
   .bg-type-veneno    { background: linear-gradient(135deg, #9f52c8, #7b1fa2); }
   .bg-type-psiquico  { background: linear-gradient(135deg, #f59785, #e57373); }
   .bg-type-gelo      { background: linear-gradient(135deg, #68c8ee, #29b6f6); }
   .bg-type-pedra     { background: linear-gradient(135deg, #c8b878, #a1887f); }
   .bg-type-fantasma  { background: linear-gradient(135deg, #6a6aa8, #4527a0); }
   .bg-type-voador    { background: linear-gradient(135deg, #a8a8f8, #7986cb); }
   .bg-type-inseto    { background: linear-gradient(135deg, #a8b828, #9ccc65); }
   .bg-type-dragao    { background: linear-gradient(135deg, #7038f8, #5e35b1); }
   .bg-type-lutador   { background: linear-gradient(135deg, #c82878, #ad1457); }
   .bg-type-solo      { background: linear-gradient(135deg, #d8bc78, #bcaaa4); }
   ```
   * As badges coloridas (`.type-badge`, `.type-fogo`...) **já existem** do Step 03 e são globais — reutilizamos sem copiar nada.

---

### 🧪 5. Teste de Validação

1. Abra a aplicação (`http://localhost:5173`) e espere a carga dos 151 Pokémons.
2. **Clique no card do Pikachu:** a ficha flutuante abre com banner AMARELO (Elétrico), `#025`, imagem grande, badge de tipo e altura/peso/habilidades reais.
3. Clique no Charmander (sem fechar o outro? o React troca o conteúdo na hora — o modal é UM, o dado que muda).
4. Feche clicando no **✖**, depois teste fechar clicando na **área escura** ao redor.
5. Teste o bubbling: clique em **"⭐ Ver Shiny"** dentro de um card — a imagem altera e o modal **NÃO** abre (`stopPropagation` funcionou).
6. Verifique o peso do Pikachu (6.0 kg) e do Charizard — a conversão `/10` da API salvou a física de Kanto.

---

### ❓ 6. Quiz de Fixação (6 Questões de Múltipla Escolha)

#### Q1. O que é um Modal em interfaces web?
- (A) Um tipo de banco de dados.
- (B) Uma janela flutuante sobre a página que exibe conteúdo focado e bloqueia a interação com o fundo até ser fechada.
- (C) Uma aba do navegador.
- (D) Um componente que só funciona com o servidor ligado.

> **Gabarito Comentado:** **(B)** O modal sobrepõe a interface atual com uma camada (`position: fixed` + `z-index`) para conteúdo pontual, como detalhes de um item.

#### Q2. No padrão "selecionado", qual é o valor inicial correto de `const [selectedPokemon, setSelectedPokemon] = useState(...)`, e por quê?
- (A) `useState('Pikachu')`, para o site já abrir bonito.
- (B) `useState([])`, porque modal é uma lista.
- (C) `useState(null)`, representando "nenhum Pokémon selecionado" — nada deve ser renderizado no início.
- (D) `useState(true)`, porque modal é ligado/desligado.

> **Gabarito Comentado:** **(C)** `null` é o "vazio significativo" do JavaScript para objetos ainda não escolhidos, e trava o render condicional do modal.

#### Q3. O que faz a expressão JSX `{selectedPokemon && <PokemonModal />}`?
- (A) Renderiza o modal sempre, escondendo com CSS.
- (B) Renderiza o modal apenas quando `selectedPokemon` for um objeto; com `null`, o React desenha nada.
- (C) Remove o `<PokemonModal />` do arquivo.
- (D) Cria uma cópia do Pokémon no estado.

> **Gabarito Comentado:** **(B)** Com `&&`, se o lado esquerdo for "falsy" (`null`), o React para por ali e não desenha o lado direito — nada de modal na tela.

#### Q4. Por que um clique no botão "Ver Shiny" do card também abriria o modal se não usássemos `e.stopPropagation()`?
- (A) Porque botões abrem modais automaticamente no React.
- (B) Porque eventos "sobem" do elemento clicado para seus ancestrais (bubbling), e o `<article>` do card tem `onClick` que abre o modal.
- (C) Porque o `useState` se confunde com dois cliques.
- (D) Porque o CSS `z-index` inverte os elementos.

> **Gabarito Comentado:** **(B)** O evento viaja de dentro para fora: botão ➜ footer ➜ article. O `stopPropagation()` corta a viagem no footer.

#### Q5. A PokéAPI devolve `height: 4` para o Pikachu (que mede 0,4 m) e `weight: 60` (6 kg). Por que dividimos por 10?
- (A) Porque os números da API estão "inchados" por bug.
- (B) Porque a API usa unidades diferentes das nossas: decímetros (altura) e hectogramas (peso); dividir por 10 converte para metros e quilos.
- (C) Para caber na tela do celular.
- (D) Porque JavaScript não conhece o Pikachu.

> **Gabarito Comentado:** **(B)** 1 decímetro = 0,1 metro e 1 hectograma = 0,1 quilo; a conversão `/10` transforma em unidades compreensíveis.

#### Q6. Qual propriedade CSS faz o overlay cobrir a JANELA INTEIRA mesmo com a página rolada?
- (A) `display: flex`
- (B) `position: static`
- (C) `position: fixed` com `inset: 0`
- (D) `overflow: scroll`

> **Gabarito Comentado:** **(C)** `position: fixed` ancora o elemento à viewport (não ao documento), e `inset: 0` estica para todos os cantos.

---

### 📝 7. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Componentes Modais e Renderização Condicional em React. Padrão selecionado com useState(null), renderização seletiva com operador lógico &&, propagação de eventos (bubbling) e stopPropagation, posicionamento fixo de overlays, enriquecimento e normalização de dados de API (conversão de unidades e lookup de estatísticas por nome)."*
