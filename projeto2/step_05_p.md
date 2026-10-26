# Workshop: Página de Livraria

## Step 5 — O primeiro parágrafo: `<p>`

---

### 📖 Teoria

`<p>` é o **parágrafo**: a unidade básica de texto corrido do HTML. Se `<h1>` é o letreiro, `<p>` é o texto da vitrine.

- Assim como `<h1>`, é elemento **com conteúdo**: o texto fica entre `<p>` e `</p>`.
- O navegador quebra **automaticamente** uma linha em branco (margem vertical) antes e depois de cada `<p>`. Você não precisa de `<br>` nem de Enter duplo no código — a margem já é do elemento.
- HTML **colapsa espaço em branco**: cinco espaços digitados viram um; quebras de linha "de digitação" dentro do texto não viram quebras na tela. Por isso estruturamos com elementos, não com espaços.
- Ordem importa para a leitura (e para o SEO): `<h1>` anuncia, `<p>` explica — o parágrafo de apoio vem **abaixo** do título, como irmão, ambos filhos do `<body>`.

```
body ──┬── h1   "XYZ Bookstore"
       └── p    "Browse our collection of amazing books!"
```

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<body>
  <h1>Cinema do Bairro</h1>
  <p>Sessões todos os dias a partir das 18h.</p>
</body>
```

---

### ✍️ Mão na massa

1. **Abaixo** do seu `<h1>` (mas ainda dentro do `<body>`), crie um parágrafo de boas-vindas.
2. O texto deve ser exatamente: `Browse our collection of amazing books!`
3. Salve e recarregue. Você deve ver: letreiro grande em cima, frase de apoio embaixo, com um respiro entre eles — sem você ter feito nada além de criar os dois elementos.

> Erro clássico do step: fechar com `</p>` mas esquecer o `!` — pontuação também faz parte do texto que o validador compara.

---

### ✅ Critérios de verificação do Step 5

- [ ] Existe um elemento `<p>` com o texto `Browse our collection of amazing books!`
- [ ] O `<p>` está **depois** do `<h1>`, dentro do `<body>`
- [ ] A frase aparece na tela abaixo do título

### 🧠 Antes de avançar

1. Se você apagasse o `<p>` e escrevesse o texto solto no `<body>`, aparecerá na tela? Por que usar o elemento mesmo assim?
2. O espaço entre título e parágrafo veio de onde?
