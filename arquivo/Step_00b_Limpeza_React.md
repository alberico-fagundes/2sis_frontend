# 🧹 Passo 00b: A Limpeza do JSX — Preparando o Canvas em Branco

O Vite é fantástico, mas ele vem de fábrica com um código de demonstração (logos girando, botões contadores e estilos prévios). Para construirmos nossa **PokéAgenda**, precisamos de uma tela 100% limpa — nosso "canvas em branco".

---

### 📌 1. O Conceito
No React, o arquivo `src/App.jsx` é o nosso **Componente Principal**. Tudo o que é colocado dentro do `return (...)` dele é exatamente o que o navegador exibe na tela. Vamos limpar os excessos para começar nossa Pokédex do zero absoluto.

---

### 💻 2. Mão na Massa (Desafio Ativo)

1. **Abra o arquivo `src/App.jsx` no VS Code.**
2. **Apague** as variáveis de estado (`useState`) e as importações de logos do topo (`reactLogo`, `viteLogo`).
3. **Substitua o conteúdo do `return (...)`** para retornar apenas uma estrutura limpa:
   ```jsx
   function App() {
     return (
       <div className="pokedex-app">
         <h1>PokéAgenda</h1>
         <p>Carregando dados dos Pokémon...</p>
       </div>
     );
   }

   export default App;
   ```
4. **Limpeza do CSS:** Abra os arquivos `src/App.css` e `src/index.css`, selecione tudo (`Ctrl + A`) e apague o conteúdo, deixando-os vazios para não haver estilos interferindo.

---

### 🧪 3. Teste de Validação
Execute `npm run dev` no terminal (ou atualize a página no Live Server). Você verá uma página limpa com o título "PokéAgenda" e o parágrafo. Agora estamos prontos para criar nossos primeiros componentes!


