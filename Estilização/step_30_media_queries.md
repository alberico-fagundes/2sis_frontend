# Workshop: Estilo da Livraria

## Step 30 — Media queries: o último refinamento

---

### 📖 Teoria

O Step 23 já fez a prateleira quebrar sozinha, sem media query. Isso não é redundância: é a diferença entre layout que o **conteúdo** resolve e decisão que é **sua**.

```css
@media (min-width: 40rem) {
  .btn-container { flex-direction: row; justify-content: space-between; }
}
```

Um bloco `@media` **não cria especificidade**: lá dentro, as regras competem normalmente e a **última escrita vence** (Step 18). Por isso o bloco fica **depois** das regras base que ele ajusta.

**Mobile-first:** escreva o estreito como base e use `min-width` para **acrescentar** quando há espaço. O caminho contrário (`max-width`, desmontar) é onde os bugs moram.

**Breakpoint não se inventa, se descobre:** arraste a largura no DevTools de 320px para cima e pare no instante em que algo ficar **feio** — linha de texto longa demais, botão espremido, texto colado na borda. Esse instante é o seu breakpoint. Arredonde e escreva em **`rem`**, não `px`: `48rem` respeita a preferência de fonte do usuário (Step 11).

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.acoes { display: flex; flex-direction: column; gap: 0.75rem; }

@media (min-width: 40rem) {
  .acoes { flex-direction: row; justify-content: space-between; }
}
```

A fila do caixa: apertada no corredor estreito, aberta em leque no salão largo. Mesma regra, duas camadas.

---

### ✍️ Mão na massa

1. Confirme a base em 320px (modo dispositivo): tudo empilhado, legível, sem transbordamento horizontal.
2. Arraste a largura devagar e **anote o pixel** em que os dois botões do rodapé cabem lado a lado sem aperto. Esse é o seu primeiro breakpoint.
3. Escreva o bloco `@media (min-width: <valor em rem>)` com `flex-direction: row` e `justify-content: space-between` na `.btn-container` — a barra de checkout do Step 18 de HTML, agora condicional.
4. **Prove a ordem:** mova o bloco para **acima** das regras base e veja o refinamento parar de funcionar. Devolva ao fim.

> Se o conteúdo nunca quebra, você não precisa de breakpoint nenhum — e um `@media` inventado é pior que nenhum.

---

### ✅ Critérios de verificação do Step 30

- [ ] A base é legível em 320px **sem** nenhuma media query
- [ ] O bloco `@media` usa `min-width`, em `rem`, e está **depois** das regras base
- [ ] O breakpoint foi derivado de um problema observado, não inventado
- [ ] Nenhuma media query altera contraste, indicador de foco ou semântica

---

### 🏁 Fim do workshop

A livraria tem as duas metades: **estrutura** (o trio `div` / `class` / `id` do workshop de HTML) e **apresentação** (seletores, caixa, tipografia, layout, estado, tema, responsividade). E o que **não** mudou pelo caminho: nenhum `<h2>` virou `<h1>`, nenhum `<button>` virou `<div>`, nenhum id foi duplicado. A regra que atravessa os dois workshops é uma só — **aparência é negociável, semântica não**.

Capa, preço, autor, web fonts, animações e JavaScript ficam para os módulos seguintes.

### 🧠 Encerramento — responda sem olhar o código

1. Desenhe de memória a caixa (conteúdo → padding → border → margin) e diga o que `box-sizing: border-box` muda nessa conta.
2. Um colega removeu o `outline` dos botões "porque fica feio". Qual é o argumento **medível** contra isso?
3. Por que `auto-fit` com `minmax` dispensa media query, e que decisão você ainda toma manualmente?
