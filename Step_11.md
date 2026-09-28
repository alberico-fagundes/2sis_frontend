# 🚀 Step 11: PokéAgenda — Publicando a Pokédex no Ar (Deploy no GitHub Pages & Vercel)

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Projeto:** PokéAgenda (Pokédex em React — Projeto Capstone Final)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica ( / Conceitual):** Entenda a diferença entre **ambiente de desenvolvimento e produção**, o que acontece dentro do **`npm run build`** (minificação e a pasta `dist/`), o conceito de **Hospedagem Estática** e como **caminho base** e Git influenciam o deploy no Vite.
> * **🛠️ Trilha Prática (Projeto Integrador):** Publique a PokéAgenda concluída de graça no **GitHub Pages** (ou na **Vercel**, em 3 cliques) e ganhe um link real para colocar no portfólio e abrir no celular do Prof. Carvalho.

---

### 🧩 1. O Problema Prático (Cenário  - Problem Statement)

**O Dilema do Projeto Preso no `localhost` da Escola:**  
Após semanas de dedicação, a **PokéAgenda** está pronta: responsiva, consumindo a PokéAPI, com busca, filtros, modal de abas e favoritos persistentes. O Prof. Carvalho queria testar o aplicativo no celular durante uma expedição na Floresta de Viridian. Porém, ao digitar `http://localhost:5173` no aparelho, a página não abriu. O estagiário descobriu, perplexo, que `localhost` **só existe dentro do computador onde o servidor roda** — para o celular do professor, "localhost" é o próprio celular, onde não há servidor nenhum!

Um aplicativo web só se torna produto real quando está publicado em um servidor acessível ao mundo.

**A Pergunta-Chave :**  
> *Como compilamos nosso projeto React em arquivos estáticos e o publicamos gratuitamente no **GitHub Pages** (ou **Vercel**) para que qualquer pessoa acesse pelo celular?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 Desenvolvimento vs. Produção: o que faz o `npm run build`?
* **`npm run dev` (aula):** o Vite serve seus arquivos `.jsx` "cru", com recarga instantânea e ferramentas de erro. Nada disso deve ir para a internet.
* **`npm run build` (entrega):** compila, minifica e otimiza todo o projeto, gerando a pasta **`dist/`** com HTML, CSS e JavaScript puros — o **único** idioma que um navegador de produção entende.
* É a diferença entre a cozinha testando o prato (dev) e o prato embalado para viagem (produção).

#### 2.2 O que é Hospedagem Estática?
* Serviços que guardam os arquivos da `dist/` e os servem publicamente 24h. Como nossa PokéAgenda não tem backend (a "inteligência" fica no navegador do usuário + na PokéAPI), hospedagem estática basta.
* **Duas opções gratuitas que usaremos:**
  1. **GitHub Pages:** transforma repositórios Git em sites (ex: `https://SEU-USUARIO.github.io/pokedex/`).
  2. **Vercel:** conecta-se ao seu GitHub e publica automaticamente a cada `git push`.

#### 2.3 O Detalhe que Derruba 9 em 10 Alunos: o Caminho Base ⚠️
* Em produção, o site não mora na raiz `https://site.com/`, e sim numa **pasta** do domínio: `https://usuario.github.io/**pokedex**/`. Se os arquivos continuarem pedindo `/assets/index.js` (raiz), o navegador procura no lugar errado ➜ **tela branca**.
* **No Vite, quem conserta isso é a opção `base` no `vite.config.js`:**
  ```js
  export default defineConfig({
    base: '/pokedex/',   // = nome do repositório, entre barras
    plugins: [react()]
  })
  ```

> [!IMPORTANT]
> **"homepage" no package.json é do Create React App, NÃO do Vite!** Você verá tutoriais antigos mandando adicionar `"homepage": "..."` — esse campo é **ignorado** pelo Vite. Aqui o caminho é sempre `base` no `vite.config.js`. Guardar essa pegadinha é aprender de verdade.

---

