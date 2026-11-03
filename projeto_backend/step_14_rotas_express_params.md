# Workshop: API da XYZ Bookstore

## Step 14 — Rotas Express: `:id`, query grátis e o 404 de fim de linha

---

### 📖 Teoria

No Step 7 você fatiou a URL com `split("/")`, indexou `partes[2]` e torceu para ninguém acrescentar `/` a mais. O Express dá nome a esse fatiamento: **parâmetro de rota**.

```javascript
app.get("/livros/:id", (req, res) => {
  // req.params.id  ->  "sally-adventure-book"
});
```

| Fase 1 | Express | O que sumiu do seu código |
|--------|---------|---------------------------|
| `split("?")` + `URLSearchParams` | `req.query` | o split e o new |
| `split("/")` + `partes[2]` | `req.params` | a contagem de índices |
| `caminho === "/livros"` | `app.get("/livros", ...)` | o if de endereço |
| `req.method === "POST" &&` | `app.post(...)` | o if de método |

`req.query` já vem parseado: `req.query.autor` é `"anne"` (ou `undefined` sem o par — o `params.get` virou acesso de objeto, mas a lógica do filtro condicional do Step 7 continua **exatamente** a mesma: `req.query.autor ? livros.filter(...) : livros`).

**A ordem das rotas importa** (a mesma do Step 6, agora imposta pelo Express, que casa a **primeira** rota que bate):

```javascript
app.get("/livros", listar);          // lista: ANTES
app.get("/livros/:id", detalhe);     // detalhe
app.use((req, res) => { ... });      // catch-all 404: SEMPRE POR ÚLTIMO
```

Se `/livros/:id` vier antes da lista, `GET /livros` casa o `:id` com... nada (não tem o segmento) — mas um `app.use` perdido no meio engole tudo. Regra de bolso: rotas **específicas primeiro**, genéricas (404) por último.

`app.use(fn)` sem caminho = "executa pra toda request que chegou até aqui". É o embrião do conceito de **middleware** que o Step 15 usa de verdade.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Portaria de eventos com rota parametrizada e filtro:

```javascript
const express = require("express");
const app = express();

const eventos = [
  { id: "show-rock", nome: "Show Rock", cidade: "POA", lotes: 5 },
  { id: "peca-teatro", nome: "Peça", cidade: "Caxias", lotes: 2 },
];

app.get("/eventos", (req, res) => {
  const lista = req.query.cidade
    ? eventos.filter((e) => e.cidade === req.query.cidade)
    : eventos;
  res.json(lista);
});

app.get("/eventos/:id", (req, res) => {
  const evento = eventos.find((e) => e.id === req.params.id);
  if (!evento) return res.status(404).json({ erro: "evento inexistente" });
  res.json(evento);
});

app.use((req, res) => res.status(404).json({ erro: "rota inexistente" }));

app.listen(3000);
```

Duas armas novas aparecem no detalhe e no 404: `res.status(404).json(...)` — o `enviar(res, status, corpo)` do Step 9, método encadeado (`res.status()` escolhe o número e devolve o `res`; `.json()` fecha). E o `return res...` do lado: em handler com validações em camadas, **retornar a resposta** é o jeito Express de dizer "chega, parei aqui" — o mesmo `return enviar(...)` que você já escrevia.

---

### ✍️ Mão na massa

1. No `app.js`, porte a rota de **detalhe**: `app.get("/livros/:id", ...)` com `find` + `req.params.id`, resposta `res.json(livro)`; se `undefined`, `res.status(404).json({erro})`.
2. Adicione o catch-all 404 **depois de todas** as rotas conhecidas: `app.use(...)` respondendo `{erro: "rota inexistente"}` com status 404.
3. Porte o **filtro** do Step 7 na rota da lista: use `req.query.autor` e o `filter` com `toLowerCase().includes` idêntico ao da Fase 1.
4. Com o `npm run dev` no ar, teste a matriz completa com `curl -i` (quatro casos, quatro status corretos):
   - `/livros` → 200 array
   - `/livros?autor=anne` → 200 array filtrado (ou vazio)
   - `/livros/sally-adventure-book` → 200 objeto
   - `/livros/nao-existe` → **404 objeto erro** • `/batatinha` → **404 rota inexistente**
5. **Caça à ordem:** mova o `app.get("/livros/:id", ...)` para **antes** do `app.get("/livros", ...)`, salve (o nodemon reinicia — o Step 12 já pagou esse favor), e teste `/livros` com `-i`: mudou alguma coisa? Explique por que o `:id` não engoliu a lista (dica: quantos segmentos tem cada caminho?). Depois, restaure.

> `req.params.id` já vem **sem** as barras, **sem** o caminho, decodificado — o `split` da Fase 1 fazia isso e mais. Cada linha que o Express apagou é uma linha a menos onde seu aluno de amanhã erraria o índice.

---

### ✅ Critérios de verificação do Step 14

- [ ] `/livros/:id` responde objeto (200) e `{erro}` 404 para id inexistente
- [ ] `/livros?autor=...` filtra sem nenhum `split("?")` no código
- [ ] Nenhuma string `req.url` aparece em nenhum handler (someu o último `split` da vida)
- [ ] O experimento do item 5 foi feito: você sabe dizer por que a ordem lista/detalhe aqui não quebrou `/livros` (segmentos!)
- [ ] 404 de rota e 404 de recurso têm mensagens **diferentes** (como devem)

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. `req.query` e `req.params`: um vem do `?`, o outro de onde? Dê o exemplo com as duas rotas do `app.js`.
2. Por que o catch-all precisa ser o **último** `app.use`/rota? O que ele engole se vier antes?
3. Seu 404 de `/livros/nao-existe` é "recurso não encontrado" e o de `/batatinha` é "endereço não existe" — qual dos dois um frontend tratiria com retry? (Pista: nenhum, mas *por que* a distinção ainda importa pra quem debug?)
