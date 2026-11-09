# Workshop: Estilo da Livraria

## Step 15 — Contraste: a parte que não é decorativa

---

### 📖 Teoria

Texto que não se lê não é feio — é **inacessível**. O WCAG exige razão mínima de contraste entre texto e fundo:

| Tipo de texto | Razão mínima |
|---|---|
| normal | **4,5 : 1** |
| grande (≥ 24px, ou ≥ 18,7px em negrito) | **3 : 1** |

A escala vai de 1:1 (texto invisível) a 21:1 (preto sobre branco). 4,5:1 é o piso, não a meta.

**Não dependa só de cor para transmitir informação.** Um botão "indisponível" que só fica cinza é invisível para parte dos leitores — junte cor **e** texto **e** ícone.

O navegador mede por você: o **seletor de cor** do DevTools (o quadradinho ao lado do valor no painel Styles) mostra a razão contra o fundo real e avisa AA/AAA.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Um cinza-claro sobre branco parece inofensivo e mede **2,5:1** — reprova. O mesmo cinza escurecido dois pontos passa. Ninguém descobre isso olhando: descobre **medindo**.

---

### ✍️ Mão na massa

1. Abra o DevTools no `<p>` das boas-vindas, clique no quadradinho de cor e leia a **razão de contraste** contra o fundo.
2. Anote o número. Passa de 4,5:1?
3. Faça o mesmo nos `.btn`: a razão é entre a **cor do texto** e a **cor de fundo do botão** — não contra a página.
4. Se algum reprovar, escureça a tinta ou clareie o fundo até passar, e **meça de novo**.

> Meça **depois** de mudar, não antes. O número é do par (texto, fundo) naquele instante do arquivo. Se você medir, escurecer o fundo e não conferir, está aprovando algo que não existe mais.

---

### ✅ Critérios de verificação do Step 15

- [ ] Você leu a razão de contraste do texto corrido no DevTools
- [ ] Você leu a razão dos botões (texto sobre a cor de fundo deles)
- [ ] Todo texto da página atende **4,5:1**
- [ ] Alguma cor foi ajustada **com re-medição**, não no chute

### 🧠 Antes de avançar

1. Por que um botão verde-ácido com texto branco pode reprovar e você não saber sem medir?
2. Que informação da sua página depende **só** de cor hoje?
