# Workshop: Estilo da Livraria

## Step 21 — Flexbox II: o vão e a travessa

---

### 📖 Teoria

**`gap`** é o espaçamento **entre** os itens da fila:

```css
.btn-container { gap: 1rem; }
```

Ele substitui a gambiarra velha de dar margem no filho e anular a última com `:last-child`:

```css
/* antes */ .item { margin-right: 1rem; } .item:last-child { margin-right: 0; }
/* agora */ .container { gap: 1rem; }
```

`gap` **não é margem**: não colapsa, não aparece fora do primeiro nem do último item, e funciona também em Grid.

**`align-items`** cuida do eixo transversal. O padrão é `stretch` (esticar os filhos para igualar a altura) — e é por isso que, sem você fazer nada, dois cartões de sinopses diferentes ficam com **alturas iguais**. `center` alinha pelo centro em vez de esticar.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.prateleira { display: flex; gap: 1.5rem; align-items: center; }
```

Uma prateleira de discos: o vão entre as capas é igual em todos os pontos, e as de altura diferente ficam centradas na travessa, não penduradas pelo topo.

---

### ✍️ Mão na massa

1. Na `.btn-container`, acrescente `gap: 1rem`.
2. Meça no DevTools o vão: é exatamente `1rem`, e **não** há espaço fora do primeiro nem do último botão.
3. Acrescente `align-items: center`. Confira que botões de alturas diferentes ficam centrados entre si, e não alinhados pela linha de base do texto.
4. **Sinta o que o `gap` substituiu:** dê `margin-right: 1rem` a um `.btn` e veja o vão dobrar no lado direito. **Remova a margem** — o `gap` já fazia o serviço.

> Se você der `gap` **e** margem nos filhos, soma os dois respiros. É o erro mais comum quando se migra de margem para gap.

---

### ✅ Critérios de verificação do Step 21

- [ ] `.btn-container` tem `gap` e `align-items` declarados
- [ ] Nenhuma margem de espaçamento sobreviveu nos `.btn`
- [ ] Você mediu o vão no DevTools e confirmou que é o valor do `gap`
- [ ] Botões de alturas diferentes aparecem centrados, não na base

### 🧠 Antes de avançar

1. Por que `gap` é mais honesto que `margin` para espaçar irmãos?
2. O que aconteceria com os dois cartões da prateleira se você tirasse o `align-items: stretch` implícito?
