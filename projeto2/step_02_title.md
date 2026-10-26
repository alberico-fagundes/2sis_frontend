# Workshop: Página de Livraria

## Step 2 — O nome da página: `<title>`

---

### 📖 Teoria

O elemento `<title>` define o texto que aparece na **aba do navegador** (e na janela, em celular). É o "cartão de visita" da página — mora no `<head>`, porque é configuração, não conteúdo visível.

- A aba mostra o título **antes** do favicon (ícone pequeno) — em textos longos, o resto é cortado com "…".
- `<title>` tem tag de fechamento `</title>` e fica em uma linha: o texto vai **entre** as tags, não como atributo.
- É obrigatório: um documento HTML sem `<title>` é considerado inválido pelo padrão e pela ferramenta de validação do navegador (DevTools reclama).
- Cuidado com a hierarquia: `<title>` fica **dentro do `<head>`**, que já está dentro do `<html>`. Aninhamento = dois níveis de recuo.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<head>
  <title>Melhores Filmes de 2026</title>
</head>
```

Perguntas para notar: o texto vai dentro ou em atributo? Dentro do `<head>` ou fora dele?

---

### ✍️ Mão na massa

Digite do zero, sem copiar deste arquivo:

1. Abra a tag do elemento de título **dentro** do seu `<head>`.
2. Escreva o texto do título da sua livraria: `XYZ Bookstore Page` (mantenha "XYZ" — é um placeholder proposital; trocaremos mais adiante).
3. Feche a tag e salve. Abra o arquivo no navegador e confira a **aba**: apareceu o nome?

> Se a aba não mudou, 9 em 10 vezes o `<title>` escapou para fora do `<head>` — ou falta a tag de fechamento.

---

### ✅ Critérios de verificação do Step 2

- [ ] Existe um elemento `<title>` com texto `XYZ Bookstore Page`
- [ ] O `<title>` está dentro do `<head>` (não do `<body>`, não fora)
- [ ] A aba do navegador mostra o título

### 🧠 Antes de avançar

1. Por que o `<title>` fica no `<head>` em vez de no `<body>`, se a gente consegue **vê-lo** na aba?
2. O que acontece com o texto entre `<title>` se você colocar `<b>` ali dentro?
