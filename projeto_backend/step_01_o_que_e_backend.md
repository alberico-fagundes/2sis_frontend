# Workshop: API da XYZ Bookstore

## Step 1 — O que é um backend (e seu primeiro programa Node)

**Objetivo do workshop:** construir o servidor da livraria que você montou no `projeto2` — um programa que recebe pedidos pela rede e devolve dados dos livros, do carrinho e do checkout. Este primeiro step tira o JavaScript do navegador e coloca ele no terminal.

---

### 📖 Teoria

No frontend, o **navegador** executa seu JavaScript: ele enxerga HTML, CSS e a tela. No backend, quem executa o JavaScript é o **Node.js** — o mesmo motor V8 do Chrome, solto no sistema operacional, sem navegador, sem tela. Ele enxerga arquivos, rede e processos.

Todo sistema web é um papo entre dois lados:

| Lado | Onde roda | O que faz |
|------|-----------|-----------|
| **Cliente** (frontend) | Navegador do aluno | Mostra a página, botões, cards |
| **Servidor** (backend) | Máquina com Node | Guarda os dados, responde pedidos |

Analogia de restaurante: o cliente (navegador) olha o cardápio e faz um pedido; a cozinha (Node) prepara e devolve o prato. O garçom que carrega pedido e prato é o **HTTP** — o protocolo que os dois lados falam. Hoje você vai começar pela cozinha: sem garçom ainda, só os **dados** do cardápio.

Para rodar um arquivo JS no Node, o comando é um só:

```bash
node nome-do-arquivo.js
```

Diferença que importa: `node arquivo.js` **roda e termina** (programo de linha); um servidor **roda e fica** — isso vem no Step 2.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Uma petshop guarda seus produtos assim:

```javascript
const produtos = [
  { nome: "Ração 1kg", preco: 25.9 },
  { nome: "Coleira", preco: 12.0 },
];

console.log(produtos);
console.log("Total de produtos: " + produtos.length);
```

Salvo como `produtos.js`, roda-se com `node produtos.js`. O `console.log` imprime no **terminal** — não existe `alert`, não existe tela.

---

### ✍️ Mão na massa

1. Crie uma pasta chamada `projeto_backend` (se ainda não existir) e entre nela no terminal (`cd`).
2. Dentro dela, crie o arquivo `catalogo.js`.
3. Nesse arquivo, declare `const livros =` seguido de um **array com 2 objetos** — um por livro da sua livraria — cada objeto com três propriedades: `titulo`, `autor` e `preco` (número, sem `$`).
4. Abaixo do array, imprima o array inteiro com `console.log(livros)`.
5. Imprima também uma frase no formato `"Catálogo com X livros"` usando `livros.length` para descobrir o X (concatenação com `+`).
6. Rode: `node catalogo.js`.

> Dica: objeto no JS usa `{ chave: valor }`, separados por vírgula; array usa `[ item, item ]`. Um array de objetos é o cardápio completo: cada linha é um objeto, o cardápio é o array.

---

### ✅ Critérios de verificação do Step 1

- [ ] `catalogo.js` existe dentro de `projeto_backend`
- [ ] `const livros` é um array com exatamente 2 objetos
- [ ] Cada objeto tem `titulo`, `autor` e `preco`
- [ ] `node catalogo.js` imprime o array e a frase com a contagem, sem erros

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. Que ferramenta executava seu JS no frontend, e quem executa agora?
2. Por que o `console.log` não aparece em uma "tela de livraria"?
3. Se a livraria tivesse 300 livros, o que mudaria nesse arquivo? (Nada? Tudo? Por quê?)
