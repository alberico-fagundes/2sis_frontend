# Workshop: API da XYZ Bookstore

## Step 16 — CORS: a permissão que o React vai exigir (e o fechamento da Fase 2)

---

### 📖 Teoria

**Mesma origem** = protocolo + host + porta idênticos. `http://localhost:3000` e `http://localhost:5173` são **portas diferentes = origens diferentes** — e a política do navegador proíbe o JS rodando numa de **ler** dados da outra. Isso é o **CORS** (*Cross-Origin Resource Sharing*): não é bug do Node, não é medo — é o navegador protegendo o usuário, e ele vai te barrar no dia em que o front (Vite:5173, Live Server:5500) chamar a API (Node:3000).

Como se manifesta (decorar o sintoma economiza uma hora de lagarta):

```
Access to fetch at 'http://localhost:3000/livros' from origin
'http://localhost:5173' has been blocked by CORS policy:
No 'Access-Control-Allow-Origin' header is present...
```

Consola do navegador, `fetch` falha **depois** de o servidor responder. Sim: o servidor atendeu normalmente — quem bloqueou foi o **navegador**, ao ler a resposta sem o carimbo de permissão. É por isso que o `curl` nunca sentiu CORS (curl não é navegador, não aplica a política).

O conserto é do **servidor**: ele passa a enviar o header `Access-Control-Allow-Origin: http://localhost:5173` (ou `*` em API pública de aula). Fazer isso na mão para todos os casos (métodos, headers, preflight) é um trabalho chato de 20 linhas — então usa-se o middleware da casa, a lição do Step 13 se repetindo:

```bash
npm install cors
```

```javascript
const cors = require("cors");
app.use(cors()); // registro: a mesma mecânica do express.json (Step 15)
```

**Preflight** (só para saber que existe, não para decorar): POST com `content-type: application/json` faz o navegador enviar antes um `OPTIONS` de sondagem — "posso te mandar isso?". O middleware `cors` também responde o OPTIONS sozinho. Sem ele, o POST do front morre no OPTIONS que você nem viu nos logs do curl.

`cors()` puro libera tudo (`*`) — aceitável para aula, **não** para produção (a regra real: lista fechada de origins). Você vai saber consciously que está usando a versão larga; é o suficiente nesta fase.

> **Nota histórica (o `express.static` que não existiu):** poderíamos ter pedido ao Express servir o `index.html` do projeto2 (API e página no mesmo lugar, CORS zero). Optamos por **API-first**: o servidor serve dados, o cliente serve a tela — porque a Fase 4 (React/Vite) vai servir a página em outra porta de qualquer forma. O static seria um atalho que a Fase 4 jogaria fora.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

A API da horta (portada p/ Express nos steps anteriores) + o primeiro "cliente cross-origin" sem framework:

```javascript
const express = require("express");
const cors = require("cors");
const app = express();

app.use(cors());
app.get("/hortalias", (req, res) => res.json([{ id: "alface" }]));
app.listen(3000);
```

Página de teste **servida de outra origem** (Live Server na 5500, por exemplo) tentando ler a API:

```html
<script>
  fetch("http://localhost:3000/hortalias")
    .then((r) => r.json())
    .then((d) => document.body.insertAdjacentHTML("beforeend", "<pre>" + JSON.stringify(d) + "</pre>"))
    .catch((e) => console.log("BLOQUEADO (ou API fora do ar):", e.message));
</script>
```

Sem `app.use(cors())`: console mostra o erro de CORS policy, `<pre>` vazio, e o `catch` roda. Com ele: os dados aparecem. **Mesmo código de front** — a mudança foi 100% no servidor. Guarde: é exatamente esse par de comportamentos que a Fase 4 vai reproduzir com o React.

---

### ✍️ Mão na massa

1. `npm install cors`. No `app.js`: `const cors = require("cors");` e `app.use(cors());` **antes** das rotas (logo acima/abaixo do `express.json()` — a ordem entre os dois é indiferente; a lei é: antes das rotas).
2. Crie `teste-frete.html` (um HTML mínimo com o `<script>` do exemplo adaptado p/ `http://localhost:3000/livros` — é o primeiro JS do curso que roda no **navegador**, não no terminal).
3. Sirva esse arquivo de **outra porta**: VS Code + Live Server (5500), ou `npx serve` (3001) — nunca abra por `file://` (origem `null` confunde o diagnóstico; aprenda primeiro o certo).
4. Rode os dois: API na 3000 (`npm run dev`), página na 5500. Abra o DevTools (F12) na página: **antes** de adicionar o cors (comente a linha, o nodemon reinicia — Step 12 pagou): erro CORS no console. **Depois** (descomente): livros na tela.
5. Teste o POST cross-origin: no mesmo `teste-frete.html`, botão que faz `fetch(".../carrinho", {method:"POST", headers:{"content-type":"application/json"}, body: '{"livroId":"sally-adventure-book","quantidade":1}'})` → sem cors, morre no preflight; com cors, 201 aparece no console.
6. **Fechamento da Fase 2 — o relatório de uma linha:** abra `server.js` (Fase 1) e `app.js` (Fase 2) lado a lado (o museu do Step 13). Conte as linhas de cada um, anote a diferença. E responda a si mesmo a pergunta guardada do Step 10: *qual dor te irritou mais escrevendo na mão, e qual linha do Express apagou ela?*

> Se o `curl` funcionar e o navegador falhar com CORS, você acabou de presenciar a prova de que a política é do **navegador**, não do servidor. Guarde a cena — ela vai aparecer em todo projeto de aluno na Fase 4.

---

### ✅ Critérios de verificação do Step 16

- [ ] A página servida em outra origem lê `/livros` **sem erro de CORS** no console
- [ ] O POST cross-origin passa (preflight respondido sozinho pelo `cors`)
- [ ] `cors` está em `dependencies` (é código de runtime, não de dev — categoria que você já sabe justificar)
- [ ] O erro de CORS foi visto **de propósito** (com a linha comentada) antes do remédio
- [ ] `app.js` vs `server.js`: contagem de linhas registrada + a "dor nº 1" do Step 10 apontada no código que a resolveu

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. O servidor respondeu `200` mas o navegador mostrou bloqueio — quem, exatamente, descartou a resposta?
2. Por que `curl` nunca vê CORS?
3. Por que NÃO usamos `express.static` para servir a página do projeto2? (Resposta esperada: a palavra "Fase 4".)