### 🛠️ 3. Desafio Ativo: Publicando no GitHub Pages (Mão na Massa)

#### Passo A: Higiene antes do commit (git)
1. Abra o terminal na raiz do projeto (`Ctrl + '` no VS Code) e confira se existe `.gitignore` na raiz:
   ```bash
   ls -a
   ```
   * Se **não** existir, crie `SEU-PROJETO/.gitignore` com no mínimo:
     ```gitignore
     node_modules
     dist
     ```
   * Sem esse passo, `git add .` empacota centenas de megabytes do `node_modules` no seu histórico — a "gordura" que ninguém quer ver no GitHub.
2. Crie um repositório **público** chamado `pokedex` no GitHub (botão **New**, sem README/`.gitignore` duplicados) e conecte:
   ```bash
   git init
   git add .
   git commit -m "Entrega Final da PokéAgenda em React"
   git branch -M main
   git remote add origin https://github.com/SEU-USUARIO/pokedex.git
   git push -u origin main
   ```

#### Passo B: Configurar o Vite para a URL pública
1. Abra `vite.config.js` e ajuste o `base` (igual ao nome do repositório):
   ```js
   import { defineConfig } from 'vite'
   import react from '@vitejs/plugin-react'

   export default defineConfig({
     plugins: [react()],
     base: '/pokedex/'
   })
   ```
2. Instale a ferramenta que empurra a `dist/` para o branch de publicação:
   ```bash
   npm install gh-pages --save-dev
   ```
3. Adicione os scripts no `package.json` (dentro de `"scripts"`):
   ```json
   "scripts": {
     "dev": "vite",
     "build": "vite build",
     "predeploy": "npm run build",
     "deploy": "gh-pages -d dist"
   }
   ```
   * `predeploy` roda o build sozinho antes do deploy — dupla segurança.

#### Passo C: O comando mágico
1. No terminal:
   ```bash
   npm run deploy
   ```
2. Aguarde a mensagem **"Published"**. O `gh-pages` criou um branch `gh-pages` com a `dist/`.
3. No GitHub, abra **Settings ➜ Pages** e confirme que a fonte é o branch `gh-pages` (geralmente já fica automático).
4. Acesse (pode levar 1–2 min na primeira vez):
   `https://SEU-USUARIO.github.io/pokedex/` 🎉

#### 🅿️ Plano B (mais fácil ainda): Vercel em 3 telas
1. Acesse `vercel.com` ➜ **Add New… ➜ Project** ➜ importe o repositório `pokedex`.
2. Vercel detecta **Vite** sozinho (Build Command: `npm run build`, Output: `dist`). Clique **Deploy**.
3. Ganhe um `https://pokeagenda.vercel.app`. *Ajuste fino:* com deploy raiz da Vercel, troque o `base` para `'/'` para evitar assets quebrados. Cada novo `git push` publica sozinho.

> [!TIP]
> **Sintoma ➜ Causa ➜ Conserto**
> * **Tela branca no GitHub Pages:** `base` errado/ausente no `vite.config.js` (abra o F12 ➜ Network: erros 404 em `/assets/...`).
> * **Site velhinho mesmo após push:** seu `base`/repo estão certos? Rode `npm run deploy` de novo; no Pages, force Ctrl+F5.
> * **404 puro:** branch errado em Settings ➜ Pages.

---

### 🏆 Checklist de Avaliação do Projeto Capstone Final

- [x] **Estrutura Semântica:** `<header>`, `<main>`, `<article>`, `<figure>` e `<footer>`.
- [x] **Componentização React:** arquivos `.jsx` independentes e reutilizáveis.
- [x] **Integração com PokéAPI:** 151 Pokémons reais via `useEffect` + `fetch` + `Promise.all`.
- [x] **Grid Responsivo:** CSS Grid `repeat(auto-fill, minmax())` sem media queries.
- [x] **Busca e Filtros:** input controlado por nome/ID e botões de tipo combinados com `.filter()`.
- [x] **Interatividade:** `useState` (shiny local, tabs do modal), modal com abertura por clique e bubbling tratado.
- [x] **Persistência:** favoritos elevados ao Grid e salvos no `localStorage` (JSON).
- [x] **Deploy Público:** link real funcionando no celular.

