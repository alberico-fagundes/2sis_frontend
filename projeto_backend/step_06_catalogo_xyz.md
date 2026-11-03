# Workshop: API da XYZ Bookstore

## Step 6 — O catálogo real: contratos precisam de `id`

---

### 📖 Teoria

No Step 5 a rota `/livros` devolvia dados, mas ainda não era um **contrato**. Contrato de API são três promessas que o backend faz ao frontend (seja o HTML do projeto2, seja o React da Fase 4):

1. **Endereço estável:** `/livros` sempre devolve livros — o consumidor nunca adivinha.
2. **Formato estável:** mesmos campos, mesmo nome, sempre.
3. **Identidade estável:** cada recurso tem um `id` — o frontend referencia, o backend localiza. Sem id, "compre o segundo livro" vira "conte itens no array e torça para a ordem nunca mudar".

Os livros da sua livraria devem ser **exatamente os dois cards do projeto2** — o `id` do recurso JSON nasce igual ao `id` do card HTML:

```javascript
const livros = [
  {
    id: "sally-adventure-book",
    titulo: "As Aventuras de Sally",
    autor: "A. Writer",
    descricao: "Uma expedição que muda tudo.",
    preco: 39.9,
  },
  {
    id: "dave-cooking-book",
    titulo: "A Cozinha do Dave",
    autor: "D. Chef",
    descricao: "Receitas para quem queimou a primeira.",
    preco: 29.5,
  },
];
```

Buscar "no servidor" é só o `array` que você já conhece — `find` devolve o objeto ou `undefined`:

```javascript
const livro = livros.find((l) => l.id === "sally-adventure-book");
```

`req.url` chega como string. `/livros/sally-adventure-book` **não casa** no `===` do Step 5 — é uma rota *parametrizada*: um pedaço do endereço é dado, não endereço. Manualmente, resolve-se com fatiamento:

```javascript
const partes = req.url.split("/"); // "/livros/sally" -> ["", "livros", "sally"]
```

`split("/")` corta a URL em pedaços; o índice `2` é o id pedido. Não existe mágica — Express (Fase 2) só dará nome bonito a exatamente isso (`/livros/:id`).

**Padrão REST de respostas** (decore agora, use a Fase inteira):

| Pedido | Resposta certa |
|--------|----------------|
| `GET /livros` (lista) | `200` + **array** (mesmo se só 1 livro; sempre array — o consumidor não trata exceção) |
| `GET /livros/:id` existe | `200` + **objeto** |
| `GET /livros/:id` não existe | `404` + `{ erro: "livro não encontrado" }` |

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Um cardápio de cafeteria com rota parametrizada manual:

```javascript
const http = require("node:http");

const cafes = [
  { id: "espresso", nome: "Espresso", preco: 7 },
  { id: "capuccino", nome: "Cappuccino", preco: 12 },
];

http.createServer((req, res) => {
  const partes = req.url.split("/"); // ["", "cafes", "espresso"]
  let corpo, status = 200;

  if (req.url === "/cafes") {
    corpo = JSON.stringify(cafes);
  } else if (partes[1] === "cafes" && partes[2]) {
    const cafe = cafes.find((c) => c.id === partes[2]);
    if (cafe) {
      corpo = JSON.stringify(cafe);
    } else {
      status = 404;
      corpo = JSON.stringify({ erro: "cafe nao encontrado" });
    }
  } else {
    status = 404;
    corpo = JSON.stringify({ erro: "rota inexistente" });
  }

  res.writeHead(status, { "content-type": "application/json; charset=utf-8" });
  res.end(corpo);
}).listen(3000);
```

A ordem dos `if` importa: a rota **exata** `/cafes` é testada antes da **padrão** `/cafes/:id`. `partes[1] === "cafes"` garante que só o recurso certo entra no fatiamento.

---

### ✍️ Mão na massa

1. Substitua o array `livros` do Step 5 pelo catálogo com contrato: 2 ou 3 livros, cada um com `id` em kebab-case, `titulo`, `autor`, `descricao`, `preco`. Use os livros da página do projeto2 (`sally-adventure-book` e o segundo card) — a API vai alimentar exatamente essa livraria depois.
2. Na estrutura de rotas do Step 5, transforme o `if/else` no formato do exemplo (variável `corpo`/`status` → um `writeHead`/`end` no fim), e adicione a rota parametrizada:
   - `GET /livros` → array inteiro
   - `GET /livros/:id` → o livro via `find`, ou `404 {erro}` se `undefined`
3. Teste os três casos (navegador **ou** `curl`):
   - `/livros` → array com todos
   - `/livros/sally-adventure-book` → um objeto
   - `/livros/livro-fantasma` → 404 JSON
4. Conferência de contrato: `curl -i http://localhost:3000/livros/livro-fantasma` — status 404, content-type application/json, corpo `{erro}`. Os três juntos.

> O `id` do card HTML (`<div id="sally-adventure-book">`) virou o `id` do recurso JSON. Não foi coincidência — foi o plano desde o projeto2. Frontend e backend agora apontam para a **mesma** identidade.

---

### ✅ Critérios de verificação do Step 6

- [ ] Todo livro tem `id` em kebab-case + `titulo`, `autor`, `descricao`, `preco`
- [ ] `/livros` devolve **array** (mesmo com 1 livro testando, continua array)
- [ ] `/livros/:id` devolve **objeto único** com status 200
- [ ] `/livros/inexistente` devolve 404 com `{"erro": ...}` em JSON
- [ ] Nenhum `res.end` esquecido em nenhum caminho possível do `if/else`

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. Por que `/livros` com 1 resultado deve virar `[livro]` e não `livro`?
2. O que `req.url.split("/")` devolve para `/livros`? E para `/livros/abc`? (Índices! Preencher de cabeça antes de responder.)
3. Se amanhã você trocar o HTML do projeto2 por React, o que muda **neste** servidor para ele continuar funcionando? (Essa é a pergunta do workshop inteiro — responda com o roadmap aberto.)
