# Workshop: Estilo da Livraria

## Step 9 — `margin` e `max-width`: a livraria no centro da tela

---

### 📖 Teoria

`margin` é o espaço **fora** da caixa — e, ao contrário do padding, **o fundo não cobre**. É transparência: mostra o que está atrás.

Duas propriedades trabalham juntas para dar forma à página:

| Propriedade | O que faz |
|---|---|
| `max-width: 60rem` | teto: a linha de texto cresce até aqui e para |
| `margin: 0 auto` | sobrou espaço horizontal? divida igual dos dois lados |

**`max-width` existe por legibilidade.** O WCAG recomenda **65 a 75 caracteres** por linha: acima disso o olho perde a linha ao voltar. Um `<body>` que ocupa a tela inteira num monitor de 27 polegadas passa de 150.

**`auto` só tem o que dividir se a caixa for menor que o continente** — por isso as duas propriedades são um par, nunca uma só. Sem `max-width`, o `auto` não centra nada.

E note o que **não** centra: `text-align` alinha o **texto dentro** da caixa; `margin: 0 auto` alinha a **caixa** na tela. São perguntas diferentes.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.lote {
  max-width: 30rem;
  margin: 0 auto;
}
```

Um lote centrado na rua: a largura é limitada de propósito, e o que sobra da rua divide-se igual dos dois lados.

---

### ✍️ Mão na massa

1. Na regra `body`, acrescente `max-width: 60rem`.
2. Recarregue em tela larga: o texto parou de correr de ponta a ponta — mas está **colado à esquerda**. Ainda falta uma.
3. Acrescente `margin: 0 auto`. Agora a livraria inteira parou no centro.
4. Reduza a janela devagar até o texto ficar ilegível em linha longa, e veja que o `max-width` é o que impede esse cenário de acontecer em tela grande.

> `margin: 0 auto` não centra elemento **inline** nem caixa sem largura definida. Se não funcionar, o problema é um desses dois — não a sintaxe.

---

### ✅ Critérios de verificação do Step 9

- [ ] `body` tem `max-width` e `margin: 0 auto`
- [ ] A livraria está centralizada na tela larga
- [ ] Você observou que o texto para de crescer antes da borda da janela
- [ ] Nenhum `width` fixo em `px` foi usado no `body`

### 🧠 Antes de avançar

1. Por que `width: 60rem` quebra no celular e `max-width: 60rem` não?
2. Que propriedade centra o **texto** dentro de um cartão, e qual centra o **cartão** na página?
