# Workshop: Estilo da Livraria

## Step 5 — Herança: o que pinga para dentro dos filhos

---

### 📖 Teoria

Algumas propriedades escorrem do elemento para **dentro** dos filhos; outras param na caixa onde foram declaradas.

| Herda | Não herda |
|---|---|
| `color` | `border` |
| `font-family` | `margin` |
| `line-height` | `width` |
| `text-align` | `padding` |

As que herdam são as de **texto** — uma frase não decide sozinha a cor das próprias palavras. As que não herdam são as de **caixa**: se `border` herdasse, um `<div>` com borda contornaria os 40 filhos dele.

Declare no `<body>` e a página inteira obedece. Com uma exceção que você já construiu e talvez não tenha notado: **declaração local vence herança**. O que já tem regra própria não muda.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
body {
  background-color: hsl(40 30% 94%);
  color: hsl(220 15% 20%);
}
```

O site de uma padaria pinta o papel inteiro de uma vez, sem repetir a cor em cada parágrafo.

---

### ✍️ Mão na massa

1. Escreva uma regra de `body` com `background-color` e `color`.
2. Recarregue: o fundo da página inteira mudou.
3. Olhe com atenção: **alguns textos não mudaram de cor.** Quais? Os que você já pintou nos Steps 2 e 3. A herança só fala onde ninguém gritou.
4. Acrescente `text-align: center` ao `body` e veja o efeito pingar para baixo. Desfaça.

> Se a página inteira mudou de uma vez, você viu herança. Se nada mudou, procure a declaração fora do bloco ou um `;` faltando.

---

### ✅ Critérios de verificação do Step 5

- [ ] `body` tem `background-color` e `color` declarados
- [ ] Você identificou quais elementos **não** herdaram a cor, e por quê
- [ ] O fundo da página inteira mudou com uma só declaração
- [ ] `text-align` foi testado e desfeito

### 🧠 Antes de avançar

1. Por que `border` não herda e `color` herda?
2. Se você aplicar `font-family` só no `<h1>`, os `<h2>` herdam dele ou do `<body>`?
