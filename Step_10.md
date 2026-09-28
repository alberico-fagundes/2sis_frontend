# 🚀 Step 10: PokéAgenda — Persistência de Favoritos com `localStorage`

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica ( / Conceitual):** Domine a API de armazenamento do navegador (**`localStorage`**), a serialização com **`JSON.stringify()` / `JSON.parse()`**, a **inicialização preguiçosa de estado** (*Lazy Initializer*) e a sincronização automática com **`useEffect`** (dependência `[favorites]`).
> * **🛠️ Trilha Prática (Projeto Integrador):** Transforme o coração do card em favoritos DE VERDADE: o estado sai de dentro do `PokemonCard` (memória RAM volátil) e vira uma lista única no `<PokemonGrid />`, persistida no navegador — sobrevive ao F5, ao fechamento da aba e ao fim do expediente.

---

### 🧩 1. O Problema Prático (Cenário  - Problem Statement)

**O Dilema dos Favoritos que Desaparecem no F5:**  
Um treinador passou 20 minutos garimpando a PokéAgenda e marcou seus 10 Pokémons favoritos com o botão ❤️. Sem querer, esbarrou na tecla **F5**. Para o seu desespero, todos os corações voltaram a ficar brancos 🤍.

O motivo é nobre e trágico ao mesmo tempo: `useState` guarda valor na **memória RAM** do navegador. Recarregou a página ➜ o componente renasceu do zero ➜ `useState(false)` de novo ➜ favoritos zerados.

**A Pergunta-Chave :**  
> *Como podemos usar o **`localStorage` do navegador** e o **`useEffect` do React** para salvar a lista de favoritos permanentemente no computador do usuário — e ainda reaproveitar essa lista para o card saber, já na primeira tela, quem é favorito?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 O que é o `localStorage` do Navegador?
* **Conceito:** um pequeno "baú" embutido em todos os navegadores modernos onde a página pode guardar textos **no computador do usuário**.
* **Características:**
  * Os dados **NÃO somem** ao recarregar (`F5`), fechar a aba ou reiniciar o PC.
  * Só armazena **texto** (String). Nada de número, objeto ou array "direto".
* **Os 3 métodos que você usa sempre:**
  1. `localStorage.setItem('chave', 'valor')` — salva.
  2. `localStorage.getItem('chave')` — lê (ou `null` se nunca foi salva).
  3. `localStorage.removeItem('chave')` — apaga uma chave.

> [!TIP]
> **Prefixo de chave:** use sempre um "sobrenome" para as chaves, ex: `@pokeagenda:favoritos`. É como etiquetar potes na geladeira compartilhada: evita colisão com outros apps e te deixa surpreso com quem mais guarda iogurte ali.

#### 2.2 Convertendo Array ➜ Texto e Texto ➜ Array (JSON)
* Como o baú só aceita texto, embalamos nosso array com `JSON.stringify` e o desembalamos com `JSON.parse`:
  ```js
  const favoritos = [25, 1, 94];

  const texto = JSON.stringify(favoritos); // '[25,1,94]' ➜ String salvable
  localStorage.setItem('@pokeagenda:favoritos', texto);

  const lido = localStorage.getItem('@pokeagenda:favoritos'); // '[25,1,94]'
  const arrayOriginal = JSON.parse(lido);                    // [25, 1, 94] ➜ array de verdade
  ```
* **Se a chave não existir ainda** (primeiro acesso), `getItem` devolve `null`. Tentar parsear `null` sem proteção é receita de erro ➜ por isso o teste `lido ? JSON.parse(lido) : []`.

#### 2.3 Inicialização Preguiçosa do Estado (*Lazy State Initializer*)
* Em vez de o estado nascer vazio e "correr atrás" do storage, passamos uma **função** para o `useState` — ela roda uma única vez, no nascimento do componente, e decide o valor inicial:
  ```js
  const [favorites, setFavorites] = useState(() => {
    const salvos = localStorage.getItem('@pokeagenda:favoritos');
    return salvos ? JSON.parse(salvos) : [];
  });
  ```
  * `useState(valor)` ➜ valor fixo. `useState(função)` ➜ React chama a função para descobrir o valor inicial.

