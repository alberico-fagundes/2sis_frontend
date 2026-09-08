# 🚀 Step 03: PokéAgenda — Rodapé Semântico (<Footer />), Acessibilidade W3C e Links Seguros

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Duração:** 50 Minutos  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica (PBL / Conceitual):** Estude HTML5 Semântico (`<footer>`), Acessibilidade W3C/WCAG (`aria-label`, contraste de cor) e segurança em navegação web (`rel="noopener noreferrer"`).
> * **🛠️ Trilha Prática (Projeto Integrador):** Crie o componente reutilizável `<Footer />` em `src/Footer.jsx` e aplique estilos acessíveis e responsivos em `src/Footer.css`.

---

### 🧩 1. O Problema Prático (Cenário PBL - Problem Statement)

**O Dilema do Rodapé Inacessível e Inseguro:**  
Ao lançar a versão de testes da **PokéAgenda**, a equipe recebeu duas reclamações graves. A primeira veio de uma usuária cega que utiliza leitores de tela: o leitor não conseguia identificar as redes sociais e links do rodapé porque eles eram apenas ícones sem texto alternativo ou rótulos acessíveis. A segunda veio da equipe de segurança de TI: um link externo que abria em uma nova aba (`target="_blank"`) permitia que a página de destino maliciosa manipulasse a aba original da PokéAgenda (ataque conhecido como *Tabnabbing*).

Um rodapé feito sem normas de acessibilidade e sem atributos de segurança expõe os usuários a riscos de segurança e exclui pessoas com deficiência.

**A Pergunta-Chave PBL:**  
> *Como podemos utilizar a tag **HTML5 `<footer>`**, atributos de **Acessibilidade W3C (`aria-label`)** e **Links Seguros (`rel="noopener noreferrer"`)** no React para criar um rodapé acessível, seguro e elegante?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 HTML5 Semântico: A Tag `<footer>` e Atributos de Segurança
* **Tag `<footer>`:** Define o rodapé de uma página web ou de uma seção de conteúdo. Geralmente contém avisos de direitos autorais, créditos de dados, links de navegação secundária e termos de uso.
* **Abertura de Links em Nova Aba (`target="_blank"`):** Faz com que o link externo seja aberto em uma nova guia do navegador.
* **Segurança em Links (`rel="noopener noreferrer"`):**
  * `noopener`: Impede que a nova página acesse o objeto `window.opener` da sua página original, prevenindo ataques de redirecionamento malicioso (*Tabnabbing*).
  * `noreferrer`: Impede o envio do cabeçalho `Referer` HTTP para o servidor de destino, protegendo a privacidade do usuário.

#### 2.2 Acessibilidade W3C/WCAG: Atributos ARIA e Contraste Visual
* **Atributo `aria-label`:** Fornece um rótulo em texto legível para leitores de tela quando o elemento visual é composto apenas por um ícone, símbolo ou imagem.
  * Exemplo: `<a href="..." aria-label="Acessar repositório no GitHub">...</a>`.
* **Contraste de Cores (Diretrizes WCAG):** Assegurar que a razão de contraste entre a cor do texto e a cor de fundo seja de no mínimo **4.5:1** para textos normais, garantindo leitura para pessoas com baixa visão ou daltonismo.
* **Indicadores de Foco (`:focus-visible`):** Garantir que elementos interativos (links e botões) exibam um contorno bem visível quando navegados pela tecla `Tab` do teclado.

#### 2.3 JavaScript ES6+: Interpolação Dinâmica de Datas e Template Literals
* **Objeto `Date()` em JS:** Usado para capturar o ano atual automaticamente sem precisar atualizar o texto de copyright manualmente todo ano.
  * `const anoAtual = new Date().getFullYear();`.
* **Template Literals (Interpolação):** Sintaxe de crases (``` `` ```) que permite inserir variáveis dentro de strings com `${}`.
  * Exemplo: `` `© ${new Date().getFullYear()} PokéAgenda - Todos os direitos reservados.` ``.

#### 2.4 React: Injeção de Expressões Dinâmicas no JSX
* **Chaves `{}` no JSX:** Permitem executar e exibir qualquer expressão ou função JavaScript diretamente dentro do código visual.
* **Componentes de Layout:** O `<Footer />` é um componente estático de estrutura que é importado e posicionado na raiz da aplicação (`App.jsx`).

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Veja como construir um rodapé semântico, acessível e seguro em React:

#### Exemplo de Componente React (`src/Rodape.jsx`):
```jsx
import './Rodape.css';

export function Rodape() {
  // Captura automática do ano atual
  const anoAtual = new Date().getFullYear();

  return (
    <footer className="rodape-conteiner">
      <div className="rodape-conteudo">
        <p className="rodape-texto">
          &copy; {anoAtual} Sistema de Ensino. Dados fornecidos por API Pública.
        </p>

        <nav className="rodape-links" aria-label="Navegação secundária do rodapé">
          {/* Link externo com atributos de segurança e acessibilidade */}
          <a 
            href="https://github.com" 
            target="_blank" 
            rel="noopener noreferrer"
            aria-label="Acessar o perfil da instituição no GitHub"
            className="rodape-link"
          >
            GitHub
          </a>
        </nav>
      </div>
    </footer>
  );
}
```

#### Exemplo de CSS Acessível (`src/Rodape.css`):
```css
.rodape-conteiner {
  background-color: #0f172a; /* Fundo escuro */
  color: #f8fafc;            /* Texto claro - Alto contraste (13:1) */
  padding: 2rem 1rem;
  margin-top: auto;
}

.rodape-conteudo {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
}

/* Indicador de foco acessível para navegação por teclado */
.rodape-link:focus-visible {
  outline: 3px solid #38bdf8;
  outline-offset: 4px;
}
```

