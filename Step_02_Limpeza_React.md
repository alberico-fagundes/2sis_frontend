# 🧹 Passo 02: A Limpeza do JSX

O Vite é ótimo, mas ele vem com um código "sujo" para demonstração (logos girando, botões que contam números). Para os nossos alunos do 3SIS, precisamos de uma tela limpa, um verdadeiro "canvas em branco".

### 📌 O Conceito (Teoria Profunda)
Lembre-se da nossa aula sobre Componentes: O arquivo `App.jsx` é o componente Mestre. Tudo o que é retornado dentro do `return ()` dele é o que o navegador pinta na tela. Para facilitar a vida do aluno, não queremos que ele brigue com CSS complexo logo no Dia 01.

### 💻 Mão na Massa (Desafio Ativo)
Vamos higienizar a nossa interface.

**Sua Tarefa Prática:**
1. Abra o arquivo `src/App.jsx`.
2. Apague TODAS as variáveis de estado (`useState`) e as tags importadas de logos (`reactLogo`, `viteLogo`).
3. Limpe o `return`. Em vez de retornar aquele monte de tags, faça o componente retornar **apenas** uma `<div>` contendo a classe `dashboard-container`.
4. Dentro dessa div, coloque um título `<h1>` escrito: "Painel de Controle 3SIS", e um parágrafo `<p>` escrito: "Aguardando integração com o backend...".
5. *(Opcional)*: Vá nos arquivos `App.css` e `index.css` e apague todo o conteúdo deles para que o site fique 100% cru e sem estilos fantasmas atrapalhando.

**Teste:** Rode `npm run dev` no terminal do frontend e abra o link. Você deve ver apenas o seu título e parágrafo em uma tela limpa!
