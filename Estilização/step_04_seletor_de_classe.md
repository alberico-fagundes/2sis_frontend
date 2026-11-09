# Workshop: Estilo da Livraria

## Step 4 — Seletor de classe: o rótulo que vira consulta

---

### 📖 Teoria

No HTML, `class` é um **atributo**. No CSS, `.nome` é uma **consulta**: "encontre quem estiver com esse rótulo vestido". O ponto não é decoração — é o que separa classe de tag.

```css
.card { background-color: white; }
```

É a colheita de duas promessas do workshop de HTML. O Step 13 disse que *uma* regra `.card` vestiria os dois cartões; o Step 17 disse que *uma* regra `.btn` vestiria os botões ao mesmo tempo. Chegou a hora de pagar as duas.

E note o que a class faz que a tag não faz: `.btn` alcança os **quatro** botões sem tocar em nenhum `<p>`, porque pergunta **a que grupo você pertence**, não **que tag você é**.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.playlist { padding: 1rem; }
.faixa    { color: #333; }
```

Uma playlist (única) e N faixas: container no nome coletivo, item no nome do membro.

---

### ✍️ Mão na massa

1. Escreva `.card` com uma cor de **fundo** diferente da página.
2. Escreva `.btn` com uma cor de fundo e uma de texto.
3. Recarregue e conte: **dois** cartões e **quatro** botões mudaram — com duas regras. É o "CSS em série" que o HTML prometeu.
4. Acrescente uma terceira class a um dos cartões no HTML (ex.: `class="card destaque"`) e estilize `.destaque`. Duas classes convivem no mesmo atributo, separadas por **espaço**.

> Com espaço no CSS (`.card .destaque`) significa outra coisa: descendência. Sem espaço (`.card.destaque`) significa "o mesmo elemento tem as duas". É o erro de digitação mais caro do CSS.

---

### ✅ Critérios de verificação do Step 4

- [ ] Existe regra `.card` afetando os dois cartões
- [ ] Existe regra `.btn` afetando os quatro botões
- [ ] Você testou duas classes no mesmo elemento
- [ ] Nenhuma class da livraria descreve conteúdo (ex.: `.sally`) — só papéis

### 🧠 Antes de avançar

1. Se amanhã você adicionar um terceiro livro, o que precisa escrever no CSS para ele nascer estilizado?
2. Por que a class se repete e o `id` do HTML não podia?
