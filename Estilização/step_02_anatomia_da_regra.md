# Workshop: Estilo da Livraria

## Step 2 — Anatomia de uma regra

---

### 📖 Teoria

Toda regra de CSS é a mesma frase:

```
seletor { propriedade: valor; }
```

Você já conhece a sintaxe parecida do HTML. Olhe onde ela **diverge**:

| HTML | CSS |
|---|---|
| `lang="en"` | `color: red;` |
| `=` | `:` |
| valor **entre aspas** | valor **sem aspas** |
| nada | `;` fechando |

O ponto e vírgula não existe em HTML — é a causa nº 1 de regra que "não funciona". Duas declarações no mesmo bloco separam-se por ele: `color: red; text-align: center;`.

E há um detalhe que o Step 1 escondeu: seu `<h1>` já era **grande e em negrito** antes de qualquer CSS seu. Isso é o **UA stylesheet** — a folha de estilo que o navegador embute. Sua regra escreve **por cima** dela, e vence.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
/* o nome do animal na placa */
h2 {
  color: darkred;
  text-align: center;
}
```

Comentário em CSS é `/* assim */` — nunca `<!-- -->`, que o navegador lê como lixo.

---

### ✍️ Mão na massa

1. Na regra de `h1` que você criou, acrescente `text-align: center` como **segunda** declaração.
2. Recarregue: o letreiro foi para o centro?
3. **Force o erro:** apague o `;` que separa as duas declarações, salve e veja o que desaparece. Conserte.
4. Abra o DevTools (F12) no `<h1>` e ache o bloco rotulado `user agent stylesheet` no painel Styles. Ali está quem pintava sua página antes de você.

> Sem o `;` entre declarações, a seguinte é descartada **em silêncio** — sem erro no console. O navegador finge que não leu.

---

### ✅ Critérios de verificação do Step 2

- [ ] A regra de `h1` tem duas declarações separadas por `;`
- [ ] O letreiro está centralizado na tela
- [ ] Você localizou `user agent stylesheet` no painel Styles
- [ ] O arquivo não contém `<!-- -->`

### 🧠 Antes de avançar

1. Por que o valor de `color` não leva aspas, mas um nome de fonte com espaço leva?
2. O que acontece com as regras seguintes se você esquecer um `}`?
