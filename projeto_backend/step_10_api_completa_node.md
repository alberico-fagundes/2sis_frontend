# Workshop: API da XYZ Bookstore

## Step 10 — FECHAMENTO DA FASE 1: a API completa, sem nenhum framework

---

### 📖 Teoria

Você tem, hoje, uma HTTP API funcional escrita com **uma biblioteca embutida e zero dependências**: catálogo com contrato, filtro, carrinho com validação. Falta o último recurso do funil da livraria do projeto2 — o botão **Checkout**: transformar carrinho em **pedido**.

Um pedido de verdade nasce de duas promessas:

1. **Total calculado no servidor, nunca no cliente.** O preço mora aqui; quem calcula total no navegador pode "editar" o preço (console do DevTools abre esse convite). O backend soma `preco × quantidade` por item e devolve o número.
2. **Efeitos colaterais explícitos.** Checkout *consome* o carrinho: depois do `200` com o resumo, `GET /carrinho` deve responder `[]`. Quem testar a API duas vezes e vir carrinho intacto, errou o `splice`.

Para calcular, entra o `reduce` — a ferramenta canônica de "array → um valor só":

```javascript
const total = itens.reduce((soma, item) => soma + item.preco * item.quantidade, 0);
```

E o carrinho fica mais inteligente ao ser **lido**: ele guarda só `{livroId, quantidade}` (o cliente mandou isso), mas `GET /carrinho` devolve itens **enriquecidos** — join manual com o catálogo, o mesmo `find` do Step 6:

```javascript
const itens = carrinho.map((c) => {
  const livro = livros.find((l) => l.id === c.livroId);
  return { ...c, titulo: livro.titulo, preco: livro.preco,
           subtotal: livro.preco * c.quantidade };
});
```

`map` + `find` + `reduce`: três métodos de array que, somados aos `if` do Step 4, **são** o seu backend — antes de qualquer Express.

> **Inventário de dores (leaia com o `server.js` aberto — é a ponte para a Fase 2):**
> 1. `if (caminho === ... && req.method === ...)` crescendo — Express chama isso de *rotas* (`app.get`, `app.post`) e o `if` some.
> 2. `split("?")` + `URLSearchParams` + acumular chunks + `JSON.parse` com try/catch — Express chama de `req.query` e `req.body`, prontos.
> 3. `enviar()` próprio, 404 próprio — Express já traz helpers e middleware.
> 4. Reboot manual a cada mudança — `nodemon` resolve antes mesmo do Express.
>
> Nada disso é "Express é mágico". É o **seu** código de hoje, embrulhado por outra pessoa — e quem escreveu por dentro sabe exatamente o que está importando.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Checkout de uma papelaria — pedido com número, total e carrinho esvaziado:

```javascript
if (caminho === "/pedidos" && req.method === "POST") {
  if (carrinho.length === 0) {
    return enviar(res, 400, { erro: "carrinho vazio: nada para fechar" });
  }
  const itens = carrinho.map((c) => { /* join com catalogo, com subtotal */ });
  const total = itens.reduce((s, i) => s + i.subtotal, 0);
  const pedido = { numero: Date.now(), itens, total }; // Date.now() = id único barato
  pedidos.push(pedido);
  carrinho.length = 0;                    // esvazia SEM sumir a referencia
  return enviar(res, 200, pedido);
}
```

Detalhe cirúrgico: `carrinho.length = 0` esvazia o **mesmo array** que a variável aponta. `carrinho = []` criaria um novo e deixaria pontas soltas se outra referência existisse. Em memória, mutate; não troque.

---

### ✍️ Mão na massa

1. Declare `const pedidos = [];` ao lado de `carrinho`.
2. Melhore o `GET /carrinho`: em vez do carrinho cru, devolva os itens **enriquecidos** (map + find, com `subtotal` por item), como no texto.
3. Crie `POST /checkout` (mesmo esqueleto assíncrono do Step 8, mas sem body: o pedido usa **este** carrinho):
   - carrinho vazio → `400 {erro: "carrinho vazio"}`
   - senão: monta itens, calcula `total` com `reduce`, cria pedido `{numero: Date.now(), itens, total}`, push em `pedidos`, esvazia carrinho, responde **200** com o pedido
4. Adicione `GET /pedidos` devolvendo o histórico.
5. Rode o ciclo completo da livraria, o "caminho do cliente" com curl:

```bash
curl localhost:3000/livros                                  # navega
curl -X POST localhost:3000/carrinho -d '{"livroId":"sally-adventure-book","quantidade":2}' -H "content-type: application/json"
curl -X POST localhost:3000/carrinho -d '{"livroId":"<outro-id>","quantidade":1}' -H "content-type: application/json"
curl localhost:3000/carrinho                                # vê itens + subtotais
curl -i -X POST localhost:3000/checkout                     # fecha: total? pedido com numero?
curl localhost:3000/carrinho                                # [] (provou o efeito colateral?)
curl localhost:3000/pedidos                                 # histórico guarda a venda
```

6. Feche com teste de honestidade: `checkout` com carrinho vazio → 400. E nenhum 400/200 sem status correto no `-i`.

**Parabéns — Fase 1 concluída.** Um arquivo `server.js`, zero `npm install`, API REST completa: GET lista, GET detalhe, filtro por query, POST validado com 201/400, checkout com cálculo e efeito colateral, erros JSON em toda rota. Você escreveu, na mão, o que o Express faz por você — no próximo módulo, com a dor catalogada, você troca conscientemente.

---

### ✅ Critérios de verificação do Step 10

- [ ] `GET /carrinho` devolve itens com `titulo`, `preco`, `quantidade`, `subtotal`
- [ ] `POST /checkout` com itens → 200, corpo com `numero`, `itens`, `total` correto (confira a soma com a calculadora!)
- [ ] Carrinho fica `[]` após checkout; `GET /pedidos` mostra o pedido
- [ ] Checkout com carrinho vazio → 400 com `{erro}` legível
- [ ] O servidor aguenta a sequência inteira sem morrer nem responder status mentiroso

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. Por que o `total` é calculado no servidor e não confiado num valor vindo do client?
2. O que `reduce` faz que `map` não faz — e por que total é trabalho do primeiro?
3. Releia o inventário de dores com o código aberto: escolha a que **mais** te irritou escrevendo. Essa é a que você vai agradecer quando o Express apagar no Step 15. (Anota a resposta — vira a primeira linha do relatório final do curso.)
