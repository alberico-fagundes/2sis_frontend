# Workshop: Estilo da Livraria

## Step 27 — Variáveis: o caldo, não o tempero em cada panela

---

### 📖 Teoria

Até aqui cada cor foi digitada à mão em cada regra. Se o cliente pedir "muda o verde da marca", você caça número por número.

**Variável** guarda um valor num nome, declarado com **dois traços** e lido com **`var()`**:

```css
:root {
  --color-brand: hsl(120 100% 23%);
}

.btn { background-color: var(--color-brand); }
```

Diferente de `background-color`, que o navegador lê, uma custom property é **só um nome seu**: ninguém a interpreta — você a lê com `var()`. E ela **herda sempre**, o que a faz servir para duas coisas de uma vez: token global no `:root` (que é o `<html>`, e portanto alcança a página inteira) e tema local declarado num componente.

**Nomeie pelo papel, nunca pela aparência:** `--verde` mente quando a marca vira azul; `--color-brand` não. E `--branco` é um nome pior que `--color-on-brand` — como você vê no Step 28, o branco sobre a marca **precisa virar preto** no tema escuro, e só o nome do papel sobrevive à troca.

Sua página tem **dez** papéis de cor. Todos viram token:

```css
:root {
  --color-bg:       hsl(220 20% 96%);   /* fundo da página    */
  --color-surface:  hsl(0 0% 100%);     /* fundo dos cards    */
  --color-ink:      hsl(220 15% 20%);   /* texto corrido      */
  --color-heading:  hsl(220 18% 14%);   /* títulos            */
  --color-muted:    hsl(220 10% 40%);   /* sinopse            */
  --color-line:     hsl(220 15% 60%);   /* borda do card      */
  --color-brand:    hsl(120 100% 23%);  /* ação               */
  --color-on-brand: hsl(0 0% 100%);     /* tinta sobre a ação */
  --color-accent:   hsl(35 90% 32%);    /* o destaque do Step 17 */
  --color-ring:     hsl(210 90% 45%);   /* anel de foco       */
}
```

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Um chef anota o **caldo-base** e não o prato: muda o caldo uma vez, e sopa, guisado e risoto acompanham a proporção juntos.

---

### ✍️ Mão na massa

1. No **topo** do `styles.css`, abaixo do reset, declare `:root` com os dez tokens acima.
2. Substitua por `var()` toda cor de **base** do arquivo — inclusive o branco do texto dos botões e a cor dos títulos. Os estados `:hover` e `:active` do Step 24 **continuam literais de propósito**: são derivações de luminosidade da marca, e o Step 28 os reescreve para o tema escuro.
3. **Prove o valor:** mude `--color-brand` para outra cor. Quantas regras você editou? **Uma.** Recarregue e veja os quatro botões e o hover acompanharem.
4. Confira que não sobrou cor de base escrita à mão. `Ctrl+F` por `hsl(` **não basta**: palavra-chave (`teal`, `crimson`) escapa da busca. Leia cada `color:` e `background` do arquivo.

> Se `var(--cor)` não funcionar: o nome tem **dois** traços? A variável está declarada num **ancestral** do elemento? Faltou `;` antes dela?

---

### ✅ Critérios de verificação do Step 27

- [ ] `:root` declara os dez tokens de cor, no topo do arquivo
- [ ] Nenhuma cor de **base** sobrevive literal fora de `:root` (estados à parte)
- [ ] Todos os nomes descrevem **papel**, nunca aparência
- [ ] Você trocou a marca editando **uma** linha e viu o efeito em cascata

### 🧠 Antes de avançar

1. Por que `--branco` é um nome pior que `--color-on-brand` quando o tema escuro chegar?
2. Que consequência tem declarar uma variável num `.card` em vez de no `:root`?
