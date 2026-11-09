# Workshop: Estilo da Livraria

## Step 7 — `border` e `border-radius`: a moldura prometida

---

### 📖 Teoria

`border` é a linha que contorna a caixa. São **três** partes num shorthand só:

```css
border: 2px solid hsl(220 15% 60%);
/*      ↑      ↑     ↑                                    */
/*   largura estilo  cor                                    */
```

**`solid` não é opcional.** Sem estilo de linha, a borda tem largura zero e desaparece — e o navegador não avisa. É o motivo nº 1 de "minha borda não aparece".

`border-radius` arredonda os cantos, e arredonda **fundo e borda juntos**:

```css
border-radius: 0.5rem;
```

Um valor só arredonda tudo. `999px` em botão produz pílula — o formato que você vê em todo aplicativo moderno.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.quadro {
  border: 3px solid #2b2b2b;
  border-radius: 2px;
}
```

A moldura do quadro na galeria. Repare que a moldura **não** empurra o quadro para longe da parede: ela faz parte dele.

---

### ✍️ Mão na massa

1. Na regra `.card`, acrescente `border` com as três partes.
2. Recarregue: os dois cartões ganharam contorno de uma vez — é o `.card` trabalhando.
3. Acrescente `border-radius`. Confira na tela que a **borda** e o **fundo** arredondam juntos, não só o fundo.
4. Na regra `.btn`, acrescente `border: none` e `border-radius: 999px`. Os botões perderam o visual de fábrica e viraram pílula.

> Se a borda não aparecer, procure o estilo de linha faltando antes de suspeitar de qualquer outra coisa.

---

### ✅ Critérios de verificação do Step 7

- [ ] `.card` tem `border` com largura, estilo e cor
- [ ] `.card` tem `border-radius`
- [ ] Os botões perderam a borda do navegador e ganharam cantos arredondados
- [ ] Os dois cartões e os quatro botões mudaram com duas regras

### 🧠 Antes de avançar

1. O que acontece se você escrever `border: 2px hsl(0 0% 50%)`, sem o `solid`?
2. Por que `border: none` nos botões é uma decisão e não preguiça?
