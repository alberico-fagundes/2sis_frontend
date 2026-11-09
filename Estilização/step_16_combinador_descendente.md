# Workshop: Estilo da Livraria

## Step 16 — `.card p`: o seletor que pergunta onde você mora

---

### 📖 Teoria

O Step 3 deixou uma dívida: `p` alcança os **quatro** parágrafos, e você só queria mexer nas sinopses. A ferramenta é o **combinador descendente** — um espaço entre dois seletores:

```css
.card p { color: hsl(220 10% 40%); }
/*  ↑  ↑                                   */
/*  onde mora  o que é                      */
```

Lê-se: "todo `<p>` que esteja **dentro** de um `.card`". Na sua livraria, são exatamente **dois** — as sinopses. As boas-vindas e o rodapé ficam intactos, porque moram fora.

| Escreve | Alcança |
|---|---|
| `p` | 4 parágrafos |
| `.card p` | 2 — só as sinopses |
| `.btn` | 4 botões |
| `button.btn` | 4 botões, declarando que são botões |

É a diferença entre perguntar *"que tag você é?"* e *"onde você mora?"*. A segunda é a que distingue papéis numa página cuja camada de texto não tem nome — e é por isso que este step existe.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.item            { padding: 1rem; }
.item .descricao { font-size: 0.9rem; }
```

Uma cafeteria: o prato e a descrição dele. A segunda regra não toca o nome do prato nem o rodapé do cardápio.

---

### ✍️ Mão na massa

1. Escreva `.card p` com uma cor **diferente** da do `p` geral, e um tamanho de fonte um degrau abaixo.
2. Recarregue e confira na tela: só as **duas sinopses** mudaram. As boas-vindas e o rodapé não.
3. No DevTools, passe o ponteiro sobre um `<p>` de sinopse e veja as **duas** regras competindo — a de `p` e a de `.card p` — com a vencedora em cima.
4. Troque `.card p` por `.card .p` (com ponto no `p`). Sumiu tudo: você passou a procurar uma **classe** chamada "p", que não existe. Conserte.

> O espaço é o operador. `.card p` é descendência; `.cardp` é outra palavra; `.card.p` é "o mesmo elemento tem as duas". Três caracteres, três sentidos.

---

### ✅ Critérios de verificação do Step 16

- [ ] Existe regra `.card p` atingindo **somente** as duas sinopses
- [ ] As boas-vindas e o rodapé conservam a cor e o tamanho do `p` geral
- [ ] Você viu as duas regras concorrentes no painel Styles do DevTools
- [ ] O teste do `.card .p` foi feito e desfeito

### 🧠 Antes de avançar

1. Por que `.card p` é mais frágil que `.card > p` (filho direto)?
2. Que outra propriedade você aplicaria em `.card p` e não em `p`?
