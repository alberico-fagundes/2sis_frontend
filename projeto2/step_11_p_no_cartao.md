# Workshop: Página de Livraria

## Step 11 — Descrição do livro: `<p>` no cartão

---

### 📖 Teoria

Todo card de produto — livro, filme, pizza — tem as mesmas três camadas:

```
card
├── título       (h2)   ← O QUE é
├── descrição    (p)    ← POR QUE importar   ← este step
└── (ação/meta)         ← preço, botão, autor (steps seguintes)
```

O `<p>` aqui é a **sinopse**: a frase que convence o cliente. Novamente, o conteúdo manda, não a aparência — um parágrafo dentro do cartão pertence **àquele** livro (filho do `div.card`), assim como o `h2` pertencia.

Posição: **depois** do `<h2>` — título e sinopse seguem a ordem natural de leitura (ficha de catálogo, contracapa de livro, card de app: sempre nome → explicação).

O que a máquina lê com isso:

```
h1 → h2 → p      =  "livro X, sobre Y"
```

Leitores de tela navegam nessa escada pulando heading por heading; a sinopse vem colada ao título do item, não solta na página.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<div class="prato-card">
  <h2>Pizza Margherita</h2>
  <p>Molho de tomate, mussarela de búfala e manjericão fresco.</p>
</div>
```

Nome, depois "por que pedir" — a mesma anatomia do cartão de livro.

---

### ✍️ Mão na massa

1. Dentro do `div.card#sally-adventure-book`, **abaixo** do `<h2>`, crie um parágrafo.
2. Texto exato: `This is an epic story of Sally and her dog Rex as they navigate through other worlds.`
3. Confira os três fechamentos que agora precisam casar em cascata: `</p>` → `</h2>` não (ele já fechou) — mas sim `</p>`, depois `</div>` do card, depois `</div>` do container.
4. Recarregue: o bloco "XYZ Bookstore / Browse our collection… / Sally's SciFi Adventure / This is an epic story…" deve aparecer na ordem de leitura, tudo alinhado à esquerda (sem CSS, o recuo do código não afeta a tela — estrutura ≠ indentação).

> Erro frequente: fechar o `</p>` fora do `</div>` do cartão. DevTools é o juiz: se o parágrafo apareceu como filho do container em vez do card, a tag de fechamento do `<p>` ou do `div` está deslocada.

---

### ✅ Critérios de verificação do Step 11

- [ ] `<p>` com o texto da sinopse existe dentro do `div.card`
- [ ] Está após o `<h2>`, antes do `</div>` do card
- [ ] Árvore do DevTools: `div.card` contém `h2` **e** `p` como filhos diretos

### 🧠 Antes de avançar

1. Por que a sinopse vai dentro do cartão em vez de um `<p>` só lá no topo, com todos os textos?
2. Cite a ordem dos elementos do seu documento até agora, do `<body>` para dentro.
