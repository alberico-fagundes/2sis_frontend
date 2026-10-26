# 🚀 Step 09b: PokéAgenda — O Modal com Abas: Sobre, Estatísticas e Golpes

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica ( / Conceitual):** Domine o **Padrão de Navegação por Abas (Tabs)** com `useState`, a **renderização condicional de painéis** com múltiplos `&&`, a **classe dinâmica do botão ativo** e **estilos inline calculados** (`style={{ width: ... }}`) para as barras de estatísticas.
> * **🛠️ Trilha Prática (Projeto Integrador):** Transforme o `<PokemonModal />` do Step 09a em uma ficha profissional de 3 abas — **Sobre**, **Estatísticas de Combate** (barras proporcionais) e **Golpes** (pílulas) — no nível dos grandes Pokédex de mercado.

*(Continuação do Step 09a: modal abrindo e fechando com dados reais. Aqui só mudamos o miolo do modal.)*

---

### 🧩 1. O Problema Prático (Cenário  - Problem Statement)

**O Dilema do Pergaminho Infinito:**  
Com o modal pronto, os treinadores pediram TUDO: altura, peso, habilidades, as 6 estatísticas de combate e a lista de golpes. O estagiário colocou tudo junto na mesma tela do modal — e como alguns Pokémons têm dezenas de golpes, a "ficha" virou um **pergaminho interminável**: o usuário precisava rolar, rolar e rolar, se perdendo no meio dos dados e clicando sem querer no botão errado.

Excesso de informação em uma única tela satura a atenção e polui a interface.

**A Pergunta-Chave :**  
> *Como podemos usar o **Estado do React (`useState`)** para criar um sistema de **Abas** dentro do modal, onde o usuário alterna entre "Sobre", "Estatísticas" e "Golpes" vendo apenas uma seção por vez?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 O Padrão de Navegação por Abas (Tabs UI Pattern)
* **Conceito:** o conteúdo é dividido em painéis; **apenas um** é exibido por vez. Em React, isso é puramente um estado com nome:
  ```jsx
  const [activeTab, setActiveTab] = useState('about'); // 'about' | 'stats' | 'moves'
  ```
* **Analogia:** é um interruptor de 3 posições. O estado guarda QUAL posição está ligada; os botões só mudam a posição; a tela decide o que desenhar com base na posição.

#### 2.2 Renderização Condicional de Painéis (&& em série)
* Cada painel se apresenta se (e somente se) for o escolhido:
  ```jsx
  {activeTab === 'about' && <div>...Sobre...</div>}
  {activeTab === 'stats' && <div>...Estatísticas...</div>}
  {activeTab === 'moves' && <div>...Golpes...</div>}
  ```
* É o MESMO `&&` do Step 09a (modal aberto/fechado), agora aplicado a três seções.

#### 2.3 O Botão de Aba "Aceso" (Classe Dinâmica)
* A técnica que você já domina desde o Step 06 (ternário dentro do `className`):
  ```jsx
  className={`tab-btn ${activeTab === 'stats' ? 'active' : ''}`}
  ```

#### 2.4 Barras de Estatísticas com Estilo Inline Calculado
* Estatísticas variam de 0 a ~180. A largura da barra é uma **porcentagem do valor**, aplicada via `style`:
  ```jsx
  <div className="stat-fill" style={{ width: `${(valor / 180) * 100}%` }}></div>
  ```
  * No JSX, o `style` recebe um **objeto** com propriedades em camelCase (`width`, `backgroundColor`...) — não uma string CSS.
* **Bônus anti-repetição (DRY):** em vez de escrever 6 blocos parecidos de `stat-line`, montamos um array de rótulos/valores e usamos o `.map()` do Step 05 para gerar as 6 barras.

> [!TIP]
> **O segredo do modal que "esquece":** quando você fecha o modal, o `{selectedPokemon && ...}` do Step 09a remove o componente da tela (**unmount**) e toda a memória dele (`activeTab`) deixa de existir. Ao reabrir, o `useState('about')` recomeça — sua ficha volta limpa na aba "Sobre". Isso não é bug: é o React sendo honesto!

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Um painel de 2 abas completo (componente + CSS + App) — depois você escala para 3:

