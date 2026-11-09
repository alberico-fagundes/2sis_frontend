# Workshop: Estilo da Livraria

## Step 20 — Flexbox I: a fila que obedece

---

### 📖 Teoria

`display: flex` numa container converte ela **e os filhos** para um sistema novo. Duas coisas mudam na hora: os vãos estranhos entre os botões `inline-block` somem, e os filhos passam a obedecer a **dois eixos**.

```
flex-direction: row       eixo principal  ──────────►
                          eixo transversal ▼
```

| Eixo | Mandam nele | Pergunta que respondem |
|---|---|---|
| **principal** | `justify-content` | como distribuir o espaço **ao longo** da fila? |
| **transversal** | `align-items` | como alinhar **em cruz** dentro da faixa? |

Os valores de `justify-content` que você vai usar:

| Valor | Efeito |
|---|---|
| `center` | agrupa no meio |
| `space-between` | **pontas coladas às bordas**, vãos iguais no meio |
| `flex-start` / `flex-end` | encosta numa ponta |

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.esteira {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

A esteira do caixa de supermercado: o primeiro produto na ponta esquerda, o último na direita, sem calcular nada.

---

### ✍️ Mão na massa

1. Na `.btn-container`, escreva `display: flex`.
2. Recarregue: os vãos entre os dois botões sumiram e eles ficaram lado a lado, alinhados de verdade.
3. Acrescente `justify-content: center`. Os dois pararam no meio da página?
4. Troque para `space-between`: o "View Cart" colou na esquerda e o "Checkout" na direita. É a barra de checkout que o Step 18 de HTML prometeu.
5. **Devolva para `center`** — o `space-between` volta no Step 30, só em tela larga.

> `justify-content` não centraliza item sozinho na transversal, e `align-items` não move item ao longo da fila. Se o botão insiste em não centrar, você aplicou no eixo errado.

---

### ✅ Critérios de verificação do Step 20

- [ ] `.btn-container` é `display: flex` com `justify-content: center`
- [ ] Os vãos de espaço em branco entre botões sumiram
- [ ] Você testou `space-between` e desfez
- [ ] O estado final do arquivo tem `center`, não `space-between`

### 🧠 Antes de avançar

1. Por que os botões `inline-block` tinham vão entre si e os flex não?
2. Que pergunta o `justify-content` responde que o `text-align` não respondia?
