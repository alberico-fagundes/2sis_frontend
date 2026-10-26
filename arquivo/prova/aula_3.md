# Aula 3 — Seções e hierarquia (fcc Steps 18–21)

## Passo 16 (fcc Step 18)

**Teoria:** Antes de adicionar qualquer novo conteúdo, você deve usar um
elemento `section` para separar o conteúdo das fotos de outros conteúdos
futuros.

O elemento `section` é usado para definir seções em um documento, como
capítulos, cabeçalhos, rodapés ou quaisquer outras seções do documento. É um
elemento semântico que ajuda com SEO e acessibilidade.

**Exemplo:**

```html
<section>
  <h2>Título da Seção</h2>
  <p>Conteúdo da seção...</p>
</section>
```

**Tarefa:** envolva o elemento `h2`, os elementos `p` e o elemento âncora (`a`)
da primeira parte do conteúdo dentro de um elemento `section`.

---

## Passo 17 (fcc Step 19)

**Teoria:** Cada assunto novo do documento merece sua própria seção.

**Tarefa:** adicione um **segundo** elemento `section` abaixo do elemento
`section` existente. Dentro do segundo `section`, adicione um novo elemento
`h2` com o texto `Listas de Gatos`.

---

## Passo 18 (fcc Steps 20–21)

**Teoria:** Quando você adiciona um elemento de título de nível inferior
(`h3`) à página, está implícito que você está iniciando uma nova subseção.
Um `h3` só faz sentido abaixo de um `h2` — ele é o filho daquele título.

**📝 Tarefa de resposta:** crie o arquivo `respostas.md` e escreva, com suas
palavras, 1 frase: *por que um `h3` nunca deve vir antes do `h2` da sua
seção?*

---

✅ **Checkpoint Aula 3** — duas `section` no arquivo, cada uma com seu `h2`,
com conteúdo corretamente aninhado e indentado + `respostas.md` escrito.
