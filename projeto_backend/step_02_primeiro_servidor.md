# Workshop: API da XYZ Bookstore

## Step 2 — O primeiro servidor: a cozinha abre a janela

---

### 📖 Teoria

Um programa de linha (`node arquivo.js`) executa, imprime e morre. Um **servidor** precisa ficar vivo, parado na porta escutando "chegou pedido?".

Três peças obrigatórias em qualquer servidor Node puro:

| Peça | Código | O que faz |
|------|--------|-----------|
| Importar o módulo | `const http = require("node:http");` | Traz o `http` embutido do Node (não se instala com npm — já veio com ele). |
| Criar o servidor | `http.createServer(funcao)` | Registra **o que fazer** quando alguém chamar. **Não abre nada ainda.** |
| Escutar a porta | `.listen(3000)` | Aí sim: o processo para e fica ouvindo a porta 3000 da sua máquina. |

**Porta** é o "apartamento" do prédio: seu IP (ou `localhost`) é o endereço do prédio, a porta identifica qual programa atende. Porta 3000 é a convenção dos desenvolvedores para testes. Duas aplicações na mesma porta = a segunda falha com `EADDRINUSE`.

A função que você entrega para `createServer` recebe um parâmetro (o `req`, o pedido que chegou) e é **executada pelo Node a cada requisição** — você não a chama, você a **registra**:

```javascript
const http = require("node:http");

const servidor = http.createServer((req) => {
  console.log("Alguém bateu na porta!");
});

servidor.listen(3000);
console.log("Servidor no http://localhost:3000");
```

Repare: `createServer` **não devolve uma resposta ao navegador ainda** — só registra o callback. Faltar o `res.end` (que vem no Step 3) deixa o navegador **girando para sempre**: o pedido foi aceito, mas a cozinha nunca entrega o prato.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Uma portaria que anota visitas:

```javascript
const http = require("node:http");

http.createServer((req) => {
  console.log("Visita registrada: " + req.url);
}).listen(8080);

console.log("Portaria aberta na 8080");
```

Rodou? O terminal **trava** (no bom sentido): o processo está vivo escutando. Para devolvê-lo, `Ctrl + C`. Abra outro terminal e visite `http://localhost:8080/fulano` — veja o que a portaria anotou.

---

### ✍️ Mão na massa

1. Na pasta `projeto_backend`, crie `server.js` (o `catalogo.js` fica de fora deste step — dados a gente serve depois).
2. Importe o módulo `http` com `require("node:http")`.
3. Crie um servidor com `createServer` recebendo um callback com um parâmetro `req`.
4. Dentro do callback, imprima `console.log("Pedido recebido em: " + req.url)`.
5. Encadeie (ou use a variável) `.listen(3000)`.
6. Fora, imprima `console.log("XYZ Bookstore no ar em http://localhost:3000")`.
7. Rode `node server.js`. Vá ao navegador e abra `http://localhost:3000/livros`. **O navegador vai travar carregando — é esperado!** Olhe o terminal: a URL foi logada?
8. Confirme o log, então `Ctrl + C` no terminal para derrubar o servidor.

> ⚠️ Se você rodar `node server.js` e receber `EADDRINUSE`, algum servidor anterior continua vivo. Ache e derrube (outro terminal: `Ctrl + C` na janela certa, ou feche o VS Code que o segurava).
>
> **Nem toda porta ocupada é sua.** No laboratório, pode haver programa de OUTRO usuário segurando a 3000 — aí não existe `Ctrl + C` que resolva. Diagnóstico de quem está na porta:
>
> ```bash
> ss -tlnp | grep 3000
> ```
>
> Se aparecer processo que você não pode derrubar (não é seu), a saída profissional é **trocar de porta pelo código**, não brigar: `servidor.listen(process.env.PORT || 3000)` — e rodar com `PORT=3005 node server.js`. Anote a sua porta no caderno; a turma inteira vai precisar dela no Step 16 (CORS).

---

### ✅ Critérios de verificação do Step 2

- [ ] `node server.js` não termina sozinho — fica "pendurado" escutando
- [ ] Abrir `http://localhost:3000/livros` no navegador imprime o log no terminal
- [ ] A URL logada mostra `/livros` (o `req.url` traz o caminho pedido)
- [ ] `Ctrl + C` encerra o servidor sem erro

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. Qual linha faz o processo **ficar vivo**? O que aconteceria sem ela?
2. Por que o navegador girou infinitamente em vez de mostrar erro?
3. Você registrou a callback ou chamou você mesmo? Qual a diferença, quem a executa?
