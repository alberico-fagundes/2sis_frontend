# Workshop: Página de Livraria

## Step 16 — Sinopse do segundo cartão: `<p>`

---

### 📖 Teoria

Nada de conceito novo — e esse é o ponto. Este step existe para você **repetir o padrão** do Step 11 num cartão diferente, sem consultar: título (`h2`) → sinopse (`p`) → (ação vem no próximo). Quando a estrutura é a mesma e o que muda é só o texto, o HTML deixa de ser sintaxe e passa a ser **reflexo** — é assim que se constrói páginas com 200 cards sem escrever 200 arquiteturas.

Anatomia de ficha (lembrete):

```
div.card#dave-cooking-book
├── h2   "Dave's Cooking Adventure"   ← O QUE é
├── p    sinopse                       ← POR que importar  ← este step
└── button.btn                         ← AÇÃO              ← step 17
```

A sinopse do Dave tem uma particularidade divertida: é um *twister* — "pancakes to pasta, one recipe at a time". Isso não muda o HTML, mas reforça a lição do Step 11: o `<p>` guarda texto corrido; listas de ingredientes de verdade mereceriam outro elemento (você verá `<ul>`/`<li>` em breve).

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<div class="prato-card">
  <h2>Massa da Casa</h2>
  <p>Espaguete fresco, do trigo ao prato, feito à mão a cada pedido.</p>
</div>
```

---

### ✍️ Mão na massa

1. Dentro do `div.card#dave-cooking-book`, **abaixo** do `<h2>` do Dave, crie um `<p>`.
2. Texto exato: `This is the story of Dave as he learns to cook everything from pancakes to pasta, one recipe at a time.`
3. Não esqueça o `.` final nem as vírgulas — o texto é comparado literal.
4. DevTools: o `p` deve ser filho do cartão do Dave, entre o `h2` e o fim do `</div>`.

> Se o parágrafo apareceu no meio do cartão da Sally, você está com um `</div>` de fechamento faltando (ou sobrando) no primeiro cartão — feche os olhos e conte os `div` abertos antes de colocar o próximo.

---

### ✅ Critérios de verificação do Step 16

- [ ] `<p>` com a sinopse do Dave existe e está dentro do `#dave-cooking-book`
- [ ] Está após o `<h2>`, antes do fechamento do card
- [ ] Os dois cartões agora têm `h2` + `p` na mesma ordem interna

### 🧠 Antes de avançar

1. Que elementos faltam no cartão do Dave para ele ficar simétrico ao da Sally?
2. Por que o texto da sinopse não pode ir dentro do `h2` com um `<br>`?
