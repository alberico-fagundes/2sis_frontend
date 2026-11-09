# Workshop: Estilo da Livraria

## Step 8 — `box-shadow`: o cartão que flutua

---

### 📖 Teoria

`box-shadow` desenha uma projeção **sem ocupar espaço**: não empurra vizinho, não aumenta a caixa.

```css
box-shadow: 0 4px 12px hsl(220 30% 20% / 0.12);
/*         ↑ ↑    ↑    ↑                                        */
/*    x  y  blur  cor com alfa                                  */
```

| Parte | O que faz |
|---|---|
| `x` | desloca para os lados (0 = centrada) |
| `y` | desloca para baixo (positivo = luz vinda de cima) |
| `blur` | difumina — quanto maior, mais longe o objeto "flutua" |
| `/ 0.12` | alfa: a transparência da sombra |

A sombra honesta de cartão: **y positivo, blur médio, alfa baixo** (0.08 a 0.18). Sombra preta opaca com blur enorme não é elevação — é carimbo sujo.

O alfa é o que faz a sombra funcionar sobre **qualquer** fundo. Uma sombra sólida denuncia o retângulo onde foi desenhada.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.vaga {
  box-shadow: 0 6px 18px rgb(0 0 0 / 0.18);
}
```

Um cartão de embarque sobre a mesa: a sombra diz ao olho que ele está **acima** do papel, sem que ninguém precise tocar nele.

---

### ✍️ Mão na massa

1. Na regra `.card`, acrescente `box-shadow` com `y` de `4px`, blur de `12px` e alfa de `0.12`.
2. Recarregue: os dois cartões se destacaram do fundo **sem borda nenhuma** — teste apagando a borda do Step 7 e vendo que a sombra segura o cartão.
3. Compare duas versões na tela: alfa `0.12` com blur `12px`, e alfa `0.6` com blur `30px`. A segunda parece suja. **Apague a segunda.**
4. Devolva a borda e deixe as duas conviverem: borda define o limite, sombra define a altura.

> Sombra não ocupa espaço no layout. Se o cartão de baixo não desceu quando você pôs a sombra, não é bug — é a propriedade funcionando.

---

### ✅ Critérios de verificação do Step 8

- [ ] `.card` tem `box-shadow` com as quatro partes
- [ ] Os cartões parecem elevados, não carimbados
- [ ] Você comparou as duas sombras e ficou com a de alfa discreto
- [ ] A sombra sobrevive sem borda (testado)

### 🧠 Antes de avançar

1. Por que a sombra com alfa funciona sobre fundo colorido e a sombra preta sólida não?
2. Se `box-shadow` não ocupa espaço, o que acontece com o vizinho de baixo quando você aumenta o blur?
