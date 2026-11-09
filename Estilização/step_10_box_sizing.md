# Workshop: Estilo da Livraria

## Step 10 — `box-sizing`: a conta que fecha

---

### 📖 Teoria

Por padrão, `width` mede **só o conteúdo**. Padding e borda são **somados** em cima:

```
width: 100%  +  padding 2rem  +  border 2px
═══════════════════════════════════════════►
total real = 100% + 4rem + 4px   ← estoura a container
```

`box-sizing: border-box` muda o que a palavra `width` significa: passa a medir a **caixa inteira**, e padding e borda são deduzidos de dentro. O conteúdo encolhe para caber.

| | padrão | `border-box` |
|---|---|---|
| `width` mede | só o conteúdo | caixa inteira |
| padding/borda | somam | comem do conteúdo |

Ninguém usa o padrão em projeto real — por isso o **reset**, três linhas que abrem quase todo CSS profissional:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

É escolher a régua certa **uma vez**, em vez de discutir medidas em cada regra.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Um alfaiate anota a medida do **terno pronto**, não a do tecido: a manga etiquetada "40" tem 40 cm no ombro do cliente, com costura e tudo.

```css
.manga { width: 40px; padding: 4px; border: 1px solid #000; }
```

Com o padrão, a peça ficaria com 50 cm e o cliente não entraria nela.

---

### ✍️ Mão na massa

1. No `.card`, declare `width: 100%`. Reduza a janela: apareceu uma barra de rolagem horizontal que não devia existir.
2. Meça no DevTools (Computed → diagrama de caixa) a largura real do card e compare com a da container. Os números não batem — esse é o bug.
3. Cole o reset de três linhas no **topo** do `styles.css`, antes de todas as regras.
4. Recarregue: a barra sumiu. Remova o `width: 100%` que você acabou de curar — blocos já ocupam o espaço do pai sem você pedir.

> Zerar margem de todo `h1` e `p` no reset é o exagero que evita: você obrigaria a redeclarar espaçamento em cada elemento. O reset aqui troca só a régua.

---

### ✅ Critérios de verificação do Step 10

- [ ] O reset de três linhas está no **topo** do arquivo, antes de qualquer regra
- [ ] Você reproduziu a barra de rolagem horizontal e a eliminou
- [ ] Nenhum `width: 100%` sobrou nos `.card`
- [ ] O arquivo não zera margens de headings e parágrafos

### 🧠 Antes de avançar

1. Com `border-box`, o que acontece com o **conteúdo** quando você aumenta o padding mantendo o `width`?
2. Por que o reset inclui `::before` e `::after` se você ainda não os usa?
