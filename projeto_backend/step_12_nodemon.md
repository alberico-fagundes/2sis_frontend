# Workshop: API da XYZ Bookstore

## Step 12 — A dor do reboot e o remédio: nodemon

---

### 📖 Teoria

Conte quantas vezes você fez isso desde o Step 2: mudou uma linha no `server.js` → `Ctrl + C` → seta-cima (`node server.js`) → recarregou o navegador. Cada ciclo ~6 segundos que o cérebro perde **no meio do raciocínio** — em 200 edições, vinte minutos e umas 40 trocas de contexto. Essa é a dor número 4 do inventário do Step 10.

O `nodemon` resolve: um programa que **vigia** a pasta e, a cada `.js` salvo, derruba e sobe o servidor sozinho. É instalado via npm — primeiro **pacote de terceiros** do curso:

```bash
npm install nodemon --save-dev
```

| Flag | Significado |
|------|-------------|
| `--save-dev` | vira `devDependencies` no package.json: ferramenta **de desenvolvimento**, não vai para produção |
| (sem flag) | viraria `dependencies`: código de que a **aplicação** precisa para rodar (como o Express no próximo step) |

A distinção é honesta: produção não precisa do vigia; precisa do Express. Errar a categoria não quebra nada hoje, mas ensina o hábito errado.

Instalado **localmente**, o binário mora em `node_modules/.bin/` — o `npm` sabe procurar ali, então o script fica:

```json
"scripts": {
  "start": "node server.js",
  "dev": "nodemon server.js"
}
```

`npm run dev` → nodemon sobe, terminal mostra `[nodemon] watching...`, e salvar arquivo reinicia sozinho (linha `[nodemon] restarting due to changes...`). Dois scripts, duas vidas: `start` = como roda de verdade; `dev` = como você trabalha.

> Conflito clássico: servidor antigo ainda na porta 3000 quando o nodemon tenta subir → `EADDRINUSE`. O nodemon não pisa em processo alheio — derrube o outro terminal. E se a resposta do navegador parecer "o código velho", confira quem está na 3000: **um** servidor, sempre.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Um site de eventos usando a mesma lógica:

```bash
npm install nodemon --save-dev
```

```json
"scripts": {
  "start": "node portal.js",
  "dev": "nodemon portal.js"
}
```

Abra `npm run dev`, edite o título no `res.end("...")`, salve (Ctrl+S) **sem tocar no terminal**: ele reinicia sozinho; recarregue o navegador e veja a mudança. O ganho não é o segundo economizado — é nunca mais perder 10 minutos procurando um "meu código não mudou" que era só servidor velho.

---

### ✍️ Mão na massa

1. Dentro de `projeto_backend`: `npm install nodemon --save-dev`.
2. Abra o `package.json`: confira que o nodemon entrou em `devDependencies` (não em `dependencies`).
3. Adicione `"dev": "nodemon server.js"` ao lado do `start` — repare na vírgula entre os scripts (JSON estrito, a lição do Step 5 vale aqui).
4. Rode `npm run dev`; mexa no `console.log` da home; salve; observe o restart automático.
5. Recarregue o navegador, confirme a mudança sem ter tocado no terminal.
6. **Armadilha pedagógica proposital:** com o `npm run dev` rodando, abra OUTRO terminal e rode `npm start`. Explique o erro (`EADDRINUSE`) para o colega ao lado — quem explica a porta nunca mais tropeça nela.
7. **E se a porta ocupada NÃO for sua?** `ss -tlnp | grep 3000` pode mostrar processo que você não tem poder de derrubar (laboratório). Solução do Step 2: `app.listen(process.env.PORT || 3000)` e `PORT=3005 npm run dev` — o nodemon respeita a variável. (Sua página de teste e o `curl` passam a usar a mesma porta nova; quem esquecer, "não entende por que o front não acha a API" — no Step 16 isso vira bug clássico.)

> O nodemon reinicia a cada salvamento — estado em memória (carrinho do Step 8) morre em cada restart. Isso é *correto* e você vai ver por quê: o servidor sem estado é o servidor que escala. Anote mentalmente: "estado volátil" ≠ "estado inexistente no banco".

---

### ✅ Critérios de verificação do Step 12

- [ ] `npm run dev` sobe o servidor; salvar um arquivo reinicia sozinho
- [ ] `nodemon` está em `devDependencies`, `package.json` continua JSON válido
- [ ] `npm start` continua funcionando (o nodemon não o substitui, o complementa)
- [ ] Você provocou o `EADDRINUSE` de propósito e sabia qual dos dois terminais derrubar

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. `--save-dev` ou nada: qual flag para o Express (próximo step) e por quê difere do nodemon?
2. O que acontece com o carrinho entre 2 reinícios do nodemon? Por que isso importa quando existir banco?
3. Por que o binário roda `nodemon` sem você instalar nodemon *no sistema*? (O `npm run` sabe onde?)
