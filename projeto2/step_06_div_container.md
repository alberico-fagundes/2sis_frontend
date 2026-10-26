# Workshop: Página de Livraria

## Step 6 — `<div>`: a caixa organizadora

---

### 📖 Teoria

O `<div>` é o **contentor genérico** do HTML: uma caixa invisível que agrupa outros elementos para que eles possam ser tratados como **uma unidade só**.

Por que agrupar? Pense na sua livraria: ela terá vários cartões de livro. Sem container, cada `<h2>`, `<p>`, `<img>` dos livros fica "solto" no body, misturado com o título e o parágrafo da página. Com containers:

```
body ──┬── h1            (letreiro da livraria)
       ├── p             (frase de boas-vindas)
       └── div           ← "a área dos cartões começa aqui"
```

Pontos-chave:

- `<div>` **não tem aparência nem semântica própria** no padrão do navegador — você só o percebe quando algo vive dentro dele (ou quando CSS chega, depois).
- É elemento **com conteúdo**: precisa de `</div>` e aceita qualquer número de elementos filhos, inclusive outros `<div>` (containers aninhados são o coração de layouts reais).
- Regra de ouro: use `<div>` quando o agrupamento é por **organização/estilo**, e elementos semânticos (`<p>`, `<h1>`, `<article>`…) quando há significado de conteúdo.

> **Nota deste workshop:** ainda não há CSS aqui. O `<div>` já está servindo para **estruturar e agrupar** o conteúdo; a parte de estilo vem no módulo futuro. Ou seja: por enquanto, a mudança dele é toda na *arquitetura* do documento, não no visual.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<body>
  <h1>Cardápio</h1>
  <div>
    <p>Pizza</p>
    <p>Lasanha</p>
  </div>
</body>
```

O `<div>` reúne os dois pratos como "grupo do cardápio" — no navegador, nada muda de aparência.

---

### ✍️ Mão na massa

1. **Abaixo** do seu `<p>` (dentro do `<body>`), crie uma `<div>` com tag de fechamento — ela será a container dos cartões de livro.
2. Por enquanto ela pode ficar vazia (ou com um comentário HTML dizendo o que ela guarda).
3. Recarregue e olhe a tela: **nada mudou**, certo? Isso é esperado. Abra o DevTools (F12 → Inspector) e localize o `<div>` entre o `<p>` e o fim do body — *aí* você o vê.

> Dica de arrumação: conforme os elementos se aninham, indente os filhos 2 espaços a cada nível. Um `<div>` que fecha na coluna errada é o bug estrutural mais comum daqui pra frente.

---

### ✅ Critérios de verificação do Step 6

- [ ] Existe uma `<div>...</div>` vazia (ou com comentário) após o `<p>`
- [ ] Ela está dentro do `<body>`
- [ ] O documento continua válido: todo `</div>` casa com uma abertura

### 🧠 Antes de avançar

1. Se o `<div>` é invisível e não muda nada na tela, o que ele está "fazendo" de útil agora?
2. Qual é a diferença entre agrupar com `<div>` e usar um `<p>` novo para cada livro?
