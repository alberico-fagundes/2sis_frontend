# Workshop: Página de Livraria

## Step 3 — Codificação (`<meta charset>`) e o `<body>`

---

### 📖 Teoria

**`<meta charset="UTF-8">`** é uma *meta tag* — ela não aparece na tela, mas dá uma instrução ao navegador. O valor `UTF-8` diz: "decodifique este arquivo usando UTF-8".

Por que isso importa?
- Acentuação é codificação disfarçada: `ç`, `ã`, `–`, emoji (`📚`) são **vários bytes** que só viram o caractere certo com a tabela UTF-8. Sem a meta tag, o navegador pode chutar uma tabela antiga e você verá o clássico `você` virar `vocÃª` (o temido "mojibake").
- Regra prática: o `charset` deve ser a **primeira coisa dentro do `<head>`**, antes de `<title>` e de qualquer outro `<meta>` — para valer sobre o resto do documento.
- `<meta>` é *elemento vazio* (void): não tem tag de fechamento nem conteúdo. Só atributos.

**`<body>`** é o outro filho do `<html>`: tudo que o usuário **vê** (textos, botões, imagens, os futuros cartões de livros) nasce aqui. Estrutura mental da página até agora:

```
html ──┬── head   → invisível (título, idioma, codificação)
       └── body   → visível (conteúdo)
```

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8">
    <title>Receta de Paella</title>
  </head>
  <body>
    <!-- conteúdo visível da página de receita -->
  </body>
</html>
```

Repare: o `<body>` é **irmão** do `<head>` (ambos filhos do `<html>`) — ele vem depois do `</head>`, não dentro dele. E o `charset` veio antes do `<title>`.

---

### ✍️ Mão na massa

Do zero, no seu arquivo:

1. No **início** do `<head>`, crie a meta tag que declara a codificação UTF-8. (Lembre: elemento vazio — sem `</meta>`.)
2. Depois do `</head>` **fechado**, crie o elemento do corpo da página, com tag de fechamento correspondente. Deixe-o vazio por enquanto — um comentário HTML indicando "conteúdo visível aqui" é bem-vindo.
3. Teste a codificação: escreva dentro do `<body>` uma frase com acentos e um emoji (ex.: `Livrção de ação à vista 📚`) e abra no navegador. Saiu certo?

> Se você colar o `charset` depois do `<title>`, o navegador geralmente ainda perdoa — mas em um arquivo salvo em outro encoding, a ordem errada quebra a decodificação. Boas práticas > "aqui funcionou".

---

### ✅ Critérios de verificação do Step 3

- [ ] `<meta charset="UTF-8">` existe dentro do `<head>`
- [ ] Ele aparece **antes** de qualquer outro conteúdo do `<head>`
- [ ] `<meta ...>` não tem tag de fechamento
- [ ] Existe um `<body>...</body>` como irmão do `<head>`, dentro do `<html>`
- [ ] O boilerplate completo já tem: DOCTYPE → html(lang) → head(charset, title) → body

### 🧠 Antes de avançar

1. Por que o navegador não pode "adivinhar" a codificação sozinho?
2. Quais elementos da sua página até agora são "invisíveis" e qual é "visível"?
3. No seu boilerplate, quem fecha primeiro: `</head>` ou `</body>`? Por quê?
