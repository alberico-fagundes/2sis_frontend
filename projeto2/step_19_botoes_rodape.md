# Workshop: Página de Livraria

## Step 19 — Os dois botões finais: `id` + `class` de novo, lado a lado

---

### 📖 Teoria

Este step fecha a página e é, de propósito, um **exame disfarçado**: cada botão exige tudo o que o workshop ensinou, na mesma tag:

```html
<button id="view-cart-btn" class="btn">View Cart</button>
```

- `id` único → porque cada botão **faz uma coisa diferente**: um leva ao carrinho, outro fecha a compra. Ação individual ⇒ identidade individual (e, mais tarde, JavaScript que os distingue exatamente por id).
- `class="btn"` repetida → porque os dois **pertencem à mesma família visual** (botões de navegação), e quando o CSS chegar, uma regra os veste em conjunto — como acontece com os "Buy Now".

Note o padrão dos ids: `view-cart-btn` / `checkout-btn` — o **sufixo `-btn`** denuncia o papel do elemento no nome. Nomes que se explicam ("o botão de ver o carrinho") sobrevivem à manutenção; `btn1`/`btn2` não.

A página completa conta agora:

| Elementos | Quantos | ids | classes |
|---|---|---|---|
| botões | 4 (`btn` em todos) | 2 com id (rodapé) | `btn` ×4 |
| cards | 2 | 2 únicos | `card` ×2 |
| containers | 2 | nenhum | `card-container`, `btn-container` |

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<div class="acoes">
  <button id="salvar-rascunho-btn" class="btn">Salvar rascunho</button>
  <button id="publicar-btn" class="btn">Publicar</button>
</div>
```

---

### ✍️ Mão na massa

1. Dentro do `div.btn-container`, crie o **primeiro** `<button>`:
   - id: `view-cart-btn` · class: `btn` · texto: `View Cart`
2. Crie o **segundo** botão, como irmão do primeiro (mesmo nível, mesma container):
   - id: `checkout-btn` · class: `btn` · texto: `Checkout`
3. Ordem importa: View Cart antes de Checkout — a sequência do funil de compra.
4. Conferência final (o "build" passou?):

```bash
# sem ferramentas, com o que você já tem no navegador:
# Ctrl+F no fonte: 2 ids novos, 4 buttons, 4 "btn"
# DevTools: btn-container com exatamente 2 filhos <button>
```

> **Congratulations!** A estrutura da livraria está pronta: `div` para agrupar, `class` para nomear tipos, `id` para nomear indivíduos — o trio exato do objetivo do workshop. O que falta (estilo, imagens, livros novos) pertence aos módulos seguintes.

---

### ✅ Critérios de verificação do Step 19

- [ ] `<button id="view-cart-btn" class="btn">View Cart</button>` dentro da `btn-container`
- [ ] `<button id="checkout-btn" class="btn">Checkout</button>` dentro da `btn-container`, após o View Cart
- [ ] Os dois ids são únicos; os dois compartilham `class="btn"`
- [ ] Documento completo sem tags órfãs (todo `</div>`/`</button>` fecha o que abriu)

### 🧠 Encerramento — responda sem olhar o código

1. Desenhe de memória a árvore do `<body>`: quantos níveis de container, quais classes em cada nó.
2. Dê um exemplo de situação em que você usaria `id` e não `class` — e o inverso.
3. Por que "Buy Now" dos cards não recebeu id, mas os botões do rodapé receberam?
