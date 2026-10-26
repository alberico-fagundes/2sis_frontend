# Workshop: Página de Livraria

## Step 10 — Título dentro do cartão: `<h2>`

---

### 📖 Teoria

Hierarquia de headings **não é estética, é sumário**. Cada nível diz "estou dentro de qual assunto":

```
h1  XYZ Bookstore          ← a página
└── h2  Sally's SciFi Adventure  ← um item DENTRO da página (o título do livro)
```

O `<h2>` do cartão vive **dentro do `<div class="card">`** porque ele é o título *daquele livro*, não *da livraria*. Se fosse `<h1>`, diria ao mundo (e ao leitor de tela, e ao Google) que o livro é o assunto da página inteira — e ainda quebraria a regra de um único `h1`.

Regra mental do aninhamento semântico: **heading desce um nível a cada "dentro" conceptual**. Página → seção → subseção. Não é obrigatório pular para `h3` aqui (o `h2` filho do `h1` está correto), mas **nunca** subir acima do que te contém.

- `<h2>` é elemento com conteúdo, como todo heading: texto entre `<h2>` e `</h2>`.
- Dentro do cartão, ele é o **primeiro** filho: título antes de descrição, como em qualquer ficha de catálogo.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<body>
  <h1>Cardápio</h1>
  <div class="prato-card">
    <h2>Pizza Margherita</h2>
    <!-- descrição viria a seguir -->
  </div>
</body>
```

O `h1` é o restaurante; o `h2`, um prato específico dele.

---

### ✍️ Mão na massa

1. Abra o `<div class="card" id="sally-adventure-book">` e, **dentro dele**, crie um heading de nível **2**.
2. Texto exato: `Sally's SciFi Adventure` — repare no apóstrofo em `Sally's` (crase, não aspas: `'`).
3. Indente o `<h2>` dentro do cartão e salve.
4. Na tela: o título aparece como segundo degrau visível abaixo do `<h1>` da livraria. No DevTools, a árvore deve mostrar `h2` como filho do `div.card`.

> Apóstrofo é conteúdo normal em HTML — não precisa de escape dentro de texto. Só dentro de **atributos** com aspas iguais ele complicaria.

---

### ✅ Critérios de verificação do Step 10

- [ ] Existe um `<h2>` com o texto `Sally's SciFi Adventure`
- [ ] O `<h2>` está dentro do `div.card#sally-adventure-book`
- [ ] O `<h1>` da página continua único e sem irmão `h2` solto no body

### 🧠 Antes de avançar

1. Por que o título do livro não pode ser um `<h1>`?
2. Se amanhã você agrupar livros por gênero com sub-títulos, que nível usaria dentro dos cartões?
