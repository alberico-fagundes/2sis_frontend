# Workshop: API da XYZ Bookstore

## Step 19 — DESAFIO FINAL: a loja inteira funcionando (sem passo a passo)

---

### 🎯 O Briefing

A partir daqui **não existe exemplo**. Existe especificação, critérios de aceite e o que você construiu nos steps 01 a 18. Este é o formato real de trabalho: um chamado abre ticket com requisitos, ninguém te dá o código — o contrato do Step 17 e a sua memória são as ferramentas.

**Missão:** fechar o funil completo da livraria — navegar, adicionar, **ver o carrinho, remover item, finalizar checkout** — com os dois lados conversando sozinhos.

---

### 📦 Escopo 1 — Backend: uma rota nova

`DELETE /carrinho/:id` (o `:id` é o **livroId**, contrato 5 invertendo o efeito):

- item existe no carrinho → remove, responde `200` com o carrinho restante (formato enriquecido da rota 4)
- item não existe → `400` com `{erro}` (a culpa é do corpo do pedido? não: da referência. Decida 400 ou 404 e **defenda oralmente** a escolha — o professor vai perguntar exatamente isso)
- adicione a linha ao `CONTRATO.md` **antes** de codar (contrato primeiro, código depois — ordem profissional)

### 📦 Escopo 2 — Frontend: dois botões ociosos desde o projeto2

Na página do Step 18, ligue os botões que esperam por isso desde o workshop de HTML:

**`#view-cart-btn`** → `GET /carrinho` e renderizar os itens com subtotal em uma `<div id="carrinho-view">` criada por você; **cada item com botão "remover"** que chama a rota DELETE e re-renderiza.

**`#checkout-btn`** → `POST /checkout`; sucesso: mostrar `{numero, total}` na tela e limpar a carrinho-view; 400 carrinho vazio: mostrar a mensagem do `{erro}` **na tela**, não só no console (regra de UX: erro que o usuário não vê não existe).

### 📦 Escopo 3 — O ciclo completo, provado

1. Recarregar a página → lista do servidor (08 do contrato)
2. Clique "Buy Now" ×3 em livros diferentes → `curl /carrinho` mostra 3 itens enriquecidos
3. Clique em "Ver carrinho" → os mesmos 3 na tela, com subtotais corretos (soma na calculadora de um deles)
4. Remova 1 → tela atualiza sem refresh; `curl` confirma
5. "Checkout" → pedido com `numero` e `total`; carrinho na tela **e** no servidor fica vazio
6. "Checkout" de novo → a tela mostra a mensagem de erro (400) legível
7. Console do DevTools: **zero erros** o ciclo inteiro
8. API (3000) e página (5500) nunca trocaram uma linha de HTML entre si — a página só **pediu** e **mostrou**

---

### ✅ Critérios de aceite (assinatura do professor = cada linha demonstrada ao vivo)

- [ ] `CONTRATO.md` tem a linha DELETE preenchida **antes** da rota existir
- [ ] DELETE remove, responde carrinho restante, e o 400/404 escolhido é justificado verbalmente
- [ ] view-cart, remover e checkout funcionam na página, sem refresh manual do browser
- [ ] Erros 400 aparecem na interface (não só console)
- [ ] O ciclo 1–8 foi demonstrado sem restart da API em nenhum momento
- [ ] `git` da alma: ao fim, você sabe apontar cada feature e **dizer o step onde ela nasceu** (filtro→07, POST→08, 400→09, total→10, `:id`→14, body automático→15, cross-origin→16, render de dados→18)

---

### 🧠 Relatório de formatura (entregue junto com a demonstração — 3 perguntas, 1 parágrafo cada)

1. **A pergunta guardada desde o Step 10:** qual dor do `node:http` puro te irritou mais, e qual linha exata do Express a apagou?
2. **A pergunta do Step 6:** o que mudou no `app.js` quando a página do projeto2 virou "Fase 1"? (Esperada: **nada** — e por que isso é a prova de que a API-first valeu a pena.)
3. **A pergunta da Fase 4:** quando o React consumir esta API, o que o servidor precisa fazer? (Esperada: nada. E agora você pode citar o CORS do Step 16 e o contrato do 17 como as duas razões.)

---

> **Backend do workshop: CONGELADO.** A partir deste step o `app.js` é intocável — a Fase 4 (React) só troca o **cliente**. Se um dia um bug obrigá-lo a mexer, abra uma issue no `CONTRATO.md` antes. Você acabou de experimentar a sensação de "o servidor está pronto": ela dura exatamente até o primeiro usuário real.
