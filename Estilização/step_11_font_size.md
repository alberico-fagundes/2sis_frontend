# Workshop: Estilo da Livraria

## Step 11 — `font-size`: a régua que o usuário controla

---

### 📖 Teoria

`font-size: 20` não existe — número sem unidade é ambíguo. As unidades que importam:

| Unidade | Mede em relação a | Uso |
|---|---|---|
| `px` | nada — é fixo | bordas, sombras, detalhes |
| `rem` | a fonte raiz (`16px` por padrão) | **texto e tudo que escala** |
| `em` | a fonte do pai, em `font-size` | escalar um filho proporcionalmente |

Com raiz de 16px: `1rem` = 16 · `1.5rem` = 24 · `0.875rem` = 14 · `2.5rem` = 40.

**Por que isso é acessibilidade, não gosto.** O usuário pode configurar o tamanho de fonte padrão do navegador. Em `rem`, o navegador respeita. Em `px`, **ignora** — e quem tem baixa visão continua lendo 16px minúsculos.

**Monte uma rampa e use só ela.** Poucos números bem escolhidos, repetidos:

```
2.5rem   letreiro (h1)
1.35rem  título de livro (h2)
1rem     texto corrido (p)
0.95rem  sinopse (.card p)
0.875rem rótulo de botão (.btn)
```

Cinco degraus para cinco papéis. Se aparecer um sexto valor, alguém o inventou por impulso.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

```css
.titulo-cidade { font-size: 2rem; }
.legenda       { font-size: 0.8rem; }
.borda-mapa    { border: 1px solid #999; }
```

Repare na última: **`px` tem lugar certo** — traço fino que viraria borrão se escalasse.

---

### ✍️ Mão na massa

1. Declare `font-size` em `rem` para `h1`, `h2`, `p` e `.btn`, usando a rampa acima.
2. Recarregue: a hierarquia apareceu — o letreiro domina, o título apoia, o corpo corre.
3. **Prove o ponto:** vá às configurações de fonte do navegador, ponha no máximo, recarregue. Tudo cresceu? Se algum texto ficou travado, ele está em `px`. Converta.
4. Na sinopse (`.card p`), aplique o quinto degrau. Só as duas sinopses encolheram — as boas-vindas e o rodapé ficaram.

> Não mude o `font-size` do `<html>` para `Xpx` "para facilitar a conta". Isso quebra a preferência do usuário e anula o benefício do `rem`.

---

### ✅ Critérios de verificação do Step 11

- [ ] Os quatro níveis de texto usam `rem`, e só valores da rampa aparecem no arquivo
- [ ] Ao aumentar a fonte padrão do navegador, **todo** o texto respondeu
- [ ] Nenhuma propriedade de texto está em `px`
- [ ] `.card p` tem tamanho próprio, menor que o do corpo

### 🧠 Antes de avançar

1. Por que `em` em `font-size` compõe (2em dentro de 1.5em = 3×) e `rem` não?
2. Sua rampa tem 5 ou 12 valores? O que isso diz sobre a consistência da página?
