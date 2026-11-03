# Workshop: API da XYZ Bookstore

## Step 18 — O primeiro fio: a página do projeto2 lê a sua API

---

### 📖 Teoria

> **Pré-requisito:** Step 16b (ponte JS na página). `querySelector`, `innerHTML`, `addEventListener` e delegação já devem estar na mão — aqui eles encontram o dado que vem de fora.

Aqui as metades se encontram: o **HTML que você escreveu à mão no projeto2** passa a ser **gerado a partir dos dados do app.js**. Uma linha de código costura os dois mundos:

```javascript
const resposta = await fetch("http://localhost:3000/livros");
```

`fetch` é o `fetch` do navegador (o mesmo que testamos no Step 16 no `teste-frete.html` — ele agora trabalha de verdade). Fluxo completo do pedido, com as mãos de JS simples que você já tem:

```javascript
fetch("http://localhost:3000/livros")
  .then((res) => res.json())          // corpo bruto -> objeto (parse do lado do CLIENTE)
  .then((livros) => {
    const container = document.querySelector(".card-container");
    container.innerHTML = "";         // os cards estáticos deram lugar aos dados
    livros.forEach((livro) => container.insertAdjacentHTML("beforeend", montarCard(livro)));
  });
```

Quatro conceitos novos, um por frase:

| Novo | Onde já morava | Agora |
|------|----------------|-------|
| `fetch` | `createServer` (você era o servidor!) | você é o **cliente** do pedido HTTP |
| `res.json()` | `JSON.stringify` | inverte o polo: **parse** no consumidor |
| Promises (`.then`) | `req.on("end")` | mesma espera, com cara de correnteza |
| `innerHTML`/`insertAdjacentHTML` | tags digitadas no editor | tags **geradas** a partir de dados |

**De onde vem o HTML gerado?** Do mesmo contrato que você escreveu no projeto2 — cada card gerado reproduz `div.card` com `id` do livro, `h3` título, `p` autor/descrição e `button.btn`. Só que agora com um `<p class="preco">` que a página estática **não tinha**: o preço passou a existir no servidor e a aparecer na tela. Bem-vindo ao motivo de existir backend.

Dois avisos de engenharia (não decorre, entende):

1. **`innerHTML` com dado do usuário é convite a injeção de script.** Hoje o catálogo é seu, fixo — seguro. Com dado de fora, o caminho é `createElement` + `textContent` (ou frameworks, como o React da Fase 4, que escapam disso por design).
2. **Origem:** a página servida pelo Live Server (`5500`) é outra origem da API (`3000`) — o `cors()` do Step 16 é o que permite esse diálogo. Sem ele, este step inteiro falha no console.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Página de petshop consumindo uma lista de produtos e montando listas simples:

```javascript
async function carregarProdutos() {
  const res = await fetch("http://localhost:3000/produtos");
  const produtos = await res.json();
  const ul = document.getElementById("lista");
  ul.innerHTML = "";
  produtos.forEach((p) => {
    ul.insertAdjacentHTML("beforeend", `
      <li>
        <strong>${p.nome}</strong> — R$ ${p.preco.toFixed(2)}
        <button data-id="${p.id}">Reservar</button>
      </li>`);
  });
}
carregarProdutos();
```

Notas: `async/await` no lugar das `.then` — **a mesma coisa**, só sem correntes (o Node do Step 8 ensinou que esperar é normal). `data-id="${p.id}"` guarda o id do recurso **no botão**, pronta para o POST do próximo bloco. `toFixed(2)` é cosmético: número no dado, texto formatado na tela — nunca se faz conta com `toFixed`.

---

### ✍️ Mão na massa

