# Workshop: Estilo da Livraria

## Step 6 — `padding`: o respiro dentro da caixa

---

### 📖 Teoria

Todo elemento é uma caixa retangular, e o `padding` é o espaço **dentro** dela — entre o conteúdo e a borda.

```
┌──────── borda ────────┐
│  ┌───── padding ─────┐ │
│  │                    │ │
│  │      CONTEÚDO      │ │
│  │                    │ │
│  └────────────────────┘ │
└─────────────────────────┘
```

A propriedade que decide a aparência aqui: **o fundo cobre o padding**. Um cartão branco com `padding: 1rem` tem 1rem de branco entre a borda e o texto. É isso que faz o card respirar em vez de apertar as letras contra a parede.

```css
padding: 1rem;              /* os quatro lados */
padding: 1rem 2rem;         /* vertical | horizontal */
```

Dois valores é o formato mais comum em cartões: menos respiro em cima e embaixo, mais nas laterais.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.quadro {
  padding: 1.25rem;
  background: #fff;
}
```

O `passe-partout` de um quadro emoldurado: o papel branco que separa a obra da moldura. Ninguém o confunde com a moldura, e é exatamente essa a distinção entre padding e borda.

---

### ✍️ Mão na massa

1. Na regra `.card` do Step 4, acrescente `padding` com dois valores (vertical menor, horizontal maior).
2. Recarregue: o texto parou de grudar na borda e o fundo branco acompanhou o respiro.
3. Troque um dos valores por `0` e veja o texto colar de novo. Conserte.
4. Acrescente o mesmo `padding` à regra `.btn`. Os botões deixaram de ser estreitos.

> Se o cartão parece ter uma faixa branca **antes** da borda, você aplicou margem onde queria padding. O fundo nunca cobre margem — isso é o próximo step.

---

### ✅ Critérios de verificação do Step 6

- [ ] `.card` tem `padding` declarado
- [ ] O texto do cartão não encosta na borda na tela
- [ ] `.btn` tem `padding` próprio
- [ ] Você observou o fundo cobrindo o padding

### 🧠 Antes de avançar

1. Por que o `background` aparece atrás do padding e nunca atrás da margem?
2. Qual é a diferença prática entre `padding: 1rem` e `padding: 1rem 2rem`?
