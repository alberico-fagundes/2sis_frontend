# Workshop: Página de Livraria

## Step 9 — O atributo `id`: identidade única

---

### 📖 Teoria

Se `class` é o **uniforme do grupo**, `id` é o **nome civil** do elemento: um identificador **exclusivo**, que só pode aparecer **uma vez** na página.

| | `class` | `id` |
|---|---|---|
| Unicidade | Pode se repetir à vontade | **Uma vez por página** — duplicar é erro |
| Quantidade por elemento | Várias (`class="card novo"`) | Só um (`id="..."`) |
| Uso típico | Estilizar grupos, rotas de navegação (`#âncora`) | Referenciar **aquele** elemento específico: âncora, `<label for>`, `getElementById` |

Regras do valor do `id`:

- **Sem espaços** — `sally adventure book` quebra o atributo em pedaços.
- Só letras, dígitos, `_` e `-` — na prática, `kebab-case` em minúsculas: `sally-adventure-book`.
- Não pode começar com número nem com hífen; sem acentos.

Por que `sally-adventure-book` e não `book1`? Bons ids nomeiam **a identidade do que apontam** (livro da Sally), não a posição. Se amanhã a ordem dos cartões mudar, `book1` mente; o nome verdadeiro não.

Formato, como no exemplo oficial:

```html
<p id="para">example paragraph</p>
```

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<div class="faixa">
  <h3>Bohemian Rhapsody</h3>
</div>
<!-- outra faixa, MESMA class, OUTRO id -->
<div class="faixa" id="we-will-rock-you">
  <h3>We Will Rock You</h3>
</div>
```

Duas faixas com o mesmo uniforme, cada uma com sua matrícula.

---

### ✍️ Mão na massa

1. No seu `<div class="card">` (o cartão do Step 8), adicione um atributo `id` com o valor exato `sally-adventure-book`.
2. Os dois atributos convivem na mesma tag de abertura —ordem não importa, mas `class` antes de `id` é convenção comum.
3. Valide a unicidade: Ctrl+F no arquivo e procure `sally-adventure-book` — deve haver **um** resultado.
4. DevTools: a tag deve aparecer como `<div class="card" id="sally-adventure-book">`.

> Teste de entendimento (e depois desfaz): copie o id para o `<h1>`. O navegador não grita — mas o padrão sim, e ferramentas de link quebram silenciosamente. `id` duplicado é bug invisível.

---

### ✅ Critérios de verificação do Step 9

- [ ] O `<div class="card">` tem `id="sally-adventure-book"`
- [ ] O valor está entre aspas, sem espaços, kebab-case
- [ ] O id não se repete em nenhum outro elemento da página

### 🧠 Antes de avançar

1. Um segundo cartão poderá ter o **mesmo** id? Poderá ter a **mesma** class?
2. Se um cliente pedir "link direto para o livro da Sally", qual atributo torna isso possível (`#...` no URL)?
