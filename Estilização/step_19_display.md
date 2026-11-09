# Workshop: Estilo da Livraria

## Step 19 — `display`: quem ocupa a linha, quem divide a linha

---

### 📖 Teoria

`display` responde a uma pergunta só: **como esta caixa participa do layout?**

| Valor | Comportamento | `width`? |
|---|---|---|
| `block` | ganha **linha própria**; preenche a largura do pai | ✅ |
| `inline` | flui junto do texto, como palavra | ❌ ignorado |
| `inline-block` | flui na linha, mas é caixa respeitada | ✅ |
| `none` | **some** do layout: não existe, não ocupa espaço | — |

Seus `div`, `p`, `h1` e `h2` são `block` por fábrica. Seus `<button>` são `inline-block` — e é por isso que os dois botões do rodapé já ficam lado a lado, sem você pedir.

**As três formas de esconder não são sinônimos:**

```css
display: none;       /* some da página; os vizinhos sobem */
visibility: hidden;  /* invisível, mas o buraco fica */
opacity: 0;          /* transparente, ocupa espaço, AINDA CLICÁVEL */
```

`opacity: 0` num botão é bug de acessibilidade: o usuário vê nada, mas o Tab chega lá e o clique funciona.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.selo       { display: inline-block; }  /* quadradinho dentro da frase */
.destaque   { display: inline; }        /* palavra: width não vale */
```

---

### ✍️ Mão na massa

1. No DevTools (Computed), leia o `display` de `h1`, `p`, `div.card` e `button`. Anote os quatro.
2. Nos `.btn`, aplique `display: block`. Os quatro botões empilharam, um por linha? Volte ao padrão.
3. **Esconda um cartão:** `display: none` no `.card` do Dave. A prateleira ficou com **um** livro e o rodapé subiu.
4. Troque por `opacity: 0`. O cartão sumiu da vista, mas o **espaço ficou** — e aperte Tab até o botão invisível: ele ainda recebe foco. Conserte com `display: none` e depois **remova a regra**.

> Margem vertical em elemento `inline` não empurra a linha. Se `margin-bottom` num `<span>` não afastou nada, não é bug seu.

---

### ✅ Critérios de verificação do Step 19

- [ ] Você leu e anotou o `display` efetivo de quatro elementos
- [ ] Diferenciou na tela `display: none` de `opacity: 0`
- [ ] Identificou o risco de acessibilidade do `opacity: 0` em elemento interativo
- [ ] Nenhuma regra de `display` sobreviveu no arquivo final

### 🧠 Antes de avançar

1. Por que `width: 200px` num elemento `inline` é ignorado?
2. Que vícios os botões `inline-block` carregam que um layout de verdade precisa curar?
