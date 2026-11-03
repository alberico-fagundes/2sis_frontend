# Workshop: API da XYZ Bookstore

## Step 3 — `req` e `res`: o pedido entra, o prato sai

---

### 📖 Teoria

A callback do servidor recebe **dois** parâmetros, e cada um é um lado do diálogo HTTP:

| Parâmetro | O que é | Analogia |
|-----------|---------|----------|
| `req` | O **request** — tudo que o navegador enviou: URL, método, cabeçalhos | O pedido que o garçom anota |
| `res` | O **response** — o balde vazio onde você escreve a resposta | O prato que você monta e entrega |

Três comandos fecham 90% do backend cru:

```javascript
res.writeHead(200, { "content-type": "text/plain; charset=utf-8" });
res.write("Olá!");
res.end();
```

- **`writeHead(status, headers)`** — carimba o envelope: código (`200` = ok) e o **content-type**, que diz ao navegador *como* ler o corpo (`text/plain`, `text/html`, `application/json`...). Errar o content-type é entregar sopa num prato de sólido: o conteúdo existe, o leitor interpreta errado.
- **`res.write(...)`** — escreve texto no corpo. Pode chamar várias vezes.
- **`res.end()`** — **obrigatório e último**. Selar o envelope e entregar. Sem ele, o navegador fica girando para sempre (o pesadelo do Step 2). Depois do `end`, nada mais é aceito.

Atalho honesto: `res.end("texto")` já escreve e sela numa chamada só.

O `req.url` que você logou no step anterior é só uma das informações do `req` — o que fazer com ela vem no Step 4.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Um servidor de padaria respondendo HTML:

```javascript
const http = require("node:http");

http.createServer((req, res) => {
  res.writeHead(200, { "content-type": "text/html; charset=utf-8" });
  res.end("<h1>Padaria do Bairro</h1><p>Pão fresco às 6h.</p>");
}).listen(3001);
```

Abra no navegador: como o content-type é `text/html`, o navegador **renderiza** o `<h1>` — a mesma string com `text/plain` apareceria crua, com as tags à mostra. Content-type muda o destino do mesmo texto.

---

### ✍️ Mão na massa

1. Edite o `server.js` do Step 2: faça o callback aceitar **dois** parâmetros `(req, res)`.
2. Dentro dele, mande `writeHead` com status `200` e content-type `text/html; charset=utf-8`.
3. Encerre com `res.end(...)` enviando uma página mínima: um `<h1>` com o nome da livraria e um `<p>` qualquer. (Apague ou comente o `console.log` com `req.url` deste step — ainda vamos usá-lo.)
4. Rode `node server.js`, abra `http://localhost:3000` e confirme: **parou de travar** e renderiza o HTML.
5. Experiência de controle: troque o content-type para `text/plain` e recarregue. As tags apareceram escritas? Esse é o poder do carimbo.
6. `Ctrl + C` para derrubar.

> Dica: mudou o código → o servidor antigo continua rodando o código **velho**. Sempre `Ctrl + C` e `node server.js` de novo. (Essa dor tem remédio chamado `nodemon` — Fase 2.)

---

### ✅ Critérios de verificação do Step 3

- [ ] O navegador mostra o HTML **renderizado** (título grande, não tags cruas)
- [ ] O carregamento termina — não fica girando (existe um `res.end` na linha)
- [ ] Com `text/plain`, recarregar mostra as tags literalmente (teste feito)
- [ ] `charset=utf-8` está no content-type (sem ele, acentos quebram)

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. O que exatamente o `res.end()` libera o navegador?
2. Por que `writeHead` precisa vir **antes** de `write`/`end`?
3. Duas respostas idênticas, content-types diferentes: o que muda na tela do aluno?
