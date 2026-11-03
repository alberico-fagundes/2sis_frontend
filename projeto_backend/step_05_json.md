# Workshop: API da XYZ Bookstore

## Step 5 — JSON: a língua oficial das APIs

---

### 📖 Teoria

Texto corrido serve para humanos lerem no navegador. **JSON** serve para *programas* consumirem — e o programa que vai consumir é o `fetch` do frontend (depois, o do React). JSON (*JavaScript Object Notation*) é o subconjunto do JS que qualquer linguagem sabe ler.

Objeto JS → string JSON: **`JSON.stringify`**. String JSON → objeto JS: **`JSON.parse`** (usaremos no Step 8).

```javascript
const livro = { titulo: "Dom Casmurro", autor: "Machado de Assis", paginas: 256 };
JSON.stringify(livro);
// '{"titulo":"Dom Casmurro","autor":"Machado de Assis","paginas":256}'
```

O que **não pode** existir em JSON (e pode em JS — é onde alunos erram):

| JS aceita | JSON exige |
|-----------|------------|
| `titulo: "x"` | `"titulo": "x"` — **chaves entre aspas**, sempre |
| `'x'` aspas simples | só aspas **duplas** |
| vírgula sobrando `{a:1,}` | sem vírgula final |
| `undefined`, função, `//` comentário | nada disso — só dados: texto, número, booleano, null, objeto, array |

**A peça invisível:** o content-type. Devolver `application/json` no `writeHead` é o carimbo que diz ao `curl`/fetch/navegador: "o corpo é JSON — você pode `parse`". Sem ele, tecnicamente é um texto; o frontend até sobrevive, mas a API está mentindo no envelope.

| Content-type | Quando |
|--------------|--------|
| `text/plain` | mensagem humana solta |
| `text/html` | **raramente aqui** — página é papel do cliente (regra API-first) |
| `application/json` | **sempre** que o corpo for JSON |

Arrays de objetos são o formato padrão de "lista de recursos": `[{...livro1...}, {...livro2...}]`.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Uma API de meteorologia devolvendo a previsão (com um objeto `dados` pronto lá do Step 1):

```javascript
const http = require("node:http");

const previsao = [
  { dia: "segunda", tempMax: 31, chuva: false },
  { dia: "terca", tempMax: 27, chuva: true },
];

http.createServer((req, res) => {
  let corpo, status = 200;
  if (req.url === "/previsao") {
    corpo = JSON.stringify(previsao); // objeto -> string
  } else {
    status = 404;
    corpo = JSON.stringify({ erro: "rota inexistente" }); // até o erro vira JSON
  }
  res.writeHead(status, { "content-type": "application/json; charset=utf-8" });
  res.end(corpo);
}).listen(3000);
```

Repare em dois hábitos de API profissional: o 404 também responde **JSON estruturado** (`{erro: ...}`, nunca texto solto em API), e o body de erro tem o mesmo envelope dos dados.

---

### ✍️ Mão na massa

1. No `server.js`, crie um array `const livros = [...]` com 2 objetos: `titulo`, `autor`, `preco` (número) — você pode reaproveitar o `catalogo.js` do Step 1, mas **declara os dados no server.js** por enquanto.
2. Transforme a rota `/livros`: em vez do texto "em construção", o corpo deve ser `JSON.stringify(livros)` e o content-type do `writeHead`, `application/json; charset=utf-8`.
3. Rotas `/` e `/carrinho` ainda podem ser texto — mas o `else` (404) já passa a responder `JSON.stringify({ erro: "rota inexistente" })`.
4. Rode e teste:
   - navegador em `http://localhost:3000/livros` (verá a string crua — normal, navegador não renderiza JSON)
   - `curl -i http://localhost:3000/livros` — confirme o header `content-type: application/json`
   - `curl -i http://localhost:3000/xyz` — confirme 404 **com corpo JSON**
5. Caça-erro didático: quebre de propósito uma chave sem aspas dentro do `JSON.stringify` (não no objeto — no *resultado* impresso com `console.log`) e tente `JSON.parse` dela no REPL do node. O `parse` reclama; ele exige o JSON estrito. Conserte.

> Dica: se `curl` imprimir `Unexpected token` no parse, 9 em 10 vezes foi vírgula final ou aspas simples. O `console.log(JSON.stringify(...))` no código antes do `end` mostra exatamente o que vai no fio.

---

### ✅ Critérios de verificação do Step 5

- [ ] `/livros` devolve **array JSON** de 2 objetos com `titulo`, `autor`, `preco`
- [ ] O header responde `content-type: application/json; charset=utf-8` (visto com `curl -i`)
- [ ] 404 responde `{"erro":"..."}` com status 404, não texto puro
- [ ] O corpo de `/livros` visto no `curl` tem chaves com aspas duplas e nenhuma vírgula final

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. Por que `{titulo: 'x'}` (JS válido) **não** é JSON válido?
2. Quem chama `JSON.stringify` — o servidor ou o consumidor? E o `parse`, quem vai chamar na Fase 3?
3. Por que um erro também deve ser devolvido em JSON, e não como frase solta?