#### 2.4 O Estado que "Mora em Lugar Melhor" (Lifting State Up)
* No Desafio Extra do Step 06, o coração morava DENTRO de cada card (cada um com `isFavorite` próprio). Para persistir, inverteremos o lado do fluxo do Step 03:
  * **Antes:** `PokemonCard` ➜ decide sozinho seu coração ➜ RAM ➜ F5 ➜ esquece.
  * **Depois:** `PokemonGrid` (o pai da lista) ➜ guarda `favorites` ➜ injeta `isFavorite` e `onToggleFavorite` de volta via **props** ➜ sincroniza com o baú do navegador ➜ F5 ➜ remembers.
* Um coração agora é **informação vinda do pai** (prop de leitura) + **pedido enviado ao pai** (callback de escrita). Exatamente o padrão do `<PokemonFilters />` do Step 08.

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

O exemplo mais enxuto possível do trio "baú ➜ estado ➜ baú":

#### `src/SalvarNome.jsx`:
```jsx
import { useState, useEffect } from 'react';

export function SalvarNome() {
  // 1. Nasce JÁ LENDO o baú (lazy initializer)
  const [nome, setNome] = useState(() => localStorage.getItem('@app:nome') || '');

  // 2. Sempre que 'nome' mudar, o baú é atualizado. [nome] = só quando ELE muda!
  useEffect(() => {
    localStorage.setItem('@app:nome', nome);
  }, [nome]);

  return (
    <div>
      <input
        type="text"
        value={nome}
        onChange={(e) => setNome(e.target.value)}
        placeholder="Digite seu nome..."
      />
      <p>Seu nome salvo é: {nome || '...'} 💾</p>
    </div>
  );
}
```

#### Uso no `src/App.jsx`:
```jsx
import { Header } from './Header';
import { SalvarNome } from './SalvarNome';

export function App() {
  return (
    <div className="app-container">
      <Header />
      <SalvarNome />
    </div>
  );
}

export default App;
```

> [!TIP]
> **Note o par simétrico:** `useState(() => getItem(...))` na descida (storage ➜ tela) e `useEffect(..., [variavel])` na subida (tela ➜ storage). É um ida-e-volta: o estado é a ponte.

---

### 🛠️ 4. Desafio Ativo (Mão na Massa)