#### `src/TabsExemplo.jsx`:
```jsx
import { useState } from 'react';
import './TabsExemplo.css';

export function TabsExemplo() {
  const [aba, setAba] = useState('perfil');

  return (
    <div className="card-tabs">
      <nav className="botoes-abas">
        <button
          className={`aba-btn ${aba === 'perfil' ? 'ativa' : ''}`}
          onClick={() => setAba('perfil')}
        >
          👤 Perfil
        </button>
        <button
          className={`aba-btn ${aba === 'config' ? 'ativa' : ''}`}
          onClick={() => setAba('config')}
        >
          ⚙️ Configurações
        </button>
      </nav>

      <main className="conteudo-aba">
        {aba === 'perfil' && <p>Alex Silva — Dev Frontend</p>}
        {aba === 'config' && <p>Tema: escuro | Idioma: pt-BR</p>}
      </main>
    </div>
  );
}
```

#### `src/TabsExemplo.css`:
```css
.card-tabs { max-width: 400px; margin: 2rem auto; background: #fff; border-radius: 12px; overflow: hidden; box-shadow: 0 4px 12px rgba(0,0,0,0.1); }
.botoes-abas { display: flex; border-bottom: 1px solid #e2e8f0; }
.aba-btn { flex: 1; padding: 0.8rem; border: none; background: #f1f5f9; cursor: pointer; font-weight: 600; }
.aba-btn.ativa { background: #ffffff; color: #dc2626; box-shadow: inset 0 -3px 0 #dc2626; }
.conteudo-aba { padding: 1.25rem; }
```

#### Uso no `src/App.jsx`:
```jsx
import { TabsExemplo } from './TabsExemplo';

export function App() {
  return (
    <div className="app-container">
      <TabsExemplo />
    </div>
  );
}

export default App;
```

---

### 🛠️ 4. Desafio Ativo (Mão na Massa)

São **2 arquivos**: reescrever o `PokemonModal.jsx` por inteiro e completar o `PokemonModal.css`. O `PokemonGrid.jsx` **não muda** (ele já entregou `stats`, `moves` e `abilities` no Step 09a!).

