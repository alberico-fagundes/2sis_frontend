# Workshop: Estilo da Livraria

## Step 22 — Grid: a prateleira em duas dimensões

---

### 📖 Teoria

Flexbox é **unidimensional**: uma fila. Ele não sabe o que acontece na linha de baixo. Grid é **bidimensional** — você declara colunas, e o navegador respeita.

```css
.card-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
}
```

**`1fr`** é "uma fração do espaço **livre**" — não é porcentagem: divide o que sobra **depois** do `gap`. `repeat(2, 1fr)` são duas metades iguais; `2fr 1fr` dá ao primeiro o dobro.

A diferença prática que você vai ver na tela:

| | Flex | Grid |
|---|---|---|
| itens lado a lado | ✅ | ✅ |
| **alinhados em coluna** com os da linha de baixo | ❌ | ✅ |
| alturas iguais | `align-items: stretch` | já é da célula |

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.mesa  { display: grid; grid-template-columns: 2fr 1fr; gap: 1rem; }
.azulejo { display: grid; grid-template-columns: repeat(4, 1fr); gap: 4px; }
```

A mesa do banquete (prato grande, sobremesa pequena) e o azulejo da parede (grade regular). Duas perguntas diferentes, duas respostas do Grid.

---

### ✍️ Mão na massa

1. Na `.card-container`, troque `display: flex` por `display: grid` e declare `grid-template-columns: repeat(2, 1fr)`. Mantenha o `gap`.
2. Recarregue: os dois cartões dividiram a linha em metades exatas.
3. Meça no DevTools a largura dos dois: são **iguais**, e as bordas direitas alinham numa coluna vertical — o que o Flex não garantia.
4. Reduza a janela: os dois **afinam juntos** até ficarem ilegíveis. O Grid respeita a grade que você mandou — e é exatamente isso que o próximo step cura.

> Grid não substitui Flex: resolve outra pergunta. O rodapé de dois botões continua melhor em Flex.

---

### ✅ Critérios de verificação do Step 22

- [ ] `.card-container` é `display: grid` com `grid-template-columns` e `gap`
- [ ] Os dois cartões dividem a linha em partes iguais
- [ ] Você mediu no DevTools que as larguras são idênticas
- [ ] `.btn-container` continua Flex (não foi migrada por impulso)

### 🧠 Antes de avançar

1. Por que `1fr` não é `100%`? O que o `gap` tem a ver com isso?
2. Que critério decide se um pedaço da página é Flex ou Grid?
