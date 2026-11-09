# Workshop: Estilo da Livraria

## Step 26 — `transform` e `transition`: o botão que flutua

---

### 📖 Teoria

`transform` desloca a caixa **sem afetar o layout**:

```css
transform: translateY(-3px) scale(1.02);
```

Um botão que sobe 3px com `translateY` deixa o vizinho exatamente onde estava. O mesmo botão com `margin-top: -3px` arrastaria a fila inteira. É a diferença entre **ilusão** de movimento e **recálculo** de página.

`transition` interpola entre dois estados. Sem ela, o `:hover` do Step 24 é um **corte** — muda num frame. Com ela, desliza:

```css
.btn {
  transition: transform 180ms ease-out, background-color 180ms ease-out;
}
```

Quatro partes: `propriedade | duração | função | atraso`.

| Regra | Valor |
|---|---|
| o que animar | **só** `transform` e `opacity` — rodam na GPU, sem recalcular layout |
| duração | **120 a 250ms** — acima de 400ms o usuário percebe espera, não polimento |
| função | `ease-out` para entrada e hover |

A `transition` vai na regra **base** (`.btn`), não no `:hover` — senão a ida desliza e a volta corta.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.vaga        { transition: transform 160ms ease-out; }
.vaga:hover  { transform: translateY(-2px); }
```

O cartão de embarque que levanta da mesa sob o ponteiro, sem empurrar o vizinho.

---

### ✍️ Mão na massa

1. No `.btn:hover` do Step 24, acrescente `transform: translateY(-2px)`.
2. Na base `.btn`, escreva `transition: transform 180ms ease-out, background-color 180ms ease-out`.
3. Passe o ponteiro: o botão levanta e escurece **suavemente**.
4. **Comprove que nada empurra:** observe o cartão vizinho durante o hover. Ele se mexeu? Não. Agora troque `transform` por `margin-top: -2px` e veja a fila pular. **Volte ao `transform`.**

> Anime `width`, `height` ou `margin` e o navegador recalcula a página a cada frame: 60fps viram 15. `transform` e `opacity` não recalculam nada.

---

### ✅ Critérios de verificação do Step 26

- [ ] `.btn:hover` usa `transform`, não `margin` nem `top`
- [ ] A `transition` está na regra **base**, e lista propriedades específicas (não `all`)
- [ ] Duração entre 120ms e 250ms
- [ ] Você comprovou na tela que o vizinho não se move durante a elevação

### 🧠 Antes de avançar

1. Por que `transition` no `:hover` em vez da base quebra a volta?
2. O que `transition: all 200ms` pode animar sem você querer?