1. **Reescreva `src/PokemonModal.jsx` — arquivo final completo com abas:**
   ```jsx
   import { useState } from 'react';
   import './PokemonModal.css';

   export function PokemonModal({ pokemon, onClose }) {
     // O interruptor de 3 posições: começa em "Sobre"
     const [activeTab, setActiveTab] = useState('about');

     const { id, name, types, image, height, weight, abilities, moves, stats } = pokemon;

     // DRY: 6 linhas de stat geradas de um array com .map() (Step 05 trabalhando de novo!)
     const barrasDeStats = [
       { rotulo: 'HP',          valor: stats.hp },
       { rotulo: 'Ataque',      valor: stats.attack },
       { rotulo: 'Defesa',      valor: stats.defense },
       { rotulo: 'Atq. Esp.',   valor: stats.specialAttack },
       { rotulo: 'Def. Esp.',   valor: stats.specialDefense },
       { rotulo: 'Velocidade',  valor: stats.speed }
     ];

     return (
       <div className="modal-overlay" onClick={onClose}>
         <div className="modal-container" onClick={(e) => e.stopPropagation()}>
           <button className="btn-close-modal" onClick={onClose} aria-label="Fechar ficha">✖</button>

           <header className={`modal-banner bg-type-${types[0].toLowerCase()}`}>
             <span className="modal-pokemon-number">{`#${String(id).padStart(3, '0')}`}</span>
             <h2 className="modal-pokemon-name">{name}</h2>
             <figure className="modal-pokemon-image-box">
               <img src={image} alt={`Ilustração oficial de ${name}`} />
             </figure>
           </header>

           {/* NAV das abas: 3 botões, 1 classe ativa por vez */}
           <nav className="modal-tabs-nav" aria-label="Seções da ficha">
             <button
               className={`tab-btn ${activeTab === 'about' ? 'active' : ''}`}
               onClick={() => setActiveTab('about')}
             >
               Sobre
             </button>
             <button
               className={`tab-btn ${activeTab === 'stats' ? 'active' : ''}`}
               onClick={() => setActiveTab('stats')}
             >
               Estatísticas
             </button>
             <button
               className={`tab-btn ${activeTab === 'moves' ? 'active' : ''}`}
               onClick={() => setActiveTab('moves')}
             >
               Golpes
             </button>
           </nav>

           {/* PAINÉIS: cada && só mostra o seu quando é o escolhido */}
           <main className="modal-tab-content">
             {activeTab === 'about' && (
               <div className="tab-pane">
                 <ul className="modal-types">
                   {types.map((tipo) => (
                     <li key={tipo} className={`type-badge type-${tipo.toLowerCase()}`}>{tipo}</li>
                   ))}
                 </ul>
                 <p><strong>Altura:</strong> {height} m</p>
                 <p><strong>Peso:</strong> {weight} kg</p>
                 <p><strong>Habilidades:</strong> {abilities.join(', ')}</p>
               </div>
             )}

             {activeTab === 'stats' && (
               <div className="tab-pane">
                 {barrasDeStats.map(({ rotulo, valor }) => (
                   <div key={rotulo} className="stat-line">
                     <span className="stat-label">{rotulo}</span>
                     <div className="stat-track">
                       <div
                         className="stat-fill"
                         style={{ width: `${(valor / 180) * 100}%` }}
                       ></div>
                     </div>
                     <span className="stat-value">{valor}</span>
                   </div>
                 ))}
               </div>
             )}

             {activeTab === 'moves' && (
               <div className="tab-pane moves-grid">
                 {moves.map((move) => (
                   <span key={move} className="move-pill">{move}</span>
                 ))}
               </div>
             )}
           </main>
         </div>
       </div>
     );
   }
   ```

2. **Adicione os estilos das abas ao FINAL do `src/PokemonModal.css`:**
   ```css
   /* NAV de abas */
   .modal-tabs-nav {
     display: flex;
     border-bottom: 2px solid #e2e8f0;
     margin-top: 0.5rem;
   }

   .tab-btn {
     flex: 1;
     padding: 0.8rem 0.5rem;
     border: none;
     background: transparent;
     font-weight: 600;
     font-size: 0.9rem;
     color: #64748b;
     cursor: pointer;
     transition: color 0.15s;
   }

   .tab-btn:hover { color: #0f172a; }

   /* O ternário do JSX liga esta classe em quem for a aba escolhida */
   .tab-btn.active {
     color: #dc2626;
     box-shadow: inset 0 -3px 0 #dc2626;
   }

   .modal-tab-content { padding: 1.25rem 1.5rem; color: #334155; }
   .tab-pane p { margin: 0.5rem 0; }
   .tab-pane .modal-types { padding: 0 0 1rem; }

   /* Barras de estatísticas */
   .stat-line {
     display: grid;
     grid-template-columns: 80px 1fr 36px;
     align-items: center;
     gap: 0.5rem;
     margin: 0.4rem 0;
     font-size: 0.85rem;
   }

   .stat-track {
     background: #e2e8f0;
     border-radius: 999px;
     height: 8px;
     overflow: hidden;
   }

   .stat-fill {
     height: 100%;
     background: linear-gradient(90deg, #fbbf24, #dc2626);
     border-radius: 999px;
     transition: width 0.4s ease;
   }

   .stat-value { text-align: right; font-weight: 700; }

   /* Pílulas de golpes */
   .moves-grid {
     display: flex;
     flex-wrap: wrap;
     gap: 0.4rem;
   }

   .move-pill {
     background: #f1f5f9;
     border: 1px solid #cbd5e1;
     border-radius: 999px;
     padding: 0.25rem 0.7rem;
     font-size: 0.75rem;
     color: #334155;
   }
   ```

> [!IMPORTANT]
> **Duas decisões de projeto embutidas no código** (você as defende na prova):
> 1. `moves.slice(0, 20)` no Step 09a: a API devolve 40+ golpes; 20 é amostra limpa e performática.
> 2. `key={rotulo}` e `key={move}`: a `key` vem do DADO (Regra de Ouro do Step 05), nunca do `index`.

---

### 🧪 5. Teste de Validação

1. Abra a aplicação e clique em um Pokémon com status alto (ex: **Charizard**).
2. Clique na aba **"Estatísticas"**: as 6 barras aparecem com larguras proporcionais aos valores (Ataque do Charizard longo, HP médio...).
3. Clique na aba **"Golpes"**: as pílulas com os 20 primeiros golpes; **nenhuma seção de aba some** na troca — só os painéis mudam.
4. Confirme o "esquecimento honesto": feche o modal (✖), reabra — a aba volta para **"Sobre"** (unmount destruiu o `activeTab`).
5. Passe de aba MUITO rápido e confira que o banner colorido não "pisca" (só o `<main>` interno re-renderiza).
6. Console limpo: sem warnings de `key`.

---

### ❓ 6. Quiz de Fixação (6 Questões de Múltipla Escolha)

#### Q1. Como criamos o controle de navegação por abas em um componente React?
- (A) Um arquivo `.html` diferente para cada aba.
- (B) Um estado `const [activeTab, setActiveTab] = useState('nomeDaAba')` alterado pelos botões.
- (C) Recarregando a página com `window.location.reload()`.
- (D) A tag `<section tab="true">`.

> **Gabarito Comentado:** **(B)** O estado guarda QUAL painel está visível; os botões apenas trocam esse valor e o React redesenha.

#### Q2. O que faz `{activeTab === 'stats' && <div className="tab-pane">...</div>}`?
- (A) Desenha todas as abas e esconde com CSS.
- (B) Desenha o painel de estatísticas apenas quando `activeTab` vale `'stats'`.
- (C) Exclui a aba stats do código.
- (D) Cria um novo estado.

> **Gabarito Comentado:** **(B)** Com `&&`, condição falsa (`'about' !== 'stats'`) derruba o lado direito e o React não desenha nada.

#### Q3. Qual a vantagem do padrão Tabs para a experiência do usuário (UX)?
- (A) Aumenta o tamanho da tela.
- (B) Organiza grandes volumes de dados em seções focadas, sem rolagem excessiva.
- (C) Oculta os dados permanentemente.
- (D) Deixa o site mais lento.

> **Gabarito Comentado:** **(B)** Abas dividem o conteúdo em contextos, reduzindo a sobrecarga visual e a rolagem.

#### Q4. Como acendemos a classe CSS apenas no botão da aba selecionada?
- (A) `className="tab-btn active"`
- (B) `className={`tab-btn ${activeTab === 'about' ? 'active' : ''}`}`
- (C) `class={activeTab}`
- (D) `style="active"`

> **Gabarito Comentado:** **(B)** Template string + ternário ligam/desligam a classe conforme o estado — o mesmo padrão do card shiny.

#### Q5. Por que limitamos os golpes com `.slice(0, 20)` ao mapear a API?
- (A) Porque a PokéAPI cobra por golpe.
- (B) Para evitar renderizar centenas de itens e poluir a interface, mantendo uma amostra limpa.
- (C) Porque o React não aceita mais de 20 itens.
- (D) Porque Pokémon aprende só 1 golpe.

> **Gabarito Comentado:** **(B)** `.slice(0, 20)` corta o array nos primeiros 20 elementos — performance e legibilidade.

#### Q6. Fechamos o modal e, ao reabrir, ele volta na aba "Sobre". Por quê?
- (A) Porque o navegador reinicia o site.
- (B) Porque fechar remove o componente da tela (unmount) e destrói seus estados; ao reabrir, o `useState('about')` recomeça.
- (C) Porque `activeTab` tem memória cacheada.
- (D) Porque o `.slice()` zera as abas.

> **Gabarito Comentado:** **(B)** O ciclo de vida do componente define o estado: "fora da tela" = "sem memória". É o que garante ficha sempre limpa.

---

### 📝 7. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Padrão Tabs UI em React com useState, renderização condicional em série com &&, classes dinâmicas de estado ativo, estilos inline calculados (barras de estatísticas em porcentagem), anti-repetição com arrays e .map() e ciclo de vida de componentes (unmount zerando estado)."*
