# Workshop: Estilo da Livraria

## Step 12 — `font-family`: a fila de reservas

---

### 📖 Teoria

`font-family` não escolhe **uma** fonte: escolhe uma **fila**. Você lista candidatas e o navegador usa a **primeira que existir na máquina** do usuário.

```css
body { font-family: Georgia, "Times New Roman", serif; }
```

| Regra | Por quê |
|---|---|
| nome com espaço leva **aspas** | `"Times New Roman"` — sem aspas, o navegador lê como três fontes |
| separado por **vírgula** | vírgula é lista; `;` encerraria a declaração |
| a **última** é uma genérica | `serif`, `sans-serif`, `monospace`, `system-ui` — sem ela, se todas falharem, o navegador chuta |

As duas genéricas que resolvem quase tudo: **`serif`** (remates nos traços — impressão, tradição, livraria) e **`sans-serif`** (limpa — interface, tela pequena).

`font-family` **herda** (Step 5): declare uma vez no `body` e a página inteira obedece.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
body { font-family: "Iowan Old Style", Georgia, Cambria, serif; }
```

Um jornal de bairro com quatro candidatas: se a primeira for do macOS e não existir no Windows, a segunda salva o layout.

---

### ✍️ Mão na massa

1. No `body`, escreva `font-family` com **três** fontes nomeadas e uma genérica por último.
2. Recarregue: a página inteira trocou de caráter — é a herança trabalhando.
3. Desvie o `<h1>` para outra família (serif se o corpo é sans, ou o contrário). Só o letreiro mudou.
4. **Prove a fila:** ponha uma fonte inventada na primeira posição. Nada mudou, porque o navegador pulou para a segunda. Remova.

> Se a página inteira **não** mudou, procure aspas faltando num nome com espaço — o navegador descarta a declaração inteira em silêncio.

---

### ✅ Critérios de verificação do Step 12

- [ ] `body` declara `font-family` com ao menos três candidatas, terminando em genérica
- [ ] O `<h1>` desvia da família do corpo
- [ ] Você testou fonte inexistente e confirmou que a fila cai na próxima
- [ ] Nomes com espaço estão entre aspas

### 🧠 Antes de avançar

1. Por que a genérica final não é redundância, mesmo se a primeira fonte existir?
2. Se você aplicar `font-family` só no `<h1>`, os `<h2>` herdam dele ou do `<body>`?