---

### 🧪 4. Teste de Validação Final

1. Pegue seu celular, abra o navegador e digite `https://SEU-USUARIO.github.io/pokedex/`.
2. Aguarde o loading da PokéAPI e confira a grade completa de 151.
3. Busque "char", filtre por "Fogo", abra o Charizard no modal, alterne as abas Sobre/Estatísticas/Golpes.
4. Ative o Shiny, favorite o Pikachu e **feche o navegador do celular inteiro**.
5. Reabra o link: o Pikachu continua ❤️ (favorito persistido) — e o Prof. Carvalho, emocionado na Floresta de Viridian.

---

### ❓ 5. Quiz de Fixação (6 Questões de Múltipla Escolha)

#### Q1. Para que serve o comando `npm run build` em um projeto React/Vite?
- (A) Apagar o código do projeto.
- (B) Compilar, minificar e otimizar o projeto, gerando os arquivos estáticos de produção na pasta `dist/`.
- (C) Reiniciar a internet da escola.
- (D) Enviar e-mail ao professor.

> **Gabarito Comentado:** **(B)** O build gera a versão final enxuta que será servida na hospedagem.

#### Q2. Por que `http://localhost:5173` não abre no celular do Prof. Carvalho?
- (A) Porque a imagem do Pikachu é pesada.
- (B) Porque `localhost` aponta para a própria máquina — o servidor de dev só existe naquele computador.
- (C) Porque falta instalar o React no celular.
- (D) Porque a bateria acabou.

> **Gabarito Comentado:** **(B)** `localhost` é o endereço interno da máquina que roda o `npm run dev`.

#### Q3. O que é o GitHub Pages?
- (A) Rede social de Pokémons.
- (B) Serviço gratuito que hospeda sites estáticos direto de um repositório Git do GitHub.
- (C) Um editor de textos.
- (D) Antivírus online.

> **Gabarito Comentado:** **(B)** Pages serve os arquivos de um branch específico como site público.

#### Q4. No Vite, qual configuração corrige os caminhos dos arquivos quando o site é hospedado dentro de uma subpasta (ex: `usuario.github.io/pokedex/`)?
- (A) `"homepage"` no `package.json`.
- (B) `base: '/pokedex/'` no `vite.config.js`.
- (C) `<base>` no `index.html`.
- (D) `dist: 'pokedex'` no terminal.

> **Gabarito Comentado:** **(B)** No Vite é o campo `base` que informa o caminho público; `homepage` é conceito do antigo CRA e é ignorado aqui.

#### Q5. Por que publicar projetos acadêmicos na web vale tanto a pena?
- (A) Porque paga dinheiro por clique.
- (B) Porque gera link público real, testável em qualquer dispositivo e incluído no portfólio profissional.
- (C) Porque elimina a necessidade de código.
- (D) Porque substitui o VS Code.

> **Gabarito Comentado:** **(B)** Portfólio publicado e acessível comprova habilidade real a recrutadores e colegas.

#### Q6. O que significa um site ser 100% responsivo?
- (A) Que responde mensagens de voz.
- (B) Que seu layout se adapta a diferentes tamanhos de tela (celular, tablet, monitor).
- (C) Que só roda em Linux.
- (D) Que baixa rápido no Drive.

> **Gabarito Comentado:** **(B)** Nossa grade `auto-fill + minmax` (Step 05) garante isso na prática.

---

### 📝 6. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Build e Deploy de Aplicações React com Vite. Diferença dev/produção, minificação e pasta dist, hospedagem estática (GitHub Pages e Vercel), configuração de caminho base no vite.config.js, fluxo Git básico para publicação com gh-pages, uso do .gitignore e diagnóstico de tela branca em deploy. Entrega final do projeto Capstone PokéAgenda."*