```text
src/PokemonGrid.jsx  ➜ DONO dos favoritos: estado lazy + useEffect salvando + toggle
src/PokemonCard.jsx  ➜ deixa de guardar coração; recebe isFavorite + onToggleFavorite
src/PokemonCard.css  ➜ estilo do coração e do card favoritado
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
     const [selectedPokemon, setSelectedPokemon] = useState(null);

     // NOVO: lista de IDs favoritos — nasce LIDA do baú, não vazia
     const [favorites, setFavorites] = useState(() => {
       const salvos = localStorage.getItem('@pokeagenda:favoritos');
       return salvos ? JSON.parse(salvos) : [];
     });

     // Busca na API (Step 07/09a) — inalterada
     useEffect(() => {
       async function fetchPokemons() {
         try {
           const response = await fetch('https://pokeapi.co/api/v2/pokemon?limit=151');
           const data = await response.json();

           const detailedPokemons = await Promise.all(
             data.results.map(async (item) => {
               const pokeRes = await fetch(item.url);
               const pokeDetails = await pokeRes.json();
               const getStat = (nome) =>
                 pokeDetails.stats.find((s) => s.stat.name === nome)?.base_stat ?? 0;

               return {
                 id: pokeDetails.id,
                 name: pokeDetails.name.charAt(0).toUpperCase() + pokeDetails.name.slice(1),
                 type: tiposPT[pokeDetails.types[0].type.name] ?? 'Normal',
                 types: pokeDetails.types.map((t) => tiposPT[t.type.name] ?? t.type.name),
                 image: pokeDetails.sprites.other['official-artwork'].front_default,
                 shinyImage: pokeDetails.sprites.other['official-artwork'].front_shiny,
                 height: pokeDetails.height / 10,
                 weight: pokeDetails.weight / 10,
                 abilities: pokeDetails.abilities.map((a) => a.ability.name),
                 moves: pokeDetails.moves.slice(0, 20).map((m) => m.move.name),
                 stats: {
                   hp: getStat('hp'), attack: getStat('attack'), defense: getStat('defense'),
                   specialAttack: getStat('special-attack'),
                   specialDefense: getStat('special-defense'), speed: getStat('speed')
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

     // NOVO: todo favorito novo/removeido cai aqui e regrava o baú
     useEffect(() => {
       localStorage.setItem('@pokeagenda:favoritos', JSON.stringify(favorites));
     }, [favorites]); // [favorites]: só quando a LISTA muda (não no fetch, não na busca!)

     // NOVO: adiciona ou remove o id da lista, SEM MUTAR a anterior (função updater)
     function toggleFavorite(pokemonId) {
       setFavorites((prevFavorites) => {
         if (prevFavorites.includes(pokemonId)) {
           return prevFavorites.filter((id) => id !== pokemonId); // já era ➜ sai
         }
         return [...prevFavorites, pokemonId]; // não era ➜ entra (novo array via spread)
       });
     }

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
                 onSeeDetails={() => setSelectedPokemon(pokemon)}
                 // DUAS NOVAS PROPS: a verdade do coração vem do pai
                 isFavorite={favorites.includes(pokemon.id)}
                 onToggleFavorite={() => toggleFavorite(pokemon.id)}
               />
             ))}
           </main>
         )}

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

2. **Reescreva `src/PokemonCard.jsx` — coração agora é de mentirinha (vem de fora):**
   ```jsx
   import { useState } from 'react';
   import './PokemonCard.css';

   export function PokemonCard({ pokemon, onSeeDetails, isFavorite, onToggleFavorite }) {
     const { id, name, type, image, shinyImage } = pokemon;

     // isShiny CONTINUA local (é preferência visual do momento)
     const [isShiny, setIsShiny] = useState(false);
     // (Se você fez o Desafio Extra do Step 06, APAGUE o useState do isFavorite daqui —
     //  a partir de agora o coração é controlado pelo PAI!)

     return (
       <article
         className={`pokemon-card ${isShiny ? 'shiny' : ''} ${isFavorite ? 'favoritado' : ''}`}
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

         <footer className="card-acoes" onClick={(e) => e.stopPropagation()}>
           <button className="btn-shiny" onClick={() => setIsShiny(!isShiny)}>
             {isShiny ? '✨ Ver Normal' : '⭐ Ver Shiny'}
           </button>

           {/* O botão não DECIDE nada: só telefona para o pai */}
           <button
             className="btn-favorito"
             aria-label={isFavorite ? `Remover ${name} dos favoritos` : `Favoritar ${name}`}
             onClick={onToggleFavorite}
           >
             {isFavorite ? '❤️' : '🤍'}
           </button>
         </footer>
       </article>
     );
   }
   ```

3. **Estilos novos no fim do `src/PokemonCard.css`:**
   ```css
   .btn-favorito {
     border: none;
     background: transparent;
     font-size: 1.4rem;
     cursor: pointer;
     line-height: 1;
     transition: transform 0.15s;
   }
   .btn-favorito:hover { transform: scale(1.25); }

   .pokemon-card.favoritado {
     border: 2px solid #dc2626;
     box-shadow: 0 0 0 3px rgba(220, 38, 38, 0.15);
   }
   ```

> [!IMPORTANT]
> **Por que `setFavorites((prev) => ...)` e não `favorites.push(id)`?** Porque estado no React NUNCA é mutado (lembra da imutabilidade das Props?). `push`/`filter` sobre o array antigo podem até funcionar no susto, mas o padrão seguro é a **função updater** com **novo array** (`[...prev, id]`). Além de correto, é o que dispara o `useEffect` de gravação.

---

### 🧪 5. Teste de Validação

1. Abra a aplicação (`http://localhost:5173`) e espere os cards carregarem.
2. Favorite 3 Pokémons (ex: **Pikachu, Bulbasaur e Gengar**) — note a borda vermelha `.favoritado`.
3. Pressione **F5**. Aguarde o loading e confirme que os **3 corações continuam ❤️**.
4. Abra o DevTools (`F12`) ➜ aba **Application/Armazenamento** ➜ **Local Storage**: a chave `@pokeagenda:favoritos` guarda algo como `[25,1,94]`.
5. Desfavorite um e F5 de novo ➜ o array salvo diminuiu.
6. Feche a aba, reabra o site ➜ favoritos intactos (persistem até limpar dados do navegador).

