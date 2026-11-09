# Workshop: Estilo da Livraria

## Step 25 — `:focus-visible`: o anel que ninguém deve tirar

---

### 📖 Teoria

No Step 12 de HTML você apertou **Tab** até o botão e ele aceitou o Enter. O navegador ainda mostra um **anel** quando isso acontece — e o erro clássico é removê-lo.

**Nunca tire o indicador de foco sem pôr outro.** Ele é o único guia de quem navega sem mouse.

A correção é trocar a roupa, não sumir com a roupa:

```css
.btn:focus-visible {
  outline: 3px solid hsl(210 90% 45%);
  outline-offset: 2px;
}
```

**`:focus-visible`, não `:focus`.** Com `:focus`, o **clique do mouse** também liga o anel — e todo mundo acha feio, e remove. Com `:focus-visible`, o navegador só mostra o anel quando o foco veio **do teclado**.

**`outline`, não `border`.** `border` **ocupa espaço**: quando o foco chega, o botão cresce e a página dá um pulo. `outline` é desenhado **por fora, sem afetar a caixa** — o pulo não acontece.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.campo:focus-visible {
  outline: 3px solid hsl(210 90% 45%);
  outline-offset: 2px;
}
```

Um formulário de checkout: o anel diz "esta é a caixa que você está digitando" sem mover nada ao redor.

---

### ✍️ Mão na massa

1. Aperte **Tab** até um botão e veja o anel de fábrica.
2. Escreva `.btn:focus-visible` com `outline` de `3px` e `outline-offset`. O anel virou seu.
3. **Prove a diferença:** troque `outline` por `border` no mesmo lugar. Aperte Tab e observe a página **pular**. Volte ao `outline`.
4. Teste `:focus` (sem `-visible`) **clicando** com o mouse: o anel aparece onde você não queria. Troque de volta.

> O DevTools mostra quais pseudo-classes estão ativas agora, no selo **`:hov`** do painel Styles. Use-o para conferir em vez de adivinhar.

---

### ✅ Critérios de verificação do Step 25

- [ ] `.btn:focus-visible` existe, com `outline` (não `border`)
- [ ] O anel aparece no Tab e **não** aparece no clique do mouse
- [ ] Nada pula no layout quando o foco chega
- [ ] O anel de fábrica não foi removido sem substituto

### 🧠 Antes de avançar

1. Por que `outline` não provoca pulo e `border` provoca?
2. Quem é prejudicado quando você escreve `outline: none` e nada mais?
