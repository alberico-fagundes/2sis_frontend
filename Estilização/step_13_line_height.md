# Workshop: Estilo da Livraria

## Step 13 — `line-height`: o respiro entre as linhas

---

### 📖 Teoria

`line-height` é a altura de cada linha de texto. Sem ele, as linhas se amontoam e o olho cansa em dois parágrafos.

```css
line-height: 1.6;     ← número nu: 1,6 × a fonte DESTE elemento
line-height: 1.6em;   ← resolvido aqui e herdado PRONTO
```

**Use número nu.** A diferença aparece no aninhamento: com número nu, o filho calcula a própria linha sobre a própria fonte; com `em`, ele herda o valor **já resolvido** do pai e fica com linha alta demais para a letra pequena.

Medidas honestas:

| Onde | Valor |
|---|---|
| texto corrido | **1.5 a 1.7** |
| títulos grandes | **1.1 a 1.3** |

Quanto **maior** a fonte, **menos** respiro a linha precisa — o título de `2.5rem` com `line-height: 1.6` ocupa meia tela de ar.

`line-height` **herda**, então declare no `body` e corrija nos títulos.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.legenda       { line-height: 1.6; }
.titulo-grande { font-size: 3rem; line-height: 1.1; }
```

A legenda de um documentário respira; o título do episódio, não. Mesma página, dois pesos.

---

### ✍️ Mão na massa

1. No `body`, acrescente `line-height: 1.6`.
2. Recarregue: os quatro parágrafos respiraram — e os **títulos também**, porque herança não discrimina.
3. Corrija o excesso: dê a `h1` e `h2` um `line-height` de `1.2`. Os títulos apertaram e o corpo continuou folgado.
4. Leia no DevTools (Computed) o valor resolvido de `line-height` de um `<h2>` e de um `<p>`: são números diferentes, multiplicados das fontes diferentes.

> Se o texto ficou com ar de folhetim — muito espaço entre linhas — você passou de 1.8. Volte a 1.6.

---

### ✅ Critérios de verificação do Step 13

- [ ] `body` usa `line-height` com **número nu**
- [ ] `h1` e `h2` têm `line-height` próprio, menor que o do corpo
- [ ] Você leu os valores resolvidos no painel Computed
- [ ] Nenhum texto corrido está abaixo de 1.5

### 🧠 Antes de avançar

1. Por que número nu escala com o filho e `em` não?
2. Por que o título grande precisa de **menos** respiro que o parágrafo pequeno?
