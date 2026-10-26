# Workshop: Página de Livraria

## Step 17 — Botão do segundo cartão e a força das classes compartilhadas

---

### 📖 Teoria

`<button class="btn">Buy Now</button>` de novo — e agora acontece a **mágica declarada** do Step 12: dois elementos distintos, rotulados igual.

> "Both button elements now share the same class, which means they can be styled consistently together."

Traduzindo para o que o CSS fará mais adiante: uma única regra `.btn { background: #0a0; ... }` vestirá **os dois botões ao mesmo tempo**. É por isso que o nome da class é genérico (`btn`, "botão") e não específico (`buy-now-sally-btn`): classes descrevem **papéis**, não conteúdos. Papel igual ⇒ uniforme igual ⇒ estilo igual, em um único lugar.

Essa é a espinha dorsal do pensamento CSS/fCC:

1. Estruture com elementos (o que é)
2. Agrupe com `div` + `class` (a que conjunto pertence)
3. Identifique com `id` (quem, individualmente)
4. Estilize **mirando classes** (como o conjunto aparece) — nunca por id, a menos que seja realmente único.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<div class="prato-card">
  <button class="btn">Adicionar ao pedido</button>
</div>
<div class="prato-card">
  <button class="btn">Adicionar ao pedido</button>
</div>
```

---

### ✍️ Mão na massa

1. Dentro do `div.card#dave-cooking-book`, **abaixo** do `<p>` da sinopse, crie um `<button>`.
2. Class: `btn`. Texto: `Buy Now`.
3. Ctrl+F por `class="btn"`: **dois** resultados, um por cartão.
4. Recarregue e confira os dois botões com o mesmo "visual de fábrica" do navegador — é o gostinho do que a class fará quando houver CSS: consistência sem repetição de trabalho.

> O botão da página agora é o único texto em **inglês duplicado** de verdade — e é exatamente por isso que funciona: "Buy Now" é uma ação, não um conteúdo; ações repetem, informações não.

---

### ✅ Critérios de verificação do Step 17

- [ ] `<button class="btn">Buy Now</button>` existe dentro do `#dave-cooking-book`
- [ ] É o último filho do cartão, abaixo do `<p>`
- [ ] Existem dois `.btn` e eles são irmãos estruturais (mesma posição nos dois cards)

### 🧠 Antes de avançar

1. Se amanhã você quiser um botão "Wishlist" diferente do "Buy Now", que class ele levaria — `btn`? outra? as duas?
2. Por que o estilo por class escala melhor que estilo por id em cards?
