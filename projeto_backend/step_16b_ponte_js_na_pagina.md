# Workshop: API da XYZ Bookstore

## Step 16b — PONTE: o JavaScript da página (antes de falar com a API)

---

### 📖 Teoria

Você passou 16 steps escrevendo JS que roda **no terminal** (Node). A partir do Step 18, o JS vai rodar **no navegador**, e lá o mundo é outro: em vez de `req`/`res`, os personagens são os **elementos da tela**. Quatro verbos cobrem 95% do JS de página:

| Verbo | Ferramenta | Lê-se |
|-------|-----------|-------|
| **ACHAR** | `document.querySelector(".card")` | "me dê o PRIMEIRO elemento que bater nesse seletor CSS" |
| **MUDAR** | `el.textContent = "oi"` / `el.innerHTML = "<b>oi</b>"` | escrever texto (seguro) ou HTML (com moderação) no elemento |
| **OUVIR** | `el.addEventListener("click", fn)` | "executa `fn` quando algo acontecer neste elemento" — você **registra**, não chama |
| **GERAR** | `array.map((x) => \`<li>${x}</li>\`).join("")` | dados → string de HTML, o músculo que o Step 18 usa pra montar cards |

**Ligar o script na página** (o `projeto2` nunca precisou, agora precisa):

```html
  <script src="script.js"></script>
</body>
```

Antes do `</body>`, **sempre**. Motivo mecânico: quando o `<script>` aparece, o navegador PARA de ler o HTML e executa ele ali. Script no `<head>` = `querySelector` procurando elementos que ainda não existem = `null` na cara (`Cannot read properties of null`). É o erro mais comum de quem começa — reconheça-o quando aparecer.

`textContent` × `innerHTML`: o primeiro escreve texto puro (um `<script>` digitado vira texto inofensivo); o segundo interpreta HTML (útil pra gerar cards, perigoso com dado de fora — o Step 18 trata disso).

**O clique que vem de elementos que ainda não existem** — conceito que o Step 19 exige e derruba todo iniciante:

```javascript
container.addEventListener("click", (evento) => {
  const btn = evento.target.closest(".buy-now"); // quem foi clicado (ou o pai dele)
  if (!btn) return;                               // clique não foi num botão: ignora
  // trabalha com btn.dataset.id
});
```

Listener no **container** (que existe desde sempre), decidindo no clique **quem** foi atingido (`evento.target`). Isso se chama **delegação de eventos**, e resolve a armadilha do `innerHTML`: elementos recriados perdem listeners individuais; o container, nunca. Um listener, infinitos botões.

`el.dataset.id` = o `data-id="..."` que você pôs na tag. Toda `data-xxx` vira propriedade de `el.dataset` — o jeito profissional de carregar informação (o `id` do livro) **dentro** do elemento, pronta no clique.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Uma página de padaria com dados **locais** (sem servidor — é ensaio): lista de pães, botão de pedido por delegação, contador reagindo:

```javascript
// dados locais, o "catalogo" do passo 2 vem igualzinho, so a fonte muda
const paes = [
  { id: "frances", nome: "Pão francês", preco: 1.5 },
  { id: "integral", nome: "Pão integral", preco: 4.0 },
];

// GERAR: array -> HTML (template string com crases: ${} embute valores)
const lista = document.querySelector("#lista");
lista.innerHTML = paes
  .map((p) => `<li>${p.nome} — R$ ${p.preco.toFixed(2)} <button class="pedir" data-id="${p.id}">Pedir</button></li>`)
  .join("");

// OUVIR com delegação + MUDAR o contador
let total = 0;
const contador = document.querySelector("#contador");
lista.addEventListener("click", (evento) => {
  const btn = evento.target.closest(".pedir");
  if (!btn) return;
  total++;
  contador.textContent = `Pedidos: ${total}`;
  console.log("pedido registrado:", btn.dataset.id); // abra o F12 e VEJA isso acontecer
});
```

```html
<p id="contador">Pedidos: 0</p>
<ul id="lista"></ul>
<script src="script.js"></script>
```

Quatro frases que resumem o exemplo: os `<li>` **não existem no HTML** — nasceram do `map`; `data-id` no botão → `btn.dataset.id` no clique; o listener vive no `<ul>` pai, não nos `<li>`; `console.log` é o `stdout` do navegador — a janela é o **Console do DevTools** (F12), não o terminal.

---

### ✍️ Mão na massa

Monte `ponte/index.html` + `ponte/script.js` (qualquer pasta, só treino):

1. **ACHAR:** HTML com `<h1 id="titulo">XYZ</h1>` e `<p id="status">...</p>`; no script, mude o `textContent` dos dois. Abra pelo VS Code (Live Server) e confirme na tela.
2. **GERAR:** cole o array `livros` do seu `app.js` (3 livros, mesmos dados — ensaio geral do Step 18) no `script.js`; renderize com `map` + template string dentro de um `<ul>`: cada `<li>` com `titulo`, `R$ ${preco}` e `<button class="buy-now" data-id="${l.id}">Buy Now</button>`.
3. **OUVIR:** com delegação, clique em qualquer Buy Now → `console.log("clicou:", btn.dataset.id)` e atualize o `#status` para `"Último clicado: <id>"`.
4. **Provoque os dois erros clássicos e aprenda o rosto deles:** (a) mova o `<script>` para o `<head>` e leia o erro de `null`; (b) troque `closest(".buy-now")` por nada (use `evento.target` cru) e clique no texto do `<li>` — por que quebrou? Devolva, conserte.
5. Teste de fogo: clique Buy Now de 2 livros diferentes — o `#status` sempre mostra o último, **sem duplicar** a contagem quando você adicionar `total++`? (Se duplicou, você tem listener por botão em algum lugar — caça e extingue.)
6. Guarde a pasta `ponte/`: ela é **exatamente** o Step 18, só que com o catálogo no script em vez de no `fetch`. Trocar `const livros = [...]` por `await fetch(...)` é a única diferença — você vai sentir esse alívio no próximo step.

---

### ✅ Critérios de verificação do Step 16b

- [ ] Script ligado antes do `</body>` e a página abre **sem erro no console** (F12 aberto — hábito, não opção)
- [ ] Os `<li>` dos 3 livros existem na tela mas **não** existem no HTML-fonte (nasceram do `map`)
- [ ] Um clique em qualquer botão produz o `console.log` com o `dataset.id` correto
- [ ] Delegação comprovada: depois de re-renderizar (chamar o render de novo), o clique **ainda funciona** sem registrar novo listener
- [ ] Você viu, de propósito, o erro do `null` (script no head) e sabe nomear a causa

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. `querySelector` devolve o elemento ou uma lista? Qual ferramenta dá a lista toda, e por que o container-pai dispensa ela aqui?
2. Por que `textContent = "<b>oi</b>"` mostra `<b>` na tela e `innerHTML` mostra **oi** em negrito? Qual usa com dado do usuário?
3. `addEventListener` executa ou registra? Onde está a prova disso no seu código (quem executa, afinal?).
4. O `#status` foi atualizado por dentro de uma função que você nunca chamou. Quem a chamou?
