# Workshop: Página de Livraria

## Step 8 — Dentro do container: o primeiro cartão

---

### 📖 Teoria

Containers podem **conter outros containers** — é assim que documentos reais ganham profundidade:

```
div.card-container ──→ "a prateleira toda"
└── div.card       ──→ "um livro em cima da prateleira"
```

Este step cria o **primeiro cartão de livro**: um `<div>` novo, **filho** da sua `card-container`, com a class `card`.

Por que a mesma class `card` em todos os cartões que virão?

- `card-container` = **um** (a área que agrupa).
- `card` = **repetido** (cada membro do grupo). É o padrão "container plural no nome, item no singular" que você verá em todo código HTML/CSS: `list`/`item`, `gallery`/`photo`, `card-container`/`card`.
- Nomear cada cartão com a class comum é o que depois permite, num único lugar, dizer "todos os `.card` têm moldura e sombra" — sem CSS ainda, funciona como **documentação viva** da estrutura.

Hierarquia esperada do seu body no fim deste step:

```
body
├── h1   "XYZ Bookstore"
├── p    "Browse our collection..."
└── div.card-container
    └── div.card        ← novo, vazio por ora
```

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<div class="playlist">
  <div class="faixa"></div>
  <div class="faixa"></div>
</div>
```

Uma playlist (única) nomeada no plural conceitual, N faixas com a mesma class — a "prateleira" e seus "discos".

---

### ✍️ Mão na massa

1. Dentro do `<div class="card-container">`, **antes** do `</div>` que o fecha, crie um novo `<div>`.
2. Dê a ele a class `card`.
3. Indente o filho em relação ao pai (2 a 4 espaços). Seus olhos são o primeiro validador de aninhamento.
4. DevTools (F12): expanda o nó `div.card-container` — o `div.card` deve estar **aninhado dentro**, não como irmão.

> Se o `card` apareceu *depois* do `</div class="card-container">`, você fechou a container cedo demais: mova o fechamento para o fim.

---

### ✅ Critérios de verificação do Step 8

- [ ] Existe um `<div class="card">` dentro do `<div class="card-container">`
- [ ] O cartão usa exatamente a class `card`
- [ ] A indentação no arquivo reflete o aninhamento real

### 🧠 Antes de avançar

1. Por que o cartão não pode ficar como **irmão** da `card-container`?
2. Quando você adicionar o segundo livro, o que muda e o que se repete na estrutura?
