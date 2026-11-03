# Workshop: API da XYZ Bookstore

## Step 17 — O contrato: a API vira especificação escrita

---

### 📖 Teoria

Nos steps anteriores, a API existia **no seu `app.js`** e no conhecimento da sua cabeça. A partir de agora ela passa a existir **no papel** — e essa distinção é o que permite duas equipes (ou dois "você": o do backend de hoje e o do React da Fase 4) trabalharem sem se tocar.

**Contrato de API** = documento que declara, para cada endpoint:

| Item | Pergunta respondida |
|------|---------------------|
| Rota | Qual caminho? (`/livros/:id`) |
| Método | Qual verbo? (`GET`, `POST`...) |
| Body | O cliente precisa mandar algo? Com que campos? |
| Sucesso | Qual status + qual corpo? (`201 {item, carrinho}`) |
| Erros | Cada 4xx possível e sua mensagem? |

O seu `app.js` da Fase 2 já implementa, sem estar escrito, exatamente este contrato:

| # | Rota | Método | Body | OK | Erros |
|---|------|--------|------|----|-------|
| 1 | `/livros` | GET | — | 200 `[{livro}]` | — |
| 2 | `/livros?autor=X` | GET | — | 200 `[{filtrados}]` (pode `[]`) | — |
| 3 | `/livros/:id` | GET | — | 200 `{livro}` | 404 `{erro}` |
| 4 | `/carrinho` | GET | — | 200 `[{item com subtotal}]` | — |
| 5 | `/carrinho` | POST | `{livroId, quantidade}` | 201 `{item, carrinho}` — **`item` já enriquecido** (`titulo`, `subtotal`): quem POSTA recebe o item pronto pra tela, sem pedir `GET` atrás e sem raspar título do DOM | 400 faltando campo / id inexistente / quantidade inválida / JSON quebrado |
| 6 | `/checkout` | POST | — | 200 `{numero, itens, total}` | 400 carrinho vazio |
| 7 | *(qualquer outra)* | * | — | — | 404 `{erro: "rota inexistente"}` |

Repare nas **três promessas estruturais** que o contrato congela — as mesmas que o React vai exigir intactas:

1. **Lista é sempre array, mesmo vazia.** O consumidor fará `.map` sem checar tamanho.
2. **Erro é sempre objeto `{erro: "texto útil"}`.** O consumidor fará `res.ok ? ... : dados.erro`. Se um endpoint voltar 404 em texto puro, o `res.json()` do front **estoura exceção** — o contrato quebrado não xinga, ele quebra o outro lado.
3. **Toda célula da tabela é testável.** "Sucesso = qual status + qual corpo" não aceita "responde alguma coisa do item": se o consumidor precisa de um campo, o campo nasce escrito aqui. (A Júlia, aluna real da turma, precisou inventar de onde tirar o `titulo` do "Adicionado" porque a versão antiga desta tabela dizia só `{item, carrinho}` — contrato omisso é contrato quebrado em câmera lenta.)

**O exercício do step não é escrever código: é escrever a tabela acima no caderno/arquivo e depois *auditar* o `app.js` contra ela** — método, status e corpo, endpoint por endpoint, com `curl -i` na mão. Auditoria de contrato é profissão; aqui é treino.

> Ferramentas que fazem isso de verdade existem (`swagger`/`openapi`) — e quando você chegar nelas, vai estar *convertendo* um contrato que já sabe ler. Nada decorativo em ordem de aula.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Auditoria de contrato de uma API de biblioteca alheia. Linha do documento do fornecedor:

> `POST /reservas` — body `{livroId, leitorId}` — 201 `{reserva}` — 400 `{erro}` se faltarem campos — 404 `{erro}` se `livroId` inexistente.

Teste de conformidade com curl (o papel do auditor): enviar as **três** situações e conferir status E corpo de cada:

```bash
curl -i -X POST .../reservas -H 'content-type: application/json' -d '{"livroId":"x"}'
# esperado: 400, corpo JSON nomeando o campo faltando.
# se vier 500 HTML: contrato violado — abrir bug, não "tentar de novo diferente".
```

O achado feio de auditoria de verdade quase nunca é "funciona ou não funciona": é **"funciona, mas não como prometeu"**.

---

### ✍️ Mão na massa

1. Copie a tabela de contrato deste step para um arquivo `CONTRATO.md` na pasta `projeto_backend` (sua API, sua versão — ajuste os campos de livro aos reais do seu catálogo).
2. Com `npm run dev` no ar, rode a bateria de auditoria, **cada linha com `-i`** para ver status, e confira contra o `CONTRATO.md`:

```bash
curl -i localhost:3000/livros
curl -i "localhost:3000/livros?autor=ninguem"        # 200 + []
curl -i localhost:3000/livros/sally-adventure-book    # 200 + objeto
curl -i localhost:3000/livros/x                       # 404 JSON
curl -i -X POST localhost:3000/carrinho -H 'content-type: application/json' -d '{"livroId":"sally-adventure-book","quantidade":2}'
curl -i -X POST localhost:3000/carrinho -H 'content-type: application/json' -d '{"livroId":"x","quantidade":1}'
curl -i localhost:3000/carrinho
curl -i -X POST localhost:3000/checkout
curl -i -X POST localhost:3000/checkout                # agora: 400 carrinho vazio
curl -i localhost:3000/nada                            # 404 rota
```

3. Marque no `CONTRATO.md` ao lado de cada linha: ✔ auditado ou ✘ com o desvio descrito. **Um desvio encontrado e consertado no código vale mais que dez ✔.**
4. Rode a bateria **duas vezes seguidas** e compare: a segunda corrida começa com carrinho `[]`? (Checkout zera — efeito colateral do contrato 6 é visível na releitura.)

> O `CONTRATO.md` será o documento de entrada da Fase 4: o aluno de React programa **contra a tabela**, sem ler uma linha do `app.js`. É esse o objetivo de "API congelada" que você leu no roadmap.

---

### ✅ Critérios de verificação do Step 17

- [ ] `CONTRATO.md` existe com as 7 linhas (rota, método, body, OK, erros) preenchidas do SEU app
- [ ] A bateria de 10 curls foi executada, todos os status conferidos com `-i`
- [ ] Filtro sem match: `200 []` (não 404) — auditado
- [ ] Checkout duas vezes: segunda chamada responde 400 `{erro}` (estado mudou) — auditado
- [ ] Nenhum endpoint devolve erro em HTML/texto (todos `{erro}` JSON)

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. O que quebra no front (Fase 4) se `/carrinho` vazio resolver voltar `{}` em vez de `[]`?
2. Contrato diz `400 {erro}` mas o código devolve 500 HTML: qual dos dois está errado — o auditor ou o programador?
3. Por que auditar com `curl -i` e não no navegador? (Dois motivos: status visível, e sem cache.)
