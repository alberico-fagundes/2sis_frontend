# Workshop: Estilo da Livraria

## Step 18 — Especificidade: quem vence quando duas regras brigam

---

### 📖 Teoria

Seu arquivo já tem duas regras incidindo sobre o mesmo botão: `.btn` e `.btn-primary`. As duas declaram fundo. Qual aparece?

O CSS desempata em três etapas, nesta ordem:

| Etapa | Critério |
|---|---|
| 1 | **origem** — navegador < você < você com `!important` |
| 2 | **especificidade** — um número por seletor |
| 3 | **ordem de escrita** — empatados, a **última** vence |

A especificidade tem quatro casas, lidas da esquerda para a direita:

| Seletor | Casas |
|---|---|
| `p` | `0,0,0,1` |
| `.card p` | `0,0,1,1` |
| `.btn` e `.btn-primary` | `0,0,1,0` — **empate** |
| `#checkout-btn` | `0,1,0,0` |

Empate na casa 3 ⇒ decide a etapa 3: **ganha quem está escrito por último no arquivo**. E `0,1,0,0` (um id) vence `0,0,99,0` (noventa e nove classes) — não é soma, é algarismo mais à esquerda.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.placa         { color: navy; }   /* 0,0,1,0 */
#placa-entrada { color: maroon; } /* 0,1,0,0  ← vence */
.placa         { color: teal; }   /* empate com a 1ª, vem depois ← vence a 1ª */
```

---

### ✍️ Mão na massa

1. Abra o DevTools sobre o botão de checkout e olhe o painel Styles: a declaração **perdida** aparece **tachada**. Passe o mouse e leia qual seletor a produziu.
2. Inverta no arquivo a ordem de `.btn` e `.btn-primary`. O checkout mudou de cor? É a etapa 3 agindo.
3. Devolva a ordem. Escreva `#checkout-btn` com uma cor e veja-o **atropelar** a classe — é a casa 2 vencendo a 3. **Apague a regra de id.**
4. Acrescente `!important` à `.btn`. Ela vence o id. **Remova** e note como o arquivo fica previsível sem ele.
5. **Aplique a régua à sua própria obra.** Passe o ponteiro sobre o botão de checkout: ele continua laranja ou **voltou a ser verde** como os demais? `.btn:hover` vale `0,0,2,0` (uma classe + uma pseudo-classe) e atropela `.btn-primary`, que vale `0,0,1,0`. Se ele voltou a verde, escreva `.btn.btn-primary:hover` com a cor do destaque — `0,0,3,0` não tem quem atropele.

> Herança fica **fora** da disputa: qualquer regra local, até `0,0,0,0`, vence o valor herdado do pai.

---

### ✅ Critérios de verificação do Step 18

- [ ] Você identificou no DevTools qual declaração estava tachada e por qual seletor
- [ ] Observou a vencedora inverter ao mudar a ordem de escrita
- [ ] O checkout **conserva** a cor de destaque no hover
- [ ] O arquivo final não tem **nenhum** seletor de id nem `!important`

### 🧠 Antes de avançar

1. Por que `0,1,0,0` vence `0,0,99,0`?
2. Que custo `!important` impõe a um projeto que vai crescer?
