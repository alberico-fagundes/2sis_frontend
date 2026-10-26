# Aula 1 — Texto e estrutura básica (fcc Steps 1–6)

> Nesta prova você construirá o **CatPhotoApp**, um app de fotos de gatos,
> trabalhando com elementos básicos de HTML: títulos, parágrafos, listas,
> imagens, links e a estrutura completa de um documento.

---

## Passo 1 (fcc Step 1)

**Teoria:** Vamos começar a trabalhar com elementos básicos de HTML como
títulos, parágrafos e listas. Comece o workshop adicionando um elemento `h1`
com o texto `CatPhotoApp`.

**Tarefa:** crie o arquivo `index.html` no VS Code e escreva o `h1`.

---

## Passo 2 (fcc Step 2)

**Teoria:** Títulos de níveis diferentes organizam o conteúdo: o `h1` é o
principal e os demais (`h2`, `h3`...) criam subníveis de leitura.

**Tarefa:** abaixo do elemento `h1`, adicione um elemento `h2` com o texto:
`Fotos de Gatos`

---

## Passo 3 (fcc Step 3)

**Teoria:** O elemento `p` representa um parágrafo de texto — a unidade
básica de conteúdo escrito em uma página.

**Tarefa:** crie um elemento `p` abaixo do seu elemento `h2` e dê a ele o
seguinte texto:

`Todo mundo ama gatinhos fofos online!`

---

## Passo 4 (fcc Step 4)

**Teoria:** Comentar permite deixar mensagens sem afetar a exibição do
navegador. Também permite tornar o código inativo. Um comentário em HTML
começa com `<!--`, contém qualquer número de linhas de texto e termina com
`-->`.

**Exemplo:** aqui está um comentário com o texto TODO: Remove h1:

```html
<!-- TODO: Remove h1 -->
```

**Tarefa:** adicione um comentário acima do elemento `p` com o texto:

`TODO: adicionar link das fotos`

---

## Passo 5 (fcc Step 5)

**Teoria:** O HTML5 possui alguns elementos que identificam diferentes áreas
de conteúdo. Esses elementos tornam seu HTML mais fácil de ler e ajudam com
Otimização para Mecanismos de Busca (SEO) e acessibilidade.

O elemento `main` é usado para representar o conteúdo principal do body de um
documento HTML. O conteúdo dentro do elemento `main` deve ser único para o
documento e não deve ser repetido em outras partes do documento.

**Exemplo:**

```html
<main>
  <h1>Conteúdo mais importante do documento</h1>
  <p>Mais conteúdo importante...</p>
</main>
```

**Tarefa:** identifique a seção principal da página adicionando uma tag de
abertura `<main>` antes do elemento `h1` e uma tag de fechamento `</main>`
depois do elemento `p`.

---

## Passo 6 (fcc Step 6)

**Teoria:** No passo anterior, você colocou os elementos `h1`, `h2`, o
comentário e o `p` dentro do elemento `main`. Isso é chamado de *nesting*
(aninhamento). Elementos aninhados devem ser colocados dois espaços mais à
direita do elemento em que estão aninhados. Esse espaçamento é chamado de
*indentação* e é usado para tornar o HTML mais fácil de ler.

**Exemplo:**

```html
<main>
  <h1>Conteúdo mais importante do documento</h1>
  <p>Mais conteúdo importante...</p>
</main>
```

**Tarefa:** o elemento `h1`, o elemento `h2` e o comentário estão indentados
dois espaços a mais que o elemento `main`. Use a tecla Tab (ou Spacebar) para
adicionar dois espaços à frente do elemento `p` para que ele também fique
indentado corretamente.

---


