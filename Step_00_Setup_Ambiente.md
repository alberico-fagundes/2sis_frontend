# ⚛️ Passo 00: Preparando o Ambiente no VS Code

Como estamos no laboratório da escola, os computadores podem estar configurados de maneiras diferentes. Para garantir que ninguém fique travado, temos **dois caminhos** para rodar o React hoje.

Antes de começar, abra o Terminal do VS Code (`Ctrl + '`) e digite:
`node -v`

Se aparecer a versão do Node (ex: `v18.x`), siga o **Plano A**.
Se der erro de comando não reconhecido, siga o **Plano B**.

---

## 🟢 Plano A: Padrão de Mercado (Com Node.js)
Este é o formato usado pelas empresas profissionais.
1. No terminal do VS Code, digite: `npm create vite@latest meu-projeto -- --template react`
2. Entre na pasta: `cd meu-projeto`
3. Instale as dependências: `npm install`
4. Inicie o servidor: `npm run dev`
5. *Seu código será feito na pasta `src/`, criando arquivos com final `.jsx`.*

---

## 🟡 Plano B: Formato de Sobrevivência (Sem Node.js)
Se o PC está bloqueado ou sem Node, vamos usar o React direto no navegador usando a extensão **Live Server** do VS Code.
1. Crie uma pasta vazia e abra no VS Code.
2. Crie um arquivo `index.html` e cole o código abaixo (ele baixa o React magicamente pela internet via CDN):
```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>React via CDN</title>
  <!-- Carregando React e Babel -->
  <script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>
  <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
</head>
<body>
  <div id="root"></div>
  <script type="text/babel">
    // Todo o seu código React (Componentes) será escrito aqui dentro!
    function App() {
      return <h1>Nosso App React está rodando!</h1>;
    }
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<App />);
  </script>
</body>
</html>
```
3. Clique com o botão direito no `index.html` e escolha **Open with Live Server**. Pronto!

---
*Dica para o Professor: Entregue aos alunos do Plano B o arquivo CSS de estilos do freeCodeCamp colocando `<style> ... </style>` no cabeçalho do HTML.*
