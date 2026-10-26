# Workshop: Página de Livraria

## Step 13 — Segundo cartão: a class se repete de propósito

---

### 📖 Teoria

Regra que você já conhece: **`class` não precisa ser única**. É a hora de provar na prática — criar um segundo `<div class="card">` e ver dois elementos com o mesmo rótulo convivendo legalmente.

Para que serve essa repetição?

1. **Padrão de design**: todos os cartões são *a mesma coisa* (um livro), logo merecem o mesmo nome. O que muda é o conteúdo, não o tipo.
2. **CSS em série** (lá na frente): uma regra `.card { border: ... }` estiliza **os dois** (e o décimo) de uma vez — é para isso que classes existem.
3. **Estrutura legível**: quem lê o código vê `card-container` com N `card` filhos e entende o modelo sem esforço: *coleção de itens do mesmo tipo*.

Dica de eficiência dos profissionais: em vez de digitar tudo de novo, **copie o bloco do primeiro cartão inteiro** (do `<div class="card"...>` até o `</div>` dele), cole como irmão *dentro da container*, e só então troque os valores. Copiar a *estrutura* é produtivo; o que se personaliza é a *identidade* (id, títulos, textos) — é o próximo step.

Árvore-alvo:

```
div.card-container
├── div.card#sally-adventure-book   (h2 + p + button)
└── div.card                        (h2 + p + button)  ← novo
```

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<div class="playlist">
  <div class="faixa">Bohemian Rhapsody</div>
  <div class="faixa">We Will Rock You</div>
</div>
```

Duas faixas, mesma class, conteúdo diferente — coleção de itens do mesmo tipo.

---

### ✍️ Mão na massa

1. Dentro do `<div class="card-container">`, **depois** do primeiro `</div>` de cartão (mas antes do `</div>` da container!), crie um segundo `<div>` com class `card`.
2. Duplique a anatomia do primeiro: `h2`, `p` de sinopse e `button.btn` com `Buy Now` — os textos do Dave entram no próximo step, então use texto provisório seu ou deixe vazio e preencha depois.
3. Cuidado com o clássico: colar o novo cartão **fora** da container. No DevTools, o `div.card` novo deve aparecer como **irmão** do primeiro, ambos dentro de `div.card-container`.
4. Ctrl+F por `class="card"`: dois resultados (e nenhum com aspas erradas).

> Um `</div>` a mais ou a menos em cards aninhados é o bug nº1 de HTML. Se a estrutura parecer "engolida", confira primeiro os fechamentos do cartão 1.

---

### ✅ Critérios de verificação do Step 13

- [ ] Existe um segundo `<div class="card">`
- [ ] Ele está dentro da `card-container`, como irmão do primeiro card
- [ ] Os dois cartões têm a mesma class `card`

### 🧠 Antes de avançar

1. Se os dois têm `class="card"`, como o documento ainda sabe distingui-los? (Spoiler do próximo step: `id`.)
2. Quantas vezes a class `btn` deve aparecer depois que o cartão do Dave ficar pronto?