1. Prepare a cena: **copie** a página final do projeto2 (aquela do Step 19, com `card-container`, 2 cards e `btn-container`) para `projeto_backend/pagina/` e crie `pagina/script.js` vazio. No `index.html` da cópia, antes do `</body>`: `<script src="script.js"></script>`.
2. No `script.js`, escreva o carregamento do Step: `fetch` da rota de lista, `res.json()`, e dentro do `.then` (ou `async` seu): limpar `.card-container` e gerar um card por livro — reproduzindo a estrutura do projeto2 (`div.card` com `id` do livro, `h3`, `p` autor, `p` descrição, `p.preco` com o valor formatado, `button.btn` "Buy Now" com `data-id` do livro).
3. Suba a API (`npm run dev`, 3000) e sirva a página (botão direito → Open with Live Server, 5500). Recarregue: **os cards agora vêm do `app.js`, não do HTML** — mude o `preco` de um livro no servidor, salve, recarregue a página: o preço mudou **sem tocar no HTML**. Isso é o contrato funcionando.
4. Fio de ida: dê aos "Buy Now" o que ainda falta — ouvir cliques e postar:

```javascript
// DELEGAÇÃO: um ouvinte só, num container que nunca some (o innerHTML vai e vem, ele fica)
document.querySelector(".card-container").addEventListener("click", async (evento) => {
  const btn = evento.target.closest(".buy-now");
  if (!btn) return; // o clique não foi num botão — ignora em paz
  const res = await fetch("http://localhost:3000/carrinho", {
    method: "POST",
    headers: { "content-type": "application/json" },
    body: JSON.stringify({ livroId: btn.dataset.id, quantidade: 1 }),
  });
  if (!res.ok) {                    // 400/404 NAO é exceção — fetch só quebra na rede
    const { erro } = await res.json();
    return console.log("RECUSADO PELO SERVIDOR:", erro);
  }
  const d = await res.json();
  console.log("no carrinho:", d.carrinho.length);
});
```

   Clique num "Buy Now", olhe o console, confirme com `curl /carrinho`.

> **Os dois sabores de "deu ruim"** (a Júlia, aluna real da turma, tropeçou aqui): `fetch` **só** entra no `catch` quando a rede falha (API desligada, CORS, URL errada). Se o servidor respondeu — mesmo 400/404/500 — o `fetch` considera **sucesso** e te entrega a resposta de braço aberto: quem checa o status é você, com `if (!res.ok)`. Front que não checa `res.ok` **engole erro silenciosamente**: o 400 `{erro}` bonito que você produziu no Step 9 morre sem ninguém ler. E o motivo da delegação ser oficial: botões criados por `innerHTML` depois de `addEventListener` não existem ainda — o listener grava em fantasma; e um listener por botão renasce a cada re-render, duplicando cliques.
5. Teste de honestidade do circuito: `?autor=ninguem` na rota — a tela fica vazia **sem erro**? (O front tratou 200+`[]` como promessa cumprida, não como exceção.)

> Se o console acusar CORS ou "Failed to fetch", o passo-a-passo do Step 16 resolve: API viva na porta certa? `cors()` registrado? página servida por http (não file://)?

---

### ✅ Critérios de verificação do Step 18

- [ ] Os cards da tela são gerados pelo `fetch` (apagar os cards estáticos do HTML não muda a tela)
- [ ] Trocar dado no `app.js` muda a tela sem editar HTML (teste 3 feito)
- [ ] Cada card tem `id`/`data-id` batendo com o `id` do contrato (`sally-adventure-book`...)
- [ ] Clicar "Buy Now" gera POST 201 e o item aparece no `GET /carrinho` do curl
- [ ] O handler do botão checa `res.ok` e imprime o `{erro}` — teste postando `livroId` inexistente e VEJA a mensagem no console
- [ ] O listener de compra está no **container** (delegação), não em botão individual — re-render não duplica clique
- [ ] Nenhum erro de CORS no console (o `cors()` trabalhando visivelmente)

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. `JSON.stringify` apareceu em qual lado do POST? E `res.json()` — em quem? (Servidor x cliente, ida x volta.)
2. Por que o listener vive no **container** e não nos botões? O que acontece com `addEventListener` dado em botão que ainda não existia quando a linha rodou?
3. O preço existia no HTML do projeto2? Existia no contrato? Onde ele "morava" antes e onde mora agora?
4. Servidor responde 400 `{erro}` — por que o `catch` do `fetch` NÃO pega isso? Quem é o responsável por olhar `res.ok`?
