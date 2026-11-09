# Workshop: Estilo da Livraria

## Step 3 — Seletor de elemento: o alto-falante fala com todo mundo

---

### 📖 Teoria

O seletor mais simples é **o nome da tag**. Ele varre o documento inteiro e encontra **todos** os elementos daquele tipo, sem perguntar se você queria.

| Escreve | Pega na sua livraria |
|---|---|
| `h2` | os títulos dos dois livros |
| `p` | boas-vindas + 2 sinopses + rodapé = **4** |
| `button` | 2 "Buy Now" + View Cart + Checkout = **4** |

Guarde a contagem: ela é o ponto do step. O seletor de elemento responde *"que tag você é?"* — e não *"o que você representa?"*. Por isso ele não distingue a sinopse do Dave da frase de boas-vindas: para ele, são os dois `<p>`.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
h2 { font-style: italic; }
p  { color: #444; }
```

O site de um cinema põe os títulos das sessões em itálico. Todos. Sem exceção.

---

### ✍️ Mão na massa

1. Escreva uma regra de `h2` com uma cor e um peso de fonte.
2. Escreva uma regra de `p` com outra cor.
3. Recarregue e **conte quantos parágrafos mudaram**. Não são dois — são quatro: as sinopses, as boas-vindas e o rodapé foram juntos.
4. Esse efeito colateral é o problema que o próximo step resolve.

> Se `p { font-size: ... }` fosse a ferramenta certa para encolher só as sinopses, o Step 16 não existiria.

---

### ✅ Critérios de verificação do Step 3

- [ ] Existe regra de `h2` afetando os dois títulos de livro
- [ ] Existe regra de `p`
- [ ] Você contou **4** parágrafos atingidos, não 2
- [ ] As duas regras usam `;` entre declarações

### 🧠 Antes de avançar

1. Quantos `<button>` o seletor alcança, e quantos papéis diferentes eles exercem?
2. O que o seletor de elemento **não consegue expressar** sobre um elemento?
