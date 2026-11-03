# Workshop: API da XYZ Bookstore

## Step 15 — `express.json()`: o middleware que engoliu o seu parser

---

### 📖 Teoria

O POST do Step 8 tinha um ritual: `let bruto = ""` → `req.on("data")` acumulando → `req.on("end")` → `try { JSON.parse } catch { 400 }` → resposta **lá dentro**. Cinco camadas de protocolo para ler um `{"livroId": "..."}`. O Express apaga as cinco com uma linha:

```javascript
app.use(express.json());
```

**Middleware** (conceito que nasce de verdade aqui): função que executa **no meio do caminho** entre a request chegar e o handler rodar. `app.use(fn)` é a forma de registrar; `express.json()` é um middleware **fabricado por** `express.json` (por isso os parênteses duplos: você chama o fabricante, não usa diretamente). Ele lê os chunks do body, da `JSON.parse`, e pendura o resultado em `req.body`. Seus handlers passam a tratar `req.body` como qualquer objeto:

```javascript
app.post("/carrinho", (req, res) => {
  const dados = req.body;             // já objeto, já parseado
  if (!dados.livroId || !dados.quantidade)
    return res.status(400).json({ erro: "faltam campos: livroId, quantidade" });
  const livro = livros.find((l) => l.id === dados.livroId);
  if (!livro) return res.status(400).json({ erro: "livro inexistente: " + dados.livroId });
  if (!Number.isInteger(dados.quantidade) || dados.quantidade <= 0)
    return res.status(400).json({ erro: "quantidade deve ser inteiro positivo" });
  const item = { ...dados };
  carrinho.push(item);
  res.status(201).json({ item, carrinho });
});
```

**O que o `express.json()` NÃO resolve (e você continua devendo):** validação de negócio. O `find` do `livroId`, o inteiro positivo, o `{erro}` legível — nada disso vem de fábrica. Sintaxe é problema de transporte (middleware); semântica é problema **seu**. Quem confunde as duas coisas acha que "Express valida JSON" e entrega API que aceita `{"livroId": "fantasma", "quantidade": -99}`.

**A ordem do `app.use` é a lei:** `express.json()` precisa estar registrado **antes** das rotas que usam `req.body`. Depois, não pega: middleware só atua sobre o que passa por ele na linha do tempo da request.

Um fantasma que volta: body **malformado**. O `express.json` da para o `try/catch` — mas quando ele falha, chama o *error handler* do Express, que responde 400 com... **HTML** de página de erro (não JSON! seu contrato rasgado no pior lugar). O remédio é um middleware de erro — **quatro parâmetros** (`err, req, res, next`; o quarto é o que diz ao Express "isso trata erro"):

```javascript
app.use((err, req, res, next) => {
  if (err.type === "entity.parse.failed")
    return res.status(400).json({ erro: "corpo nao e JSON valido" });
  res.status(500).json({ erro: "falha interna" });
});
```

Registre-o **por último**, depois das rotas, antes do `app.listen`.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

O agendamento da cantina com body automático:

```javascript
const express = require("express");
const app = express();

app.use(express.json()); // linha única = 30 linhas do Step 8

const cardapio = [];

app.post("/sugestoes", (req, res) => {
  if (!req.body.prato) return res.status(400).json({ erro: "faltou prato" });
  cardapio.push(req.body);
  res.status(201).json({ total: cardapio.length });
});

app.use((err, req, res, next) =>
  res.status(400).json({ erro: "corpo nao e JSON valido" })
);
```

Repare o antes/depois mental: o handler de `POST` agora **parece o GET do Step 14** — sem eventos, sem callback dentro de callback, sem `return` solto. A assincronicidade do body não sumiu do mundo: o Express a escondeu num lugar bem escolhido.

---

### ✍️ Mão na massa

1. No `app.js`, registre `app.use(express.json());` **antes** das rotas.
2. Porte o `POST /carrinho` (o bloco do texto teoria, adaptado aos seus dados: `livros`, `carrinho`) usando `req.body` direto. Sem nenhum `req.on`.
3. Porte o `POST /checkout`: sem body — o handler fica o `reduce`/`map`/`splice` do Step 10 com cara de função comum (`req` entra, `res` sai, uma passada).
4. Adicione o middleware de erro de 4 parâmetros no fim.
5. **Caça à ordem (a ferrada do Tiago, agora de propósito):** recorte o middleware de erro e cole **antes** do catch-all 404. Salve (nodemon reinicia), refaça o curl do JSON quebrado com `-H "content-type: application/json"`. O que chega? **404 "rota inexistente" em vez do 400 JSON** — o catch-all interceptou o request com erro antes dele chegar no tratador. Entenda: erro viaja pela lista como qualquer request; quem trata tem que estar **abaixo** de quem descarta. Devolva o handler para o fim e confirme o 400 de volta.
6. Teste o **trio de corpos** com `curl` e confira status E content-type com `-i`:
   - válido → 201 JSON com item+total
   - campo faltando → 400 JSON `{erro}` (a camada que o middleware **não** fez por você)
   - `curl -i -X POST localhost:3000/carrinho -H "content-type: application/json" -d 'quebrado'` → **antes** do middleware de erro: HTML de erro do Express; **depois**: 400 JSON limpo. Sem o `-H`, o `express.json` nem tenta parsear (pula body não-JSON) e quem devolve 400 é a sua validação de campos. Os dois caminhos, dois 400, origens diferentes — leia os `-i` com atenção. Sinta a diferença e mostre ao colega.

> A dor nº 2 do inventário do Step 10 (acumular chunks) acabou de morrer. Confere com a lista: sobram as dores do `if/else` de rota (resolveu Step 14) e o `split` (resolveu Step 14). A contagem de linhas do `app.js` vs `server.js` (que você anotou no Step 13) agora tem o número final — a gente cobra no 16.

---

### ✅ Critérios de verificação do Step 15

- [ ] `app.use(express.json())` aparece **antes** das rotas no arquivo
- [ ] POST `/carrinho` não contém nenhum `req.on`, `JSON.parse` ou try/catch
- [ ] As 3 validações de negócio (campos, id existente, quantidade) continuam **no seu handler**
- [ ] Body malformado responde 400 **em JSON** (não HTML)
- [ ] Você fez a caça à ordem: sabe explicar por que handler na posição errada devolve 404 em vez de 400
- [ ] Checkout funciona sem body, portado com a lógica de `reduce` intacta

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. Por que `express.json()` **antes** das rotas e o error handler **depois**? Desenhe a linha do tempo da request.
2. `req.body` de um POST com `content-type: text/plain` (nosso curl `-d 'quebrado'` sem `-H`): o que o middleware faz? (Pesquisa honesta: leia o `err.type` no handler.)
3. Qual das camadas de validação do POST o Express faz por você e qual é sua para sempre?
