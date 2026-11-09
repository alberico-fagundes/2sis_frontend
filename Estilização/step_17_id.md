# Workshop: Estilo da Livraria

## Step 17 — `id`: a matrícula, e por que ela não veste ninguém

---

### 📖 Teoria

No CSS, `#nome` busca **um** elemento — aquele cujo atributo `id` é esse. É a tradução do Step 9 de HTML: `class` é uniforme de grupo, `id` é nome civil.

Sua página tem **quatro** ids, e nenhum deles precisa de regra de estilo. Os três usos legítimos:

| Uso | Por que precisa ser único |
|---|---|
| **âncora** — `index.html#dave-cooking-book` | o navegador precisa achar *um* destino |
| **JavaScript** — `getElementById` | o script quer *aquele* elemento |
| **`<label for>` / ARIA** | acessibilidade liga dois elementos por nome |

**Por que não estilizar por id:**

1. **peso na balança** — um id atropela qualquer classe (o Step 18 quantifica isso);
2. **não reusável** — a regra nasce condenada a um elemento só; o terceiro livro não herda nada;
3. **frágil** — renomear o id no HTML quebra o CSS **sem erro visível**.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<div class="cadeira" id="setor-norte-a12">A12</div>
```

```css
.cadeira { padding: 4px; }            /* o uniforme: todas */
#setor-norte-a12 { background: gold; } /* a matrícula: só uma */
```

Se o camarote virar três assentos, a regra de id precisa ser triplicada à mão; a de classe já serve.

---

### ✍️ Mão na massa

1. Copie a URL da página, cole `#dave-cooking-book` no fim e abra. O navegador rolou até o cartão do Dave?
2. Repita com `#sally-adventure-book`. Se a página for curta e não tiver para onde rolar, confira no DevTools que o elemento recebeu o foco — a âncora funcionou do mesmo jeito.
3. Escreva uma regra `#checkout-btn` com uma cor de fundo e veja que **só** ele muda. Funcionou — e é exatamente isso que se questiona.
4. **Refatore:** no HTML, dê ao checkout uma segunda class (`class="btn btn-primary"`). No CSS, transforme a regra de id em `.btn-primary` e **apague a de id**.

> `Ctrl+F` por `#` no `styles.css` deve dar **zero** seletores de id. Os quatro ids do HTML continuam lá, intactos, servindo de âncora e de alvo futuro do JavaScript.

---

### ✅ Critérios de verificação do Step 17

- [ ] O teste de âncora rolou (ou focou) o cartão certo
- [ ] O botão de checkout está distinto **por classe**, não por id
- [ ] `styles.css` não tem **nenhum** seletor de id
- [ ] Os quatro ids do HTML permanecem únicos e intactos

### 🧠 Antes de avançar

1. Que três funções o id ainda cumpre sem ser estilo?
2. Se a livraria crescer para 40 livros, quantas regras de classe você escreve — e quantas de id seriam viáveis?
