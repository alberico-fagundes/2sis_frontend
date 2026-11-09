# Workshop: Estilo da Livraria

## Step 24 — `:hover`: o botão que responde ao dedo

---

### 📖 Teoria

Pseudo-classe descreve **estado**, não conteúdo: ela se cola ao seletor e vale enquanto o estado dura.

```css
.btn:hover { background-color: hsl(120 100% 18%); }
```

| Pseudo-classe | Dispara quando |
|---|---|
| `:hover` | ponteiro sobre o elemento |
| `:active` | pressionado, entre apertar e soltar |
| `:focus` | recebeu foco (teclado **ou** mouse) |

**A regra do estado: mude uma dose, não a cor.** Se você escolheu a cor da marca em `hsl`, escurecer é mexer no **terceiro** número e manter matiz e saturação:

```
hsl(120 100% 23%)   base
hsl(120 100% 18%)   hover  ← mesma cor, mais funda
```

Em hexadecimal isso seria adivinhar três valores aparentados por acaso. Em `hsl` é aritmética.

**Toque não tem hover.** No celular o primeiro toque **ativa** e simula hover junto: informação escondida só no `:hover` é perdida para metade dos usuários.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.interruptor         { background: hsl(210 20% 90%); }
.interruptor:hover   { background: hsl(210 20% 82%); }  /* 8 pontos, não 40 */
.interruptor:active  { background: hsl(210 20% 74%); }
```

---

### ✍️ Mão na massa

1. Na base `.btn`, acrescente `cursor: pointer`. O navegador **não** faz isso por botão — a mãozinha é o padrão do link.
2. Escreva `.btn:hover` escurecendo a **luminosidade** em 5 pontos.
3. Recarregue e passe o ponteiro sobre um botão: a mãozinha aparece e ele afunda sob o dedo. Os **quatro** respondem com uma regra.
4. **Re-meda o contraste** (Step 15) com o ponteiro em cima: o texto ainda passa de 4,5:1 no hover? Se não, escureça menos.
5. Acrescente `:active` mais 3 pontos abaixo do hover. Segure o clique no botão: ele afunda ainda mais.

> Escreva na ordem base → `:hover` → `:active`. Empatadas em especificidade, vence a última escrita — se `:active` vier antes, o hover engole o clique.

---

### ✅ Critérios de verificação do Step 24

- [ ] `.btn` tem `cursor: pointer` declarado na base
- [ ] `.btn:hover` muda só a **luminosidade** da cor da marca
- [ ] Os quatro botões respondem ao ponteiro com uma regra
- [ ] Você re-medeu o contraste **no estado de hover**, não só no base
- [ ] `:active` existe e vem depois do `:hover` no arquivo

### 🧠 Antes de avançar

1. Por que o `hsl` torna este step trivial e o hexadecimal doloroso?
2. Que informação da sua página estaria perdida para quem toca na tela?
