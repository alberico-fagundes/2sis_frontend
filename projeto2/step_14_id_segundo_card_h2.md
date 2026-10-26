# Workshop: Página de Livraria

## Step 14 — Identidade do segundo cartão: `id` + `<h2>`

---

### 📖 Teoria

Aqui os dois conceitos do workshop se encontram na mesma tag:

```html
<div class="card" id="dave-cooking-book">
```

- `class="card"` → **tipo**: "sou um cartão de livro como os outros".
- `id="dave-cooking-book"` → **indivíduo**: "sou *este* livro específico".

É exatamente o par uniforme + matrícula do Step 9. O id do segundo cartão **precisa ser diferente** — dois `id="..."` iguais é duplicação proibida. Foi por isso que o Step 13 criou o cartão sem id: a duplicata só pode existir entre elementos que se distinguem por outro atributo.

Por que o nome é `dave-cooking-book` e não `card2`? Mesma lição do Sally: id nomeia **o conteúdo apontado**, não a posição. Se a livraria reordenar os livros, `#dave-cooking-book` continua sendo verdade; `#card2` pode passar a apontar para outro livro.

Anatomia do título: `h2` filho do novo card, como no primeiro cartão — o nível **2** indica "item de uma seção", independentemente de ser o livro 1º ou 50º. (Não existe `h3` "porque é o segundo cartão": nível vem da hierarquia de assunto, não da ordem de criação.)

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<div class="faixa" id="bohemian-rhapsody">
  <h3>Bohemian Rhapsody</h3>
</div>
<div class="faixa" id="we-will-rock-you">
  <h3>We Will Rock You</h3>
</div>
```

Mesmo tipo (faixa), identidades únicas, título interno de mesmo nível.

---

### ✍️ Mão na massa

1. No segundo `<div class="card">`, adicione o atributo `id` com o valor exato `dave-cooking-book`.
2. Dentro desse cartão, como primeiro filho, crie um `<h2>` com o texto exato: `Dave's Cooking Adventure` (apóstrofo em `Dave's`).
3. Ctrl+F por `id="` — deve listar agora **dois** valores diferentes. E pelo título: um `h2` por cartão, nenhum solto fora dos cards.
4. DevTools: expanda `div.card-container` e confira os dois filhos `div.card` cada um com seu `h2`.

> Lembrete de simetria: o que você fez no cartão da Sally, repita estruturalmente no do Dave — *mesmo esqueleto, outro conteúdo*. Padrão de card existe para exatamente isso.

---

### ✅ Critérios de verificação do Step 14

- [ ] O segundo card tem `id="dave-cooking-book"` (único na página)
- [ ] Existe `<h2>Dave's Cooking Adventure</h2>` dentro desse card
- [ ] Nenhum id se repete; nenhum `h2` ficou fora de um card

### 🧠 Antes de avançar

1. Você linkaria `index.html#sally-adventure-book` vs `#dave-cooking-book` — o que cada um faria na tela?
2. Escreva de memória a árvore inteira do `<body>` até aqui, com classes e ids.
