# Workshop: Página de Livraria

## Step 12 — `<button>`: o primeiro elemento interativo

---

### 📖 Teoria

Até agora sua página é **informativa** — títulos e textos. `<button>` introduz a **interação**: um elemento que o usuário *faz algo com* (clique, toque, Enter com foco).

Por que `<button>` e não uma `<div>` estilizada "de botão"?

- **Acessibilidade de graça**: leitor de tela anuncia "botão", navegação por Tab o alcança, Espaço/Enter ativam — tudo isso precisa ser recriado à mão numa `<div>`.
- **Semântica**: o navegador sabe que é controle clicável; "parecer um botão" não é ser um.
- É elemento **com conteúdo**: o rótulo fica entre `<button>` e `</button>`. O texto do botão deve dizer **o que acontece** ao clicar ("Buy Now", não "Clique aqui").

Este botão carrega também uma class: `btn`. É o mesmo princípio do `card` — uma class **compartilhável**, pensada para quando o CSS chegar e você quiser que *todos* os botões da livraria tenham a mesma cara.

Posição no cartão: último filho, abaixo da sinopse — padrão de card de produto (nome → descrição → ação).

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```html
<div class="prato-card">
  <h2>Pizza Margherita</h2>
  <p>Molho de tomate, mussarela e manjericão.</p>
  <button class="btn">Adicionar ao pedido</button>
</div>
```

Ação por último, sempre com rótulo que descreve o ato.

---

### ✍️ Mão na massa

1. Dentro do `div.card#sally-adventure-book`, **abaixo** do `<p>` da sinopse, crie um `<button>`.
2. Dê a ele a class `btn` (na tag de abertura, entre aspas).
3. Texto exato: `Buy Now`.
4. Salve e clique no botão… nada acontece — e está correto! A *ação* viria com JavaScript (módulo futuro); por enquanto, ele declara a **intenção** de interação. Repare que o cursor já muda para "mãozinha" no hover: o navegador trata como botão mesmo sem estilo.

> Teste de tabulação: com a página focada, aperte Tab até o botão e Enter. Se ele "aceita" o teclado, você acabou de verificar acessibilidade sem escrever uma linha de código de acessibilidade.

---

### ✅ Critérios de verificação do Step 12

- [ ] Existe um `<button class="btn">Buy Now</button>` dentro do primeiro card
- [ ] O botão é o último filho do `div.card#sally-adventure-book`
- [ ] É `<button>`, não `<div>` disfarçada

### 🧠 Antes de avançar

1. Por que o texto do botão não deveria ser só "Clique"?
2. Que vantagens o `<button>` tem sobre uma `<p>` pintada de amarelo?
