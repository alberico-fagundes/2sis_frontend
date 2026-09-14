# 🚀 Step 04: PokéAgenda — Rodapé Semântico (<Footer />), Acessibilidade W3C e Links Seguros

**Disciplina:** Programação Front-End (HTML5, CSS3, JavaScript ES6+ e React)  
**Projeto:** PokéAgenda (Pokédex em React)

---

> [!NOTE]
> **📚 ESTRUTURA PEDAGÓGICA (DUAL-TRACK):**
> * **📖 Trilha Teórica (PBL / Conceitual):** Estude HTML5 Semântico (`<footer>`), Acessibilidade W3C/WCAG (`aria-label`, contraste de cores), segurança em navegação web (`rel="noopener noreferrer"`) e datas dinâmicas no JS.
> * **🛠️ Trilha Prática (Projeto Integrador):** Crie o componente reutilizável `<Footer />` em `src/Footer.jsx` e aplique estilos acessíveis e responsivos em `src/Footer.css`.

---

### 🧩 1. O Problema Prático (Cenário PBL - Problem Statement)

**O Dilema do Rodapé Inacessível e Inseguro:**  
Ao lançar a primeira versão da **PokéAgenda**, a equipe recebeu duas notificações sérias. A primeira veio de uma usuária cega que utiliza leitores de tela: o software assistivo não conseguia identificar os links do rodapé porque eles não tinham texto ou rótulos acessíveis. A segunda notificação veio da equipe de segurança: os links externos abrindo em nova aba (`target="_blank"`) permitiam que páginas externas tentassem sequestrar a aba do aplicativo (*Tabnabbing*).

Um rodapé sem padrões de acessibilidade exclui pessoas e, sem atributos de segurança, expõe o usuário a riscos.

**A Pergunta-Chave PBL:**  
> *Como podemos utilizar a tag **HTML5 `<footer>`**, atributos de **Acessibilidade W3C (`aria-label`)** e **Links Seguros (`rel="noopener noreferrer"`)** no React para criar um rodapé acessível, seguro e com ano de copyright automático?*

---

### 📖 2. Teoria Fundamentadora Completa

#### 2.1 HTML5 Semântico: A Tag `<footer>` e Atributos de Segurança
* **Tag `<footer>`:** Define o rodapé de uma página web ou seção de conteúdo. Geralmente contém avisos de direitos autorais, créditos de dados, links de navegação secundária e termos de uso.
* **Abertura de Links em Nova Aba (`target="_blank"`):** Faz com que o link externo seja aberto em uma nova guia do navegador.
* **Segurança em Links (`rel="noopener noreferrer"`):**
  * `noopener`: Impede que a nova página acesse a aba de origem, prevenindo ataques de redirecionamento malicioso (*Tabnabbing*).
  * `noreferrer`: Protege a privacidade do usuário não enviando o endereço de origem no cabeçalho HTTP.

> [!IMPORTANT]
> **Aviso de Segurança (Regra de Ouro):** Sempre que usar `target="_blank"` em qualquer link externo, adicione obrigatoriamente `rel="noopener noreferrer"`. Isso protege sua aplicação contra ataques de sequestro de aba.

#### 2.2 Acessibilidade W3C/WCAG: Atributos ARIA e Contraste Visual
* **Atributo `aria-label`:** Fornece um rótulo textual legível para leitores de tela quando o elemento visual é composto apenas por um ícone ou link simplificado.
  * Exemplo: `<a href="..." aria-label="Acessar documentação oficial da PokéAPI">...</a>`.
* **Contraste de Cores (Diretrizes WCAG):** Garantir que o texto em cima do fundo escuro possua alto contraste, assegurando leitura para pessoas com baixa visão.
* **Indicadores de Foco (`:focus-visible`):** Estilo visual exibido quando o usuário navega pela interface usando a tecla `Tab` do teclado.

#### 2.3 JavaScript ES6+: Interpolação Dinâmica de Datas
* **Objeto `Date()`:** Captura o ano atual automaticamente para que o copyright nunca fique desatualizado:
  ```js
  const anoAtual = new Date().getFullYear();
  ```

---

### 💻 3. Sintaxe Básica & Exemplo Análogo (Consulta Visual)

Veja como construir um rodapé institucional acessível e seguro:

#### Exemplo de Componente React (`src/RodapeInstitucional.jsx`):
```jsx
import './RodapeInstitucional.css';

export function RodapeInstitucional() {
  // Captura dinâmica do ano atual
  const anoAtual = new Date().getFullYear();

  return (
    <footer className="rodape-container">
      <div className="rodape-conteudo">
        <p className="rodape-texto">
          &copy; {anoAtual} Portal Educacional. Todos os direitos reservados.
        </p>

        <nav className="rodape-navegacao" aria-label="Links institucionais">
          <a 
            href="https://github.com" 
            target="_blank" 
            rel="noopener noreferrer"
            aria-label="Acessar página oficial no GitHub"
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

#### Exemplo de CSS Acessível (`src/RodapeInstitucional.css`):
```css
.rodape-container {
  background-color: #0f172a;
  color: #f8fafc;
  padding: 1.5rem 2rem;
  margin-top: 2rem;
}

.rodape-conteudo {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
}

.rodape-link {
  color: #38bdf8;
  text-decoration: none;
  font-weight: 600;
}

.rodape-link:hover {
  text-decoration: underline;
}

