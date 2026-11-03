# Workshop: API da XYZ Bookstore

## Step 9 — Status codes: a API para de fingir que está tudo bem

---

### 📖 Teoria

No Step 8 você postou `{"livroId": "nao-existe"}` e o servidor **aceitou de sorriso no rosto**. Isso ébug com diploma: o cliente recebe `200 OK` e um carrinho envenenado. Uma API madura **mente sobre status nenhum** — o código numérico da resposta é a fala honesta do servidor:

| Status | Nome | Quando usar |
|--------|------|-------------|
| `200` | OK | Deu certo, tem corpo pra entregar |
| `201` | Created | Deu certo e **criou** um recurso (POST que adiciona item) |
| `400` | Bad Request | O **cliente** errou: JSON quebrado, campo faltando, quantidade negativa |
| `404` | Not Found | O **recurso do endereço** não existe (rota errada, id inexistente) |
| `500` | Internal Server Error | O **servidor** errou (bug, banco caiu). Cliente não tem culpa |

A régua: **4xx = culpa de quem pediu; 5xx = culpa de quem respondeu.** Errar a categoria faz o frontend tratar retry do jeito errado (400 não adianta repetir igual!).

O `400` do body quebrado tem motor conhecido: `JSON.parse` de string inválida **lança exceção**. Sem tratamento, a exceção derruba o servidor Node — o processo **morre** no `curl` malicioso. O remédio é o `try/catch`:

```javascript
try {
  const dados = JSON.parse(bruto);
} catch {
  return enviar(res, 400, { erro: "JSON malformado" });
}
```

Validação de negócio (as outras portas de entrada do 400): `livroId` existe no catálogo? `quantidade` é número inteiro positivo? Cada porta negada devolve 400 com `{erro: "motivo legível"}` — o cliente corrige e reenvia.

> **A ferrada antes do remédio (o Tiago, aluno real da turma, caiu aqui):** a validação *ingênua* `if (!dados.quantidade || dados.quantidade <= 0)` parece correta — mas `quantidade: "2"` (string, como vem de um `<input>`) **passa**: `"2" <= 0` é `false` e `!"2"` é `false`. O servidor aceita e o subtotal vira `10210210...` — `"39.9" * "2"` funciona, mas `preco + quantidade` **concatena texto**. URL e `<input>` só entregam *string*; "é número?" é validação **de tipo**, não de existência — e existe um teste exato para isso:
>
> ```javascript
> Number.isInteger(dados.quantidade) && dados.quantidade > 0 // "2" -> false | 2.5 -> false | -2 -> false | 0 -> false | 3 -> true
> ```

**Refatoração do step:** o `writeHead`+`end` repetido em 8 lugares vira um helper — DRY, e o status fica explícito em cada chamada:

```javascript
function enviar(res, status, corpo) {
  res.writeHead(status, { "content-type": "application/json; charset=utf-8" });
  res.end(JSON.stringify(corpo));
}
```

Toda resposta do servidor passa por `enviar`. Se algum `res.end` sobreviver solto no código, é bug esperando.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Um API de agendamento de consultas recebendo POST validado em camadas:

```javascript
function criarAgendamento(req, res) {
  let bruto = "";
  req.on("data", (p) => { bruto += p; });
  req.on("end", () => {
    let dados;
    try {
      dados = JSON.parse(bruto);                 // camada 1: é JSON?
    } catch {
      return enviar(res, 400, { erro: "corpo nao e JSON valido" });
    }
    if (!dados.paciente || !dados.medico) {      // camada 2: campos obrigatórios?
      return enviar(res, 400, { erro: "faltam campos: paciente, medico" });
    }
    const dr = medicos.find((m) => m.id === dados.medico); // camada 3: referência existe?
    if (!dr) {
      return enviar(res, 400, { erro: "medico inexistente: " + dados.medico });
    }
    const agendamento = { id: gerarId(), ...dados };
    agenda.push(agendamento);
    enviar(res, 201, agendamento);               // criou -> 201, corpo = o recurso novo
  });
}
```

Sequência deliberada: **sintaxe → campos → negócio**. A mais barata primeiro; um pedido ruim sai rápido e com motivo específico (`"faltam campos"` ensina o cliente certo, `"erro"` não ensina nada).

---

### ✍️ Mão na massa

1. Crie o helper `enviar(res, status, corpo)` no topo do `server.js` e **substitua** todo `writeHead`+`end` por chamadas a ele.
2. No `POST /carrinho`, monte as três camadas de validação dentro do `req.on("end")`:
   - `try/catch` no `JSON.parse` → 400 `{erro: "corpo nao e JSON valido"}`
   - `livroId` ausente **ou** `quantidade` ausente → 400 com `{erro}` nomeando o campo faltante
   - `livros.find(l => l.id === dados.livroId)` retornando `undefined` → 400 `{erro: "livro inexistente: <id>"}` (é 400, **não** 404: o endereço `/carrinho` existe, o dado do corpo que está errado)
   - `quantidade` falhar no teste `Number.isInteger(dados.quantidade) && dados.quantidade > 0` → 400 (corta string `"2"`, float `1.5`, `0` e negativo de uma vez)
3. Sucesso: `carrinho.push(...)`, então `enviar(res, 201, { item, carrinho })` — criado, 201.
4. Teste as 6 portas com `curl` (cada uma com `-i` para ver o status):

```bash
# sintaxe ruim
curl -i -X POST localhost:3000/carrinho -d '{livroId quebrado'
# campo faltando
curl -i -X POST localhost:3000/carrinho -d '{"quantidade": 2}'
# id inexistente
curl -i -X POST localhost:3000/carrinho -d '{"livroId": "fantasma", "quantidade": 1}'
# quantidade negativa
curl -i -X POST localhost:3000/carrinho -d '{"livroId": "sally-adventure-book", "quantidade": -3}'
# quantidade STRING (a ferrada do Tiago - com -H json para chegar como texto no campo)
curl -i -X POST localhost:3000/carrinho -H "content-type: application/json" -d '{"livroId": "sally-adventure-book", "quantidade": "2"}'
# válido (agora sim)
curl -i -X POST localhost:3000/carrinho -d '{"livroId": "sally-adventure-book", "quantidade": 1}'
```

5. **O teste que importa:** depois de qualquer 400, o servidor continua **vivo**? (`GET /carrinho` responde?) Se o processo morreu, algum `JSON.parse` escapou do `try`.

> O `{erro}` bom é o que permite a alguém *sem ver o código* consertar o pedido. "Bad Request" não; "faltam campos: livroId, quantidade" sim. Escreva mensagens como se fosse o aluno mais perdido lendo.

---

### ✅ Critérios de verificação do Step 9

- [ ] JSON malformado devolve `400` e o servidor não morre
- [ ] `livroId` inexistente no corpo devolve `400` (não 404) com mensagem citando o id
- [ ] Sucesso no POST devolve `201`, e o corpo mostra o item + carrinho atualizado
- [ ] Não existe nenhum `writeHead` fora do helper `enviar`
- [ ] `GET /carrinho` continua `200` mesmo no meio dos testes de erro
- [ ] A string `"2"` no lugar do número `2` devolve **400** (a ferrada da tipologia — se passar, sua validação é de existência, não de tipo)

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. Por que "livro não existe no catálogo" é 400, mas "rota /batatinha" é 404? Onde mora a diferença?
2. Por que 201 e não 200 para o POST que funcionou? O que o número a mais comunica ao frontend?
3. Seu `curl '{livroId quebrado'` teria derrubado o servidor **antes** do try/catch? Por quê (o que `JSON.parse` faz com string inválida)?
