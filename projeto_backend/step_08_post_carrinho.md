# Workshop: API da XYZ Bookstore

## Step 8 — POST: o cliente também manda dados (e o body não cai pronto)

---

### 📖 Teoria

Até agora, todo pedido era `GET`: "me entrega aquilo". O botão **Buy Now** do projeto2 pede outra coisa: *guarda este livro no carrinho*. Dados agora viajam **na ida** — no **corpo** do request (`body`) — e corpo na ida é trabalho do método `POST`.

| | GET | POST |
|---|-----|------|
| Dados do cliente | só na URL (query, curtos, públicos) | no corpo (qualquer tamanho/formato) |
| Semântica | "leia" | "execute/crie" |
| `req.method` | `"GET"` | `"POST"` |

Você acessa o método com `req.method` — e passa a comparar **caminho + método** juntos: o `/carrinho` que *lista* (GET) e o `/carrinho` que *adiciona* (POST) são a mesma URL, vidas diferentes.

**A pegadinha estrutural:** o corpo **não chega pronto**. Ele chega em **pedaços** (chunks), como stream — e isso muda o fluxo do seu handler, que era todo síncrono. O `req` é um **Readable** que emite eventos:

```javascript
let bruto = "";
req.on("data", (pedaco) => { bruto += pedaco; }); // chega pedaço -> acumula
req.on("end", () => { /* body completo AQUI */ }); // acabou -> parseia e responde
```

Consequência direta: **o `res.end` não pode mais ficar no fim do handler** — ele deve viver **dentro** do callback do `"end"`. Se você responder fora dele (o instinto de quem vem do Step 7), responde *antes* do body chegar: carrinho vazio garantido. O pedido vira uma pequena história assíncrona: acumula... acumula... chegou tudo — aí sim processa e responde.

Parse do corpo: `JSON.parse(bruto)` (o cliente mandou JSON — você exige `content-type: application/json` do lado dele? Ainda não; o erro malformado é o assunto do Step 9).

Estado: `const carrinho = []` no módulo, memória pura — o POST adiciona `{ livroId, quantidade }` com `push`.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Um formulário de sugestões da cantina recebendo POST:

```javascript
const http = require("node:http");

const sugestoes = [];

http.createServer((req, res) => {
  const [caminho] = req.url.split("?");

  if (caminho === "/sugestoes" && req.method === "GET") {
    res.writeHead(200, { "content-type": "application/json" });
    return res.end(JSON.stringify(sugestoes));
  }

  if (caminho === "/sugestoes" && req.method === "POST") {
    let bruto = "";
    req.on("data", (pedaco) => { bruto += pedaco; });
    req.on("end", () => {
      const texto = JSON.parse(bruto);        // -> dentro do "end", não fora!
      sugestoes.push(texto);
      res.writeHead(200, { "content-type": "application/json" });
      res.end(JSON.stringify({ gravado: texto }));
    });
    return; // o "end" acima é quem responde — aqui ainda não há resposta
  }

  res.writeHead(404, { "content-type": "application/json" });
  res.end(JSON.stringify({ erro: "rota inexistente" }));
}).listen(3000);
```

Testável sem navegador, mandando corpo na linha de comando:

```bash
curl -X POST http://localhost:3000/sugestoes \
  -H "content-type: application/json" \
  -d '{"prato": "feijoada", "dia": "sexta"}'
```

`-X POST` muda o método, `-H` adiciona header, `-d` é o **d**ado do corpo.

---

### ✍️ Mão na massa

1. Declare `const carrinho = [];` perto do `const livros`.
2. Reorganize o handler para o formato do exemplo: blocos `if` com `return res.end(...)` em vez da variável única — a resposta agora tem dois tempos (síncrona no GET, assíncrona no POST), e o fluxo unificado do Step 7 não aguenta mais.
3. `GET /carrinho` → array atual (substitui o texto "em construção").
4. `POST /carrinho` → acumule os chunks em `bruto`, dentro do `req.on("end")`: `JSON.parse`, faça `push` no `carrinho`, responda `res.end(JSON.stringify({ carrinho }))` com o carrinho **já atualizado** (o cliente vê o resultado, não um "ok" vago).
5. Teste o ciclo completo **no terminal** (vários pedidos, uma sessão `curl` de cada vez):

```bash
curl http://localhost:3000/carrinho
curl -X POST http://localhost:3000/carrinho \
  -H "content-type: application/json" \
  -d '{"livroId": "sally-adventure-book", "quantidade": 1}'
curl http://localhost:3000/carrinho   # o item apareceu?
```

6. Experimento de maldade controlada: envie `-d '{"livroId": "nao-existe", ...}'`. O servidor **aceitou** (ele ainda não valida). Anota essa dor — ela é o Step 9.

> `Ctrl + C` e re-rodar apaga o carrinho (memória ≠ banco). Está correto: estado volátil é honesto nessa fase; persistência é assunto de outro módulo (e chega mais perto com banco na sequência do curso).

---

### ✅ Critérios de verificação do Step 8

- [ ] `GET /carrinho` e `POST /carrinho` respondem **coisas diferentes** na mesma URL (a comparação usa `req.method`)
- [ ] O POST **acumula** chunks e só responde dentro de `req.on("end")`
- [ ] A resposta do POST já traz o item incluído
- [ ] Um `curl -X POST` com JSON válido adiciona item confirmado pelo `GET` seguinte

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. Por que `res.end` no fim do handler quebrou quando você mexeu com POST? (Desenhe a ordem: handler roda inteiro ANTES do `"end"` do body.)
2. O que acontece se um chunk chegar pela metade do JSON (`{"livro` ... `Id": ...}`) e você responder no `"data"` em vez do `"end"`?
3. Duas requisições POST simultâneas no mesmo `carrinho` do módulo: alguma garante a ordem? Por que isso preocuparia um banco de verdade?
