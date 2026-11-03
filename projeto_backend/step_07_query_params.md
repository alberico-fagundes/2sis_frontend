# Workshop: API da XYZ Bookstore

## Step 7 — Query params: o cliente escolhe o filtro, não o servidor

---

### 📖 Teoria

`GET /livros` devolve tudo. Mas o cliente quer "só os da Anne". Ele não merece uma rota nova por autor (`/livros/anne`, `/livros/machado`...) — ele quer **filtrar**. Filtro via URL tem sintaxe própria:

```
GET /livros?autor=anne&genero=aventura
    └─caminho─┘└────────query string────────┘
```

| Peça | Nome | Como se lê |
|------|------|------------|
| `?` | abre a consulta | "a partir daqui, são parâmetros, não endereço" |
| `autor=anne` | par `chave=valor` | |
| `&` | cola outro par | `chave=valor&chave2=valor2` |

**A bomba que isso planta no seu código do Step 6:** `req.url` traz **a linha inteira** — `/livros?autor=anne` — e aquele `=== "/livros"` **para de casar**! A rota que estava perfeita no step anterior quebra silenciosamente com filtro. Flag no navegador em `/livros?x=1`: se aparecer 404, você acabou de sentir a dor ao vivo.

Remédio em duas etapas:

```javascript
const [caminho, query] = req.url.split("?"); // "/livros?autor=anne" -> "/livros" + "autor=anne"
const params = new URLSearchParams(query || ""); // objeto de consultas
params.get("autor"); // "anne"  (ou null se o par não veio)
```

- `split("?")` separa **endereço** de **consulta**; suas rotas passam a comparar `caminho` (nunca mais `req.url` cru).
- `URLSearchParams` é embutido do Node — parseia a query sem regex. `.get("chave")` devolve o valor **ou `null`** quando o parâmetro não foi enviado. Filtro é sempre **opcional**: sem `?autor=`, a rota devolve tudo (contrato do Step 6 não muda).

Filtrar é o método de array que você já tem: `filter` devolve array (zero, um ou muitos — o cliente sempre recebe array, promessa mantida).

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Uma API de biblioteca com consulta opcional por ano:

```javascript
const http = require("node:http");

const acervo = [
  { titulo: "1984", ano: 1949 },
  { titulo: "Duna", ano: 1965 },
  { titulo: "Neuromancer", ano: 1984 },
];

http.createServer((req, res) => {
  const [caminho, query] = req.url.split("?");
  const params = new URLSearchParams(query || "");

  let corpo;
  if (caminho === "/livros") {
    const ano = params.get("ano"); // null se não veio
    const lista = ano ? acervo.filter((l) => String(l.ano) === ano) : acervo;
    corpo = JSON.stringify(lista);
  } else {
    corpo = JSON.stringify({ erro: "rota inexistente" });
  }

  res.writeHead(200, { "content-type": "application/json; charset=utf-8" });
  res.end(corpo);
}).listen(3000);
```

Ponto-chave: `params.get` pode devolver `null`, por isso o `ano ? filtra : devolve tudo`. Comparação de número vindo de URL é **comparação de texto** (`String(l.ano) === ano`) — URL não tem tipo numérico.

---

### ✍️ Mão na massa

1. No `server.js`, antes do primeiro `if`, extraia `caminho` e `query` com `split("?")` e monte o `URLSearchParams` (garanta `|| ""` para quando não houver `?`).
2. Troque **todas** as comparações `req.url === ...` por `caminho === ...`. As rotas do Step 6 passam a funcionar com ou sem query.
3. Na rota do catálogo (`/livros`), leia `params.get("autor")` e, se vier valor, filtre com `filter` comparando `l.autor.toLowerCase().includes(autor.toLowerCase())`. Sem parâmetro → array completo.
4. Adicione `?genero=`? Ainda não — seus livros não têm esse campo. (Tarefa de casa opcional: adicionar campo `genero` ao catálogo e mais um filtro.)
5. Teste os quatro casos com `curl` (e confirme os status no `-i`):
   - `/livros` → todos
   - `/livros?autor=<parte de um autor>` → só os que batem
   - `/livros?autor=ninguem` → `[]` (array vazio — **status 200**, não 404: a rota existe, o filtro que não casou)
   - `/livros/sally-adventure-book?x=1` → o detalhe ainda funciona (rota parametrizada agora usa `caminho`)

> Pergunta de prova que cai hoje: filtro sem resultado é `[]` com 200 ou 404? R: **200 + array vazio**. 404 significa "o *endereço* não existe", não "estoquei zero itens".

---

### ✅ Critérios de verificação do Step 7

- [ ] Nenhuma rota compara `req.url` cru — todas usam `caminho`
- [ ] `/livros?autor=qualquer` responde filtro, `/livros` responde tudo
- [ ] Filtro sem match responde `[]` com status 200
- [ ] `/livros/:id?id... ` com query bobagem ainda devolve o livro (rota detalhe não ligou pra query)

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. Por que `=== "/livros"` quebrou quando você digitou `/livros?autor=...`?
2. O que `params.get("autor")` devolve se o cliente chamar `/livros` pura? Como o seu `if` usa isso?
3. Filtro com 0 resultados: por que **não** é 404? Dê um exemplo da vida real (busca no site que retorna "nada encontrado" — a página é 200 ou 404?).
