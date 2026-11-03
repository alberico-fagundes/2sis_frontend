# Workshop: API da XYZ Bookstore

## Step 4 — Rotas: a URL escolhe o prato

---

### 📖 Teoria

Até agora o servidor responde **a mesma coisa** para qualquer URL. Isso não é servidor — é vitrine. Servir de verdade é: cada **endereço** (`req.url`) devolve **a coisa certa**.

A estrutura é pura lógica de decisão, exatamente um `if/else` que você já domina no frontend:

```javascript
http.createServer((req, res) => {
  if (req.url === "/livros") {
    // monta e devolve a resposta de livros
  } else if (req.url === "/autores") {
    // devolve autores
  } else {
    // nada bateu: devolve erro, NUNCA a mesma coisa de sempre
  }
});
```

| Conceito | Nome correto | Observação |
|----------|--------------|------------|
| O caminho pedido (`/livros`) | **rota** / endpoint | `req.url` traz o caminho **exato** — `/livros/` com barra final é outra string! |
| O que fazer com ele | **handler** | O bloco que escreve a resposta |
| URL que não existe | cai no `else` → erro | Responder catálogo para `/livros2` é mentir para o cliente |

> **Regra de arquitetura do workshop (vale até o React):** a API é *API-first* — endpoints devolvem **dados**, não páginas. HTML de livraria é trabalho do navegador; a cozinha serve o ingrediente, não o prato decorado. Neste step, para fixar a ideia, vamos inclusive responder `text/plain` com o **nome** do recurso — que no Step 5 vira JSON de verdade.

`req.url` ainda guarda um detalhe que veremos no Step 7: ele traz junto o que vier depois de `?` — mas as rotas de hoje comparam a string inteira.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Um servidor de horta comunitária, três endereços:

```javascript
const http = require("node:http");

http.createServer((req, res) => {
  let corpo, status = 200;
  if (req.url === "/alface") {
    corpo = "Alface: colheita toda terça.";
  } else if (req.url === "/cenoura") {
    corpo = "Cenoura: disponível no canteiro 3.";
  } else {
    status = 404;
    corpo = "Nao encontrei essa hortalica no galpao.";
  }
  res.writeHead(status, { "content-type": "text/plain; charset=utf-8" });
  res.end(corpo);
}).listen(3000);
```

Repare no padrão **uma variável de corpo → um único `writeHead`/`end` no fim**: cada rota decide a *mensagem*, o encerramento é centralizado. Menos repetição, menos chance de esquecer o `end`.

---

### ✍️ Mão na massa

1. Abra o `server.js` e adicione o parâmetro `req` de volta no callback (agora `(req, res)`).
2. Crie as três rotas com `if / else if / else` sobre `req.url`:
   - `/` → texto: `Bem-vindo a API da XYZ Bookstore`
   - `/livros` → texto: `Rota de livros - em construcao`
   - `/carrinho` → texto: `Rota do carrinho - em construcao`
   - qualquer outra → `Endereco nao encontrado`
3. Use o padrão do exemplo: monte a string na variável, defina o status (200 ou 404) e faça **um único** `writeHead` + `res.end` no fim do callback.
4. Rode (`node server.js`) e teste no navegador, um por um: `http://localhost:3000/`, `/livros`, `/carrinho`, e um endereço errado de propósito (`/xyz`).
5. Com o servidor ainda rodando, teste pelo **terminal** (abra outra aba):

```bash
curl -i http://localhost:3000/xyz
```

O `-i` mostra o cabeçalho: confirme que a linha do meio é `HTTP/1.1 404 Not Found`.

> `curl` é o navegador de linha de comando: sem interface, só o osso do HTTP. Vamos usá-lo em todos os steps — ele mostra status e headers que o navegador esconde.

---

### ✅ Critérios de verificação do Step 4

- [ ] `/`, `/livros` e `/carrinho` respondem textos **diferentes**
- [ ] `/xyz` (ou outro inexistente) responde `Endereco nao encontrado`
- [ ] `curl -i` no endereço errado mostra status `404`; nos certos, `200`
- [ ] Existe um único `writeHead`/`res.end` por request (não um dentro de cada `if`)

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. Por que responder o catálogo quando alguém pede `/livrros` (com r dobrado) seria um bug, não um favor?
2. O que `req.url` contém exatamente — a URL inteira ou só o caminho?
3. Por que centralizar `writeHead`/`end` no fim evita o travamento do Step 2?
