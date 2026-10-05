# Aula 6 — Documento completo: head, title, lang, meta (fcc Steps 38–42)

## Passo 29 (fcc Step 38)

**Teoria:** Note que tudo que você adicionou à página até agora está dentro
do elemento `body`. Todos os elementos de conteúdo da página que devem ser
renderizados na página ficam dentro do elemento `body`. No entanto, outras
informações importantes ficam dentro do elemento `head`.

O elemento `head` é usado para conter **metadados** sobre o documento, como
seu título, links para folhas de estilo e scripts. Metadados são informações
sobre a página que não são exibidas diretamente na página.

**Tarefa:** adicione um elemento `head` acima do elemento `body`. Envolva
todo o conteúdo visível atual em um elemento `body`.

---

## Passo 30 (fcc Step 39)

**Teoria:** O elemento `title` determina o que os navegadores mostram na
barra de título ou na aba da página.

**Tarefa:** adicione um elemento `title` dentro do elemento `head` com o
texto abaixo:

`CatPhotoApp`

---

## Passo 31 (fcc Steps 40–41)

**Teoria:** Note que todo o conteúdo da página está aninhado dentro de um
elemento `html`. O elemento `html` é o elemento raiz de uma página HTML e
envolve todo o conteúdo da página.

Você também pode especificar o idioma da sua página adicionando o atributo
`lang` ao elemento `html`.

**Tarefa:** adicione o atributo `lang` com o valor `pt-BR` à tag de abertura
do `html` para especificar que o idioma da página é o português.
Garanta que `head` e `body` estejam aninhados dentro do `html`.

---

## Passo 32 (fcc Step 42)

**Teoria:** Você pode definir o comportamento do navegador adicionando
elementos `meta` no `head`. Aqui está um exemplo:

```html
<meta attribute="value">
```

Dentro do elemento `head`, envolva um elemento `meta` com um atributo
`charset` definido com o valor `UTF-8`. Isso diz ao navegador como codificar
os caracteres da página.

**Nota:** o elemento `meta` é um elemento vazio.

**Tarefa:** adicione ao `head`:

```html
<meta charset="UTF-8">
```

---

## Passo 33 — Prova final (sem a folha!)

Crie um novo arquivo `estrutura.md` na pasta da prova e escreva, **de
memória**, apenas a estrutura vazia do documento completo:

```
html (com lang) → head (title + meta) → body → main (com 2 section) → footer
```

Só tags de abertura e fechamento, com indentação de 2 espaços. Sem conteúdo.

---

✅ **Entrega final** — `index.html` completo + `respostas.md` +
`estrutura.md` + checklist de autoavaliação preenchido (ver folha inicial).
