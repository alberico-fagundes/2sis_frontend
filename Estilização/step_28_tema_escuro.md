# Workshop: Estilo da Livraria

## Step 28 — Tema escuro: colher o que as variáveis plantaram

---

### 📖 Teoria

Como as cores têm **nome**, o tema escuro não duplica regra — só redeclara valores:

```css
@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: hsl(220 15% 10%);
    --color-surface: hsl(220 15% 15%);
    --color-ink: hsl(220 10% 88%);
    --color-brand: hsl(120 70% 42%);
    --color-on-brand: hsl(220 20% 8%);
    --color-accent: hsl(35 85% 58%);
  }
}
```

O `body`, os `.card`, os `.btn` — **nenhum** precisa de uma linha nova. Se você tivesse digitado `hsl(...)` em cada lugar, seriam trinta edições. É esse o retorno do Step 27.

**Repare no último token.** A marca **clareia** no escuro (verde 23% sobre fundo 10% seria invisível) — e quando a marca clareia, a tinta que vai **sobre** ela precisa **escurecer**, senão o texto do botão vira branco-sobre-verde-claro e reprova. É por isso que o Step 27 chamou aquele branco de `--color-on-brand` e não de `--branco`: o nome do **papel** é o que permite inverter os dois em pares.

**Duas inversões que o escuro exige:**

1. o **hover clareia**, em vez de escurecer — escurecer mais sobre fundo escuro some com o feedback;
2. a **sombra fica mais funda**, não mais clara.

**E o escuro não perdoa contraste frouxo.** Tinta clara sobre fundo escuro precisa ser **medida** de novo (Step 15), não presumida.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Um jornal que imprime edição matutina e noturna no mesmo papel: o **layout** é idêntico, só a **tinta** troca. Ninguém redesenha a página às nove da noite.

---

### ✍️ Mão na massa

1. Escreva o bloco `@media (prefers-color-scheme: dark)` no fim do arquivo, redeclarando os tokens de cor.
2. DevTools → aba **Rendering** → emule `prefers-color-scheme: dark`. A página virou sem nenhuma regra de estilo nova.
3. **Re-meda o contraste no escuro:** tinta sobre fundo, e o texto do botão sobre a marca. Ajuste os tokens até passar em 4,5:1.
4. **Corrija o hover do escuro:** dentro do mesmo bloco `@media`, reescreva `.btn:hover` com a marca **clarecida** (ex.: luminosidade acima da base). Fora disso, o hover escurece sobre fundo escuro e o botão não responde ao dedo.

> Token que falta no bloco escuro mantém o valor do claro sobre fundo escuro — e o bug é silencioso, porque o tema claro continua perfeito.

---

### ✅ Critérios de verificação do Step 28

- [ ] O bloco `prefers-color-scheme` redeclara os tokens de cor, sem duplicar regra de estilo
- [ ] Você emulou o escuro no DevTools e confirmou a troca
- [ ] O contraste foi re-medido **no tema escuro**
- [ ] O hover dá feedback nos dois temas

### 🧠 Antes de avançar

1. Quantas regras você editaria para o tema escuro **sem** variáveis?
2. Por que o hover inverte a direção no escuro?
