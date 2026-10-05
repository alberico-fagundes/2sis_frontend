# Aula 2 — Imagens e links (fcc Steps 7–17)

## Passo 7 (fcc Step 7)

**Teoria:** Você pode adicionar imagens ao seu site usando o elemento `img`.
Elementos `img` têm uma tag de abertura sem tag de fechamento. Um elemento
sem tag de fechamento é conhecido como *elemento vazio* (void element).

**Tarefa:** adicione um elemento `img` abaixo do elemento `p`. Neste momento,
nenhuma imagem aparecerá no navegador.

---

## Passo 8 (fcc Step 8)

**Teoria:** Atributos HTML são palavras especiais usadas dentro da tag de
abertura de um elemento para controlar o comportamento do elemento. O
atributo `src` em um elemento `img` especifica a URL da imagem (onde a
imagem está localizada).

**Exemplo:** um elemento `img` com um atributo `src` apontando para o logo
do freeCodeCamp:

```html
<img src="https://cdn.freecodecamp.org/platform/universal/fcc_secondary.svg">
```

**Tarefa:** dentro do elemento `img` existente, adicione um atributo `src`
com esta URL:

`https://cdn.freecodecamp.org/curriculum/cat-photo-app/relaxing-cat.jpg`

---

## Passo 9 (fcc Step 9)

**Teoria:** Todos os elementos `img` devem ter um atributo `alt`. O texto do
atributo `alt` é usado por leitores de tela para melhorar a acessibilidade e
é exibido se a imagem falhar ao carregar.

**Exemplo:**

```html
<img src="cat.jpg" alt="A cat">
```

**Tarefa:** dentro do elemento `img`, adicione um atributo `alt` com este
texto:

`Um gato laranja deitado de barriga para cima`

---

## Passo 10 (fcc Step 10)

**Teoria:** Você pode linkar para outra página com o elemento âncora (`a`).

**Exemplo:** um link para https://www.freecodecamp.org:

```html
<a href="https://www.freecodecamp.org"></a>
```

**Tarefa:** adicione um elemento âncora após o parágrafo que linka para
`https://freecatphotoapp.com`. Neste momento, o link não aparecerá na prévia.

---

## Passo 11 (fcc Step 11)

**Teoria:** O texto de um link deve ser colocado entre as tags de abertura e
fechamento de um elemento âncora (`a`).

**Exemplo:**

```html
<a href="https://www.freecodecamp.org">clique aqui para ir ao freeCodeCamp.org</a>
```

**Tarefa:** adicione o texto-âncora `fotos de gatos` ao elemento âncora.
Isso se tornará o texto do link.

---

## Passo 12 (fcc Step 12)

**Tarefa:** adicione a palavra `Veja` antes do elemento âncora e
`em nossa galeria` depois dele.

---

## Passo 13 (fcc Step 13)

**Tarefa:** adicione tags `p` para transformar a linha
`Veja <a href="https://freecatphotoapp.com">fotos de gatos</a> em nossa galeria.`
em um parágrafo.

---

## Passo 14 (fcc Step 17)

**Teoria:** Em passos anteriores, você usou um elemento âncora para
transformar texto em link. Outros tipos de conteúdo também podem ser
transformados em link envolvido por tags âncora.

**Exemplo:** transformar uma imagem em um link:

```html
<a href="example-link">
  <img src="image-link.jpg" alt="A photo of a cat.">
</a>
```

**Tarefa:** transforme a imagem em um link cercado-a com as tags de elemento
necessárias. Use `https://freecatphotoapp.com` como valor do atributo `href` da
âncora.

---

## Passo 15 (fcc Step 15)

**Teoria:** Para abrir links em uma nova aba, você pode usar o atributo
`target` em um elemento âncora (`a`).

O atributo `target` especifica onde abrir o documento linkado.
`target="_blank"` abre o documento linkado em uma nova aba ou janela.

**Exemplo — sintaxe básica de um elemento `a` com atributo `target`:**

```html
<a href="https://www.freecodecamp.org" target="_blank">freeCodeCamp</a>
```

**Tarefa:** adicione um atributo `target` com o valor `_blank` na tag de
abertura do elemento âncora `fotos de gatos`, para que o link abra em
uma nova aba.

---

✅ **Checkpoint Aula 2** — imagem visível no preview; clicar na imagem tenta
abrir `freecatphotoapp.com`; o link de texto abre em nova aba. Todas as `img`
têm `alt`.