---

### 🛠️ 4. Desafio Ativo PBL (Mão na Massa - 30 Minutos)

Como desenvolvedor Frontend na PokéAgenda, sua missão é implementar o componente `<Footer />`:

1. **Criar os arquivos:**
   * Na pasta `src/`, crie o arquivo `Footer.jsx` e o arquivo `Footer.css`.
2. **Desenvolver o componente `<Footer />` em `src/Footer.jsx`:**
   * Crie e exporte a função `Footer`.
   * Obtenha o ano atual usando `new Date().getFullYear()`.
   * Retorne a tag HTML5 Semântica `<footer>` com a classe `pokedex-footer`.
   * Dentro do footer, adicione:
     * Um parágrafo `<p>` com a mensagem de copyright usando o ano dinâmico:
       `© {anoAtual} PokéAgenda. Dados consumidos da PokéAPI.`
     * Uma tag `<nav>` com o atributo `aria-label="Links de créditos e redes sociais"`.
     * Dois links externos `<a>` abrindo em nova guia (`target="_blank"`):
       1. Link para a documentação da PokéAPI (`https://pokeapi.co`), com `rel="noopener noreferrer"` e `aria-label="Acessar site oficial da PokéAPI"`.
       2. Link para o GitHub do projeto, com `rel="noopener noreferrer"` e `aria-label="Ver código fonte no GitHub"`.
3. **Estilizar o rodapé com foco em Acessibilidade (`src/Footer.css`):**
   * Importe `Footer.css` em `Footer.jsx`.
   * Defina um fundo escuro (`#1e293b`), texto em tom claro de cinza/branco (`#f1f5f9`) garantindo alto contraste.
   * Use Flexbox para distribuir o texto à esquerda e os links à direita.
   * Adicione o estado `:focus-visible` nos links com uma borda/outline destacada para quem navega via tecla `Tab`.
4. **Renderizar no `App.jsx`:**
   * Importe e adicione a tag `<Footer />` ao final da estrutura do `App.jsx`.

---

### 🧪 5. Teste de Validação (5 Minutos)

1. Abra a aplicação no navegador (`http://localhost:5173`) e role até o final da página.
2. Verifique se o ano de copyright no rodapé exibe o ano atual automaticamente.
3. Clique nos links externos e confirme se ambos abrem em uma nova aba do navegador.
4. Pressione a tecla `Tab` no teclado até selecionar os links do rodapé e confirme se um contorno visível de foco aparece ao redor deles.

---

### ❓ 6. Quiz de Fixação PBL (6 Questões de Múltipla Escolha)

#### Q1. Qual é a tag semântica do HTML5 indicada para representar a seção de rodapé de uma página web?
- (A) `<bottom>`
- (B) `<footer>`
- (C) `<section id="footer">`
- (D) `<end>`

> **Gabarito Comentado:** **(B)** A tag `<footer>` é a especificação oficial do HTML5 para rodapés de páginas e seções.

#### Q2. Ao abrir um link externo em nova aba usando `target="_blank"`, qual combinação de valores do atributo `rel` deve ser utilizada para prevenir vulnerabilidades de segurança como o Tabnabbing?
- (A) `rel="safe"`
- (B) `rel="noopener noreferrer"`
- (C) `rel="external"`
- (D) `rel="blank"`

> **Gabarito Comentado:** **(B)** O valor `noopener noreferrer` impede que a nova página aberta acesse ou redirecione a página de origem através da API `window.opener`.

#### Q3. Qual é a principal função do atributo `aria-label` na acessibilidade de interfaces web?
- (A) Mudar a cor da fonte para leitores noturnos.
- (B) Fornecer uma descrição textual clara de um elemento para leitores de tela usados por pessoas cegas.
- (C) Otimizar o carregamento de imagens no servidor.
- (D) Bloquear a cópia de texto pelo usuário.

> **Gabarito Comentado:** **(B)** O `aria-label` atribui um rótulo em texto para tecnologias assistivas quando o elemento visual não possui texto explícito.

#### Q4. Como capturamos o ano atual de forma dinâmica em JavaScript puro sem precisar atualizar a string manualmente no código?
- (A) `Date.now()`
- (B) `new Date().getFullYear()`
- (C) `Calendar.getYear()`
- (D) `Time.currentYear()`

> **Gabarito Comentado:** **(B)** A classe nativa `new Date()` instancia o objeto de data atual e a função `.getFullYear()` retorna o ano com 4 dígitos.

#### Q5. De acordo com as diretrizes de acessibilidade WCAG, qual é a razão de contraste mínima recomendada entre a cor do texto e a cor do fundo para textos normais?
- (A) 1:1
- (B) 2:1
- (C) 4.5:1
- (D) 100:1

> **Gabarito Comentado:** **(C)** A norma WCAG 2.1 estabelece a razão de contraste mínima de 4.5:1 no nível AA para garantir leitura por pessoas com deficiências visuais moderadas.

#### Q6. No CSS, qual pseudo-classe é recomendada para aplicar estilos de foco apenas quando o usuário navega na interface utilizando o teclado (tecla Tab)?
- (A) `:hover`
- (B) `:active`
- (C) `:focus-visible`
- (D) `:visited`

> **Gabarito Comentado:** **(C)** O seletor `:focus-visible` ativa o indicador de foco apenas quando o navegador identifica que a interação está sendo realizada por teclado.

---

### 📝 7. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Acessibilidade Web (W3C/WCAG) e Estruturação de Rodapés com HTML5. Uso da tag semântica footer, atributos aria-label, links externos seguros com rel noopener noreferrer, contraste de cores e captura de datas dinâmicas em JS/React."*
