# Workshop: Página de Livraria

## Step 7 — O atributo `class`

---

### 📖 Teoria

Atributos qualificam elementos: ficam na tag de abertura, no formato `nome="valor"`. Você já usou um: `lang="en"` no `<html>`. Agora entra o **`class`**.

`class` serve para **marcar elementos com um rótulo** — uma etiqueta que diz "quem eu sou / a que grupo pertenço". Originalmente o CSS usa essas etiquetas para estilizar ("todos com a classe X ficam com fundo branco"), mas classes também servem para **organizar e nomear** a estrutura, que é o caso deste workshop.

Regras do `class`:

| Propriedade | Detalhe |
|---|---|
| Pode ser repetida | **Vários** elementos podem ter a **mesma** class (ex.: todos os cartões com `card`). |
| Pode combinar | Um elemento aceita **várias classes** de uma vez: `class="card novo"`. |
| Não é único | Se precisa de um nome exclusivo para um único elemento, existe outro atributo — o `id` (viemos dele falar já). |
| Nome em kebab-case | Nomes compostos usam hífen: `card-container`, não `cardContainer` ou `card container` (espaço separa classes!). |

Formato de um parágrafo rotulado, como no exemplo oficial do fCC:

```html
<p class="example">example paragraph</p>
```

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<div class="itens-do-cardapio">
  <p class="prato">Pizza</p>
  <p class="prato">Lasanha</p>
</div>
```

Perceba: o container ganhou um nome de grupo (`itens-do-cardapio`) e cada item repete o **mesmo** rótulo `prato` — porque `class` não precisa ser única.

---

### ✍️ Mão na massa

1. Volte ao `<div>` do Step 6 (sua container de cartões).
2. Dê a ele uma **class** que o nomeie como o que ele agrupa: o valor exato deve ser `card-container`.
3. Escreva o atributo na **tag de abertura**, com aspas no valor — nada de `<div>class="..."` ou `</div class=...>`.
4. Confirme no DevTools: a tag passa a aparecer como `<div class="card-container">`.

> Anti-padrão que vale testar de propósito (e depois desfazer): tirar as aspas. Veja como o navegador reage — e por que as aspas não são decoração.

---

### ✅ Critérios de verificação do Step 7

- [ ] O `<div>` do Step 6 agora tem `class="card-container"`
- [ ] O atributo está na tag de **abertura**
- [ ] O nome está exatamente como pedido (kebab-case, minúsculas)

### 🧠 Antes de avançar

1. Dois cartões diferentes podem carregar a mesma class? E o `lang` do `<html>`, poderia ser repetido em outro elemento?
2. Qual é a diferença prática entre `class` e `id` (que vem nos próximos steps)?
