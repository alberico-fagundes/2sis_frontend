# Workshop: Estilo da Livraria

## Step 23 — `auto-fit` + `minmax`: a prateleira que se vira sozinha

---

### 📖 Teoria

O Step 22 deixou a prateleira ilegível em janela estreita. A cura cabe em uma linha:

```css
grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
/*                            ↑                    ↑        ↑     */
/*                     quantas couberem       piso  teto     */
```

Lê-se: "crie **tantas** colunas de no mínimo 250px e no máximo uma fração igual, quantas couberem na largura". Janela larga → 2, 3, 4 colunas. Janela estreita → 1. **Sem media query, sem breakpoint, sem cálculo seu.**

| Parte | O que faz |
|---|---|
| `minmax(250px, 1fr)` | piso de 250px, cresce dividindo o resto |
| `auto-fit` | colunas vazias **somem** e as existentes esticam |
| `auto-fill` | colunas vazias **ficam**, ocupando espaço |

`auto-fit` é o que você quer para cards. `auto-fill` é para grade decorativa, tabuleiro.

É a diferença entre layout que **você** decide por faixa de tela e layout que o **conteúdo** resolve sozinho.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.galeria { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 1rem; }
```

Uma galeria de fotos: num celular, uma por linha; num monitor, seis. A regra é **uma**, e ninguém contou telas.

---

### ✍️ Mão na massa

1. Na `.card-container`, troque `repeat(2, 1fr)` por `repeat(auto-fit, minmax(250px, 1fr))`.
2. Recarregue em tela larga: mesma coisa de antes. Nenhuma surpresa — ótimo.
3. **Arraste a largura da janela devagar.** Em algum ponto o segundo cartão **desce** para a linha de baixo, sozinho, e volta a ficar inteiro. É o piso de 250px falando.
4. Adicione um **terceiro** `<div class="card">` ao HTML, com título, sinopse e botão seus. Ele entrou na fila sem você escrever **uma linha de CSS**. Depois **remova** o card extra.

> Se a quebra não acontecer, procure `minmax()` faltando: com `repeat(auto-fit, 1fr)` você escreveu uma coluna só, sempre.

---

### ✅ Critérios de verificação do Step 23

- [ ] `.card-container` usa `repeat(auto-fit, minmax(250px, 1fr))`
- [ ] Reduzir a janela derruba para 1 coluna **sem nenhuma media query**
- [ ] Um terceiro card de teste entrou na prateleira sem CSS novo
- [ ] O card extra foi removido do HTML

### 🧠 Antes de avançar

1. Que número você escolheu como piso, e o que acontece se você baixar para 120px?
2. Por que `auto-fit` e não `auto-fill` para cards?
