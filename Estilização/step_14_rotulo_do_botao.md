# Workshop: Estilo da Livraria

## Step 14 — O rótulo do botão: maiúscula, ar e peso

---

### 📖 Teoria

Três propriedades transformam "Buy Now" de texto em **rótulo de botão**:

| Propriedade | O que faz |
|---|---|
| `text-transform: uppercase` | força maiúsculas |
| `letter-spacing: 0.08em` | espaço **entre letras** |
| `font-weight: 700` | engrossa o traço |

Elas andam juntas por um motivo físico: **maiúscula miúda precisa de ar**. Sem `letter-spacing`, as capitulares se tocam e o rótulo vira mancha. Repare em qualquer aplicativo: botões em maiúscula têm espaço entre letras, e é deliberado.

O sinal importa:

- **positivo** (`0.08em`) — rótulos pequenos, etiquetas, maiúsculas
- **negativo** (`-0.01em`) — títulos grandes, onde as letras já se abraçam demais

`text-transform` muda o que aparece **na tela**, não o que está no arquivo: quem copia o texto leva o original. Por isso ele é seguro — e por isso não substitui escrever direito.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.cartao-creditos {
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 0.12em;
}
```

Os créditos de um filme: letra miúda, maiúscula, muito ar. A mesma receita do seu botão.

---

### ✍️ Mão na massa

1. Na regra `.btn`, acrescente as três propriedades.
2. Recarregue: os **quatro** botões mudaram de uma vez — é o `.btn` pagando a promessa do Step 4.
3. No `<h1>`, aplique `letter-spacing` **negativo** (`-0.01em`). O letreiro se fechou e ganhou densidade.
4. Tire o `letter-spacing` do botão mantendo a maiúscula. O rótulo virou mancha. Devolva.

> `text-align: center` no botão alinha o **texto dentro** dele. Não centra o botão na página — isso é trabalho do Step 20.

---

### ✅ Critérios de verificação do Step 14

- [ ] `.btn` tem `text-transform`, `letter-spacing` e `font-weight`
- [ ] Os quatro botões mudaram juntos, com uma regra
- [ ] O `<h1>` usa `letter-spacing` de sinal **contrário** ao dos botões
- [ ] Você comparou o rótulo com e sem o espaço entre letras

### 🧠 Antes de avançar

1. Por que maiúscula miúda pede espaço positivo e título grande pede negativo?
2. O que `text-transform` muda no arquivo, e o que muda só na tela?
