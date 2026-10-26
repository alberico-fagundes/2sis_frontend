# Workshop: Página de Livraria

## Step 4 — O primeiro título visível: `<h1>`

---

### 📖 Teoria

Até agora, tudo o que você criou era **configuração invisível** (`head`, `title`, `meta`). A partir deste step, o conteúdo aparece na tela — dentro do `<body>`.

`<h1>` é a **heading de nível 1**: o título principal, o "letreiro" da página. Existe uma escada de seis níveis, `<h1>` → `<h6>`, e ela comunica **hierarquia**, não tamanho de fonte:

- `<h1>` = o assunto da página (um só, tipicamente)
- `<h2>` = grandes seções dentro dela
- `<h3>`…`<h6>` = subdivisões cada vez menores

Por que não usar só `<b>` ou fonte grande? Porque leitores de tela navegam **por headings** (pula de título em título como um cego faria com o sumário de um livro), e buscadores usam `<h1>` para entender sobre o que é a página. Pular níveis (`h1` → `h4`) quebra essa régua.

Diferença crucial com o `<title>` do Step 2: o `<title>` nomeia a **aba do navegador**; o `<h1>` nomeia a **página visível**. Os dois costumam se parecer, mas vivem em lugares diferentes do documento.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<body>
  <h1>Cinema do Bairro</h1>
</body>
```

Repare: heading é elemento **com conteúdo** — o texto fica entre `<h1>` e `</h1>`, e ele é filho direto do `<body>`.

---

### ✍️ Mão na massa

1. Dentro do seu `<body>`, crie o título principal da livraria, nível máximo da hierarquia.
2. O texto deve ser exatamente: `XYZ Bookstore`.
3. Feche a tag, salve, recarregue o navegador (F5). O nome apareceu grande e em negrito? Isso é o **estilo padrão do navegador**, não CSS seu — o visual refinado vem depois.

> Se nada apareceu, confira se o `<h1>` está **dentro** do `<body>` — conteúdo solto fora do body é zona cinzenta do parse HTML.

---

### ✅ Critérios de verificação do Step 4

- [ ] Existe um elemento `<h1>` com o texto `XYZ Bookstore`
- [ ] O `<h1>` está dentro do `<body>`
- [ ] A página visível mostra o texto ao recarregar

### 🧠 Antes de avançar

1. Por que `XYZ Bookstore` não pode ir direto dentro do `<title>` e ponto final? Que função cada um cumpre?
2. Quantos `<h1>` uma página bem estruturada costuma ter?
