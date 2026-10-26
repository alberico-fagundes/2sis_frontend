# Workshop: Página de Livraria

## Step 18 — Fora dos cards: rodapé de ações e `btn-container`

---

### 📖 Teoria

Até aqui, **tudo** vivia dentro do `<body>` sob a forma: letreiro → boas-vindas → prateleira. Agora a página ganha um **rodapé de navegação**, e uma nova regra estrutural aparece:

> Elementos que não pertencem a um livro ficam **irmãos** da `card-container` — não dentro dela.

```
body
├── h1 / p              (topo)
├── div.card-container  (prateleira)
├── p                   (frase de rodapé)   ← este step
└── div.btn-container   (botões de rodapé)  ← este step
```

Lembre da sintaxe que o enunciado repete:

```html
<element attribute="value">
    inner text
</element>
```

- O `<p>` do rodapé **tem conteúdo** (texto).
- O `<div class="btn-container">` é só **esqueleto** por ora: vazio, esperando os dois botões do próximo step.
- A class segue o padrão container-do-step-7: `btn-container` agrupa, `btn` (próximo step) rotula os membros. Mesma dupla semântica *plural-único* de `card-container`/`card`.

Por que uma container só para botões, se a página já é uma container? Porque o rodapé terá **vida própria de estilo**: quando o CSS chegar, `.btn-container` pode centralizar os botões, criar a barra de checkout, espaçá-los — sem tocar nos botões "Buy Now" dos cards. Containers existem para **delimitar unidades de estilo**, e unidades de estilo nascem de unidades de intenção.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<body>
  <h1>Cardápio</h1>
  <div class="pratos">
    <div class="prato">Pizza</div>
  </div>
  <p>Pronto para fechar o pedido?</p>
  <div class="acoes"></div>
</body>
```

---

### ✍️ Mão na massa

1. **Depois** do `</div>` que fecha a `card-container` (e ainda dentro do `<body>`), crie um `<p>` com o texto exato: `Review your selections and continue to checkout.`
2. Abaixo dele, crie um `<div>` com class `btn-container` — vazio, ou com um comentário HTML indicando que ele aguarda os botões de navegação.
3. A armadilha do step: o `p` e o `div` novos devem estar **fora** da `card-container`. No DevTools, `div.card-container` deve ter exatamente **2 filhos** (os cards) — se o novo `p` apareceu dentro, você fechou a container depois de hora.
4. Recarregue: a frase do rodapé aparece abaixo dos dois cartões.

---

### ✅ Critérios de verificação do Step 18

- [ ] `<p>` "Review your selections and continue to checkout." existe, como filho do body, após a card-container
- [ ] `<div class="btn-container">` existe abaixo desse `<p>`
- [ ] Nenhum dos dois está aninhado dentro da `card-container`

### 🧠 Antes de avançar

1. Por que um `<p>` de rodapé não pode ficar dentro da `card-container` mesmo "parecendo texto solto"?
2. Que nomes de class você reutilizaria para centralizar só os botões do rodapé?
