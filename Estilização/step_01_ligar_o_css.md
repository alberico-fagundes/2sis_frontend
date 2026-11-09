# Workshop: Estilo da Livraria

## Step 1 — Ligar o CSS: a primeira opinião sua


---

### 📖 Teoria

Sua página hoje é estilizada pelo navegador, não por você. Para dar opinião própria, existem três endereços possíveis:

| Forma | Onde vive | Quando usar |
|---|---|---|
| **inline** | atributo `style` na tag 
| **interno** | `<style>` no `<head>` 
| **externo** | arquivo `.css` à parte

O externo vence porque separa as responsabilidades: HTML responde *o que é*, CSS responde *como aparece*. Um arquivo, todas as páginas.

`<link>` é **elemento vazio** — da mesma família do `<meta charset>` que você já escreveu: sem tag de fechamento, só atributos. E a ordem dentro do `<head>` é `charset` → `title` → `link`.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<head>
  <meta charset="UTF-8">
  <title>Horta do Bairro</title>
  <link rel="stylesheet" href="estilos.css">
</head>
```

Repare: o `href` aponta para um arquivo que **ainda não existe** — e isso não é erro, é ordem de trabalho.

---

### ✍️ Mão na massa

1. Ao lado do seu `index.html`, crie um arquivo vazio chamado `styles.css`.
2. No `<head>`, **depois** do `<title>`, escreva a tag de ligação com `rel="stylesheet"` e `href="styles.css"`.
3. No `styles.css`, escreva sua primeira regra: o seletor `h1` com a propriedade `color` e uma cor de sua escolha.
4. Salve, recarregue (F5): o letreiro da livraria mudou de cor?

> Se nada mudou, 9 em 10 vezes é `rel` faltando ou caminho errado. O console não grita com link quebrado — a aba **Network** do DevTools sim.

---

### ✅ Critérios de verificação do Step 1

- [ ] `styles.css` existe na mesma pasta que o `index.html`
- [ ] `<link rel="stylesheet" href="styles.css">` está no `<head>`, depois do `<title>`, sem `</link>`
- [ ] Existe uma regra de `h1` com `color` no `styles.css`
- [ ] O letreiro aparece com a cor nova na tela

### 🧠 Antes de avançar

1. Por que `rel="stylesheet"` não é decorativo?
2. Se o CSS morar em `css/styles.css`, o que muda no `href`?
