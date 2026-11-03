# Workshop: API da XYZ Bookstore

## Step 11 — npm e package.json: a certidão de nascimento do projeto

---

### 📖 Teoria

`npm` é duas coisas que os alunos confundem no primeiro dia:

| Papel | O que é | Exemplo |
|-------|---------|---------|
| **Gerenciador de pacotes** | baixa código dos outros (`express`, `nodemon`) e resolve as dependências deles | `npm install express` |
| **Gerenciador de scripts** | atalhos nomeados que rodam comandos do projeto | `npm start` |

O `package.json` é o documento único que amarra os dois papéis. Criar um sem ele é programar de contrabando. Com ele:

```json
{
  "name": "xyz-bookstore-api",
  "version": "1.0.0",
  "scripts": {
    "start": "node server.js"
  }
}
```

- **`name`** em kebab-case (mesmo hábito do `id` dos livros — o pacote vai para um registro mundial, espaço reservado é por nome).
- **`version`** — `1.0.0` por enquanto; três números com regras próprias (major.minor.patch).
- **`scripts`** — o que importa aqui: `npm start` executa `node server.js`. A partir de hoje ninguém digita `node server.js`; digita-se o **nome** do script. O comando fica registrado no projeto, não na memória do aluno.
- **`dependencies`** aparece sozinho quando rodar `npm install` — o npm cria também o `package-lock.json` (receita exata das versões baixadas) e a pasta `node_modules` (o código instalado em si, gigabytes que **nunca** se versionam nem se copiam).

> **Regra de convivência:** todo comando `npm` do projeto se roda **dentro** da pasta `projeto_backend` (onde está o `package.json`). Rodar `npm` fora cria uma certidão no lugar errado e a confusão está armazém.

O `npm init -y` aceita tudo no default — útil, mas **nesta etapa** você vai editar os campos à mão depois, para conhecer o documento. Uma certidão gerada e nunca lida é a origem do "por que meu npm start roda o server antigo?".

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Criando a base de uma calculadora de churrasco:

```bash
cd churras-api
npm init -y
npm install express
```

`package.json` resultante (o `dependencies` apareceu sozinho):

```json
{
  "name": "churras-api",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": { "test": "echo \"Error: no test specified\" && exit 1" },
  "dependencies": { "express": "^4.19.2" }
}
```

O `^4.19.2` lê-se: "4.x.x a partir de 4.19.2, mas nunca 5" — o `~`/`^` são contratos de confiança em atualização. (Não decorar agora; saber que existe já basta.)

---

### ✍️ Mão na massa

1. Terminal dentro de `projeto_backend`: `npm init -y`.
2. Abra o `package.json` e **edite à mão**: `name` → `xyz-bookstore-api`; `description` → `"API da livraria do projeto2"`; `scripts` → troque o test inútil por `"start": "node server.js"`.
3. Rode `npm start`. Confirme: o servidor da Fase 1 subiu (mesmo comportamento do `node server.js`). `Ctrl + C` derruba.
4. Responda a si mesmo: o que `npm start` sabe que a linha de comando pura não sabe? (O script está **dentro do projeto** — outro aluno que clonar a pasta terá o mesmo atalho.)
5. Olhe a pasta: `node_modules` **não** existe ainda (você não instalou nada — `init` não baixa). Ela aparece no Step 13. Não se assuste com o tamanho dela depois.

> Se `npm init` perguntar algo em vez de usar o `-y` (versões antigas de npm), responda com Enter até o fim — é o mesmo `-y` feito à mão.

---

### ✅ Critérios de verificação do Step 11

- [ ] `package.json` existe com `name: "xyz-bookstore-api"` editado à mão
- [ ] `npm start` sobe o servidor da Fase 1 sem erro
- [ ] `node server.js` e `npm start` rodam **o mesmo** arquivo (compare com `cat package.json`)
- [ ] Você sabe onde moram `name`, `version` e `scripts` no documento

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. Qual a diferença entre `package.json` e `package-lock.json`? (Um é a intenção; o outro é...)
2. Por que `node_modules` não deve ser copiado/versionado se ela é o código que roda?
3. O que acontece com `npm start` se o `scripts.start` apontar para `server.js` mas você renomear o arquivo para `app.js`? (Anota: vem no Step 13.)
