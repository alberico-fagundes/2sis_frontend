# Workshop: Estilo da Livraria

## Step 29 — `viewport`: a dívida que o boilerplate deixou

---

### 📖 Teoria

Olhe o `<head>` do seu `index.html`. Tem `charset`, tem `title`, tem seu `<link>`. **Falta uma linha** que o workshop de HTML nunca ensinou — e sem ela, o layout que você construiu dos Steps 9 a 23 desmorona no celular.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

O navegador do celular, sem essa tag, **finge ter 980px** de largura: renderiza a página inteira nesse palco imaginário e dá zoom para trás para caber no vidro. Seu `<h1>` de `2.5rem` vira fio de letra e o usuário pinça para ler.

| Parte | O que declara |
|---|---|
| `width=device-width` | a largura CSS é a largura **real** do aparelho |
| `initial-scale=1` | zoom inicial de 1× |

**Posição:** depois do `<meta charset>`, antes do `<title>`.

**⛔ Nunca desative o zoom do usuário.** `user-scalable=no` e `maximum-scale` parecem controle de layout e são **barreira**: pinch-to-zoom é requisito do WCAG para quem tem baixa visão.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Um cartaz impresso em três formatos: sem a instrução de escala, a gráfica imprime o A3 e entrega no A5 — o conteúdo é o mesmo, ilegível.

---

### ✍️ Mão na massa

1. **Sinta o estrago antes de curar.** DevTools → **Ctrl+Shift+M** (modo dispositivo) → escolha um iPhone. Recarregue. Que largura aparece na barra? (Perto de 980px, não 375.)
2. Escreva a meta tag no `<head>`, depois do `charset`.
3. Recarregue no mesmo aparelho simulado: a largura virou a real do dispositivo e o texto parou de ser microscópico.
4. **Prove o dano do bloqueio:** adicione `user-scalable=no` temporariamente, tente dar zoom no modo dispositivo e veja o gesto não produzir efeito. **Remova o parâmetro.**

> Se o layout "funciona no desktop e quebra no celular", a causa quase nunca é o CSS — é a meta tag ausente. É o bug mais caro e mais banal do frontend.

---

### ✅ Critérios de verificação do Step 29

- [ ] `<meta name="viewport" content="width=device-width, initial-scale=1">` existe, depois do `charset`
- [ ] Não há `user-scalable=no` nem `maximum-scale` no arquivo
- [ ] Você comprovou no modo dispositivo a mudança de ~980px para a largura real
- [ ] Nenhum texto ficou abaixo de 16px equivalente em 320px de largura

### 🧠 Antes de avançar

1. Por que o navegador móvel finge ter 980px na ausência da meta tag?
2. Que direito do usuário você tira ao escrever `maximum-scale=1`?