---

### ❓ 6. Quiz de Fixação (6 Questões de Múltipla Escolha)

#### Q1. O que é o `localStorage` nos navegadores web?
- (A) Um antivírus instalado no computador.
- (B) Uma API do navegador que salva dados em formato texto de forma persistente no computador do usuário.
- (C) Uma extensão do VS Code.
- (D) Um recurso pago do Google Chrome.

> **Gabarito Comentado:** **(B)** É a solução nativa de armazenamento persistente *client-side* do navegador.

#### Q2. Qual método do `localStorage` grava uma informação nova?
- (A) `localStorage.getItem()`
- (B) `localStorage.setItem('chave', 'valor')`
- (C) `localStorage.push()`
- (D) `localStorage.save()`

> **Gabarito Comentado:** **(B)** `setItem` grava o par chave/valor (sempre texto).

#### Q3. Por que usamos `JSON.stringify()` antes de salvar o array de favoritos?
- (A) Porque o `localStorage` só aceita Strings, e `stringify` embala o array como texto.
- (B) Para criptografar a senha do usuário.
- (C) Para diminuir as imagens.
- (D) Para trocar a cor do texto.

> **Gabarito Comentado:** **(A)** O baú do navegador armazena exclusivamente texto; estruturas viram JSON textográfico com `stringify`.

#### Q4. Qual método reconverte o texto do baú de volta em array funcional?
- (A) `JSON.parse()`
- (B) `JSON.toString()`
- (C) `JSON.convert()`
- (D) `JSON.toArray()`

> **Gabarito Comentado:** **(A)** `JSON.parse` recria o objeto/array a partir do texto JSON.

#### Q5. Quando os dados do `localStorage` somem do computador?
- (A) Ao fechar a aba.
- (B) Ao desligar o PC.
- (C) Só se o código chamar `removeItem/clear`, ou o usuário limpar os dados de navegação.
- (D) A cada 5 minutos.

> **Gabarito Comentado:** **(C)** Diferente do `sessionStorage`, o `localStorage` persiste indefinidamente.

#### Q6. Por que o botão de coração não usa mais `const [isFavorite, setIsFavorite] = useState(false)` dentro do card?
- (A) Porque `useState` dentro de card não funciona.
- (B) Porque o "dono da verdade" subiu para o `PokemonGrid` (que persiste no `localStorage`) e injeta `isFavorite`/`onToggleFavorite` via props.
- (C) Porque corações não são permitidos em JSX.
- (D) Porque o `localStorage` substitui o React.

> **Gabarito Comentado:** **(B)** Uma única lista de favoritos coerente + persistente só existe se o estado for elevado ao pai da coleção (lifting state up).

---

### 📝 7. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Persistência de Dados no Cliente com Web Storage API. Métodos localStorage.setItem/getItem, serialização com JSON.stringify/parse, Lazy State Initializer, useEffect com array de dependências [favorites] como sincronizador, atualização imutável com função updater e padrão de elevação de estado (lifting state up) com props de leitura e callbacks de escrita."*
