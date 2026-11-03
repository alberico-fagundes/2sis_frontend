# Workshop: API da XYZ Bookstore

## Step 13 — Express: o seu código, embrulhado por outra pessoa

---

### 📖 Teoria

`npm install express` — e a primeira pergunta honesta: **o que ele faz que eu não sabia fazer?** O Step 10 escreveu, na mão, roteador, parser e helper. O Express não inventa nada: ele **é** esse código, com nome. Quem escreveu por dentro sabe exatamente o que importou — e é por isso que o Express vem só agora, nunca antes.

Instalação como `dependencies` (diferente do nodemon!): a aplicação **precisa** do Express para rodar em produção.

```bash
npm install express
```

A paridade, lado a lado (guie o olho, é o quadro-negro do step):

| Fase 1 (você escreveu) | Express |
|------------------------|---------|
| `require("node:http")` + `createServer((req,res)=>{...})` | `const app = express()` |
| `if (caminho === "/livros" && req.method === "GET")` | `app.get("/livros", handler)` |
| `enviar(res, 200, JSON.stringify(x))` | `res.json(x)` ( stringify + content-type + end, tudo junto) |
| seu 404 no `else` final | `app.use((req, res) => ...)` por último |
| `servidor.listen(3000)` | `app.listen(3000)` |

O `app` **é** a função que o `http.createServer` esperava — um Express app é, por baixo, o callback do Step 2 que você já assinava. `res.json()` não é mágica: é o `enviar()` do Step 9, pronto de fábrica.

**Arquitetura da mudança (importante):** você NÃO apaga o `server.js` da Fase 1. Ele é a referência de comparação — e o professor vai pedir os dois abertos lado a lado no Step 16. O Express vive num arquivo novo, `app.js`, e nesta aula **um dos dois** roda na porta: um servidor por vez, sempre (`EADDRINUSE` é o fiscal).

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

A API da horta do Step 4, em três versões: 15 linhas de `if` na Fase 1, cinco linhas de Express:

```javascript
const express = require("express");
const app = express();

const hortalias = [{ id: "alface", nome: "Alface" }];

app.get("/hortalias", (req, res) => {
  res.json(hortalias);
});

app.listen(3000, () => console.log("Horta Express na 3000"));
```

`app.get(caminho, handler)` substitui a cadeia inteira `if (caminho === ... && req.method === "GET")`. O handler continua recebendo `(req, res)` — os mesmos objetos do Step 3, só que com superpoderes chegando (`req.query`, `req.body`, `req.params` — um por step agora).

---

### ✍️ Mão na massa

1. `npm install express`. Abra `package.json`: o Express entrou em `dependencies` (e o nodemon continua em `devDependencies` — categorias corretas, olhe com os olhos).
2. Crie `app.js`. Dentro, a estrutura mínima do exemplo: require, `express()`, rota `app.get("/livros", ...)` respondendo `res.json(livros)` com o catálogo real do Step 6 (copie o array `const livros` do `server.js` para dentro do `app.js` — memória ainda, sem módulos por enquanto).
3. Suba com o script novo: edite `package.json` → `"start": "node app.js"` e `"dev": "nodemon app.js"` (a profecia do Step 11 se cumpriu). Rode `npm run dev`.
4. Teste `GET /livros` com `curl` e compare o corpo com o `server.js`: **byte a byte igual**. O contrato não mudou — trocou o motor, não a saída. (Guarde essa frase: é a regra da Fase 3 inteira.)
5. Derrube, e rode `npm run dev` com o `server.js` ainda vivo no outro terminal: provoque e leia o `EADDRINUSE`, depois restaure um servidor só.
6. `Ctrl+C` → `git diff` mental: quantas linhas o Express te devolveu? (Escreva o número no caderno; o Step 16 cobra.)

> Nenhuma rota da Fase 1 foi portada além de `/livros` — de propósito. Rotas e params vêm no Step 14; POST/carrinho no 15. Quem porta tudo de uma vez não sente o Express, só o usa.

---

### ✅ Critérios de verificação do Step 13

- [ ] `app.js` roda com `npm run dev` e responde `GET /livros` com o mesmo JSON do `server.js`
- [ ] `express` está em `dependencies`; `nodemon` em `devDependencies`
- [ ] Os scripts `start`/`dev` apontam para `app.js` (o `server.js` ficou de museu, não sumiu)
- [ ] O header `content-type: application/json` continua presente no `curl -i` (sem escrever nenhum `writeHead`!)

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. O que `res.json()` faz nas três linhas que o seu `enviar()` fazia? Liste.
2. `const app = express()` — onde está o `createServer` aí dentro? (Pista: `app` é função; quem a chamaria?)
3. Por que manter o `server.js` intacto ao lado do `app.js` em vez de editar em cima? (Resposta curta: a régua que prova que o contrato não mudou.)