/* Foco acessível para navegação via teclado */
.rodape-link:focus-visible {
  outline: 3px solid #38bdf8;
  outline-offset: 4px;
}
```

---

### 🛠️ 4. Desafio Ativo (Mão na Massa)

Como desenvolvedor Frontend na PokéAgenda, sua missão é implementar o componente `<Footer />` oficial:

1. **Criar os arquivos:**
   * Na pasta `src/`, crie o arquivo `Footer.jsx` e o arquivo `Footer.css`.
2. **Desenvolver o componente `<Footer />` em `src/Footer.jsx`:**
   * Crie e exporte a função `Footer`.
   * Obtenha o ano atual dinamicamente com `const anoAtual = new Date().getFullYear();`.
   * Retorne a tag HTML5 Semântica `<footer>` com a classe `pokedex-footer`.
   * Dentro do footer, adicione:
     * Um parágrafo `<p>` com o texto dinâmico:
       `© {anoAtual} PokéAgenda. Dados consumidos da PokéAPI.`
     * Uma tag `<nav>` com o atributo `aria-label="Links de documentação e código fonte"`.
     * Dois links externos `<a>` com `target="_blank"`, `rel="noopener noreferrer"` e `aria-label`:
       1. Link para a PokéAPI: `https://pokeapi.co` (Texto: "PokéAPI", `aria-label="Acessar site oficial da PokéAPI"`).
       2. Link para o GitHub: `https://github.com` (Texto: "GitHub", `aria-label="Ver código fonte no GitHub"`).
3. **Estilizar o rodapé (`src/Footer.css`):**
   * Importe `Footer.css` no topo de `Footer.jsx`.
   * Use fundo escuro (`#1e293b`), texto claro (`#f1f5f9`), Flexbox para alinhar nas extremidades (`justify-content: space-between`) e espaçamento interno.
   * Adicione o estilo `:focus-visible` nos links com contorno destacado.
4. **Renderizar no `App.jsx`:**
   * Importe e adicione o `<Footer />` na base do seu `src/App.jsx`.

---

### 🧪 5. Teste de Validação

1. Abra a aplicação no navegador (`http://localhost:5173`) e observe o final da página.
2. Verifique se o ano do copyright exibe o ano atual automaticamente.
3. Clique nos links e confirme que ambos abrem em novas guias do navegador de forma segura.
4. Pressione a tecla `Tab` no teclado até chegar nos links e verifique o indicador visual de foco acessível.

---

### ❓ 6. Quiz de Fixação (6 Questões de Múltipla Escolha)

#### Q1. Qual tag semântica do HTML5 é a indicada para o encerramento e rodapé de uma página web?
- (A) `<bottom>`
- (B) `<footer>`
- (C) `<section-end>`
- (D) `<base>`

> **Gabarito Comentado:** **(B)** A tag `<footer>` é o padrão semântico do HTML5 para rodapés.

#### Q2. Por que devemos usar `rel="noopener noreferrer"` ao abrir links externos com `target="_blank"`?
- (A) Para acelerar o download de imagens.
- (B) Para proteger a aplicação contra ataques de segurança como o Tabnabbing e preservar a privacidade do usuário.
- (C) Para forçar o navegador a abrir em tela cheia.
- (D) Para traduzir o site automaticamente.

> **Gabarito Comentado:** **(B)** O atributo `noopener noreferrer` impede que a página de destino acesse o objeto `window.opener` da página original.

#### Q3. Qual é o papel do atributo `aria-label` na acessibilidade web?
- (A) Modificar a cor do texto para o modo noturno.
- (B) Fornecer uma descrição clara para leitores de tela em elementos visuais interativos.
- (C) Reduzir o consumo de memória do computador.
- (D) Impedir que o usuário clique no link.

> **Gabarito Comentado:** **(B)** O `aria-label` melhora a experiência de navegação de pessoas com deficiência visual que usam tecnologias assistivas.

#### Q4. Qual instrução em JavaScript captura o ano corrente com quatro dígitos?
- (A) `Date.now()`
- (B) `new Date().getFullYear()`
- (C) `Time.getYear()`
- (D) `Calendar.currentYear()`

> **Gabarito Comentado:** **(B)** `new Date().getFullYear()` retorna o ano atual em formato numérico (ex: `2026`).

#### Q5. De acordo com as diretrizes de acessibilidade WCAG (Nível AA), qual é o contraste mínimo de cor recomendado para textos normais?
- (A) 1.5:1
- (B) 4.5:1
- (C) 10:1
- (D) 50:1

> **Gabarito Comentado:** **(B)** A relação de contraste de 4.5:1 assegura legibilidade para pessoas com baixa visão ou daltonismo.

#### Q6. Qual seletor CSS garante um indicador de foco visível apenas durante a navegação por teclado?
- (A) `:hover`
- (B) `:focus-visible`
- (C) `:active`
- (D) `:visited`

> **Gabarito Comentado:** **(B)** O pseudo-seletor `:focus-visible` estiliza o contorno de foco para usuários navegando via tecla `Tab`.

---

### 📝 7. Resumo RCO (Cópia para o Diário do Professor)

> **Resumo RCO (Diário de Classe):**  
> *"Conteúdo Ministrado: Acessibilidade Web (W3C/WCAG) e Estruturação de Rodapés com HTML5. Uso da tag semântica footer, atributos aria-label, links externos seguros com rel noopener noreferrer, contraste de cores e captura de datas dinâmicas em JS/React."*
