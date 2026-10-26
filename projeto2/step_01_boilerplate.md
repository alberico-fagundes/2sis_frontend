# Workshop: Página de Livraria

## Step 1 — O esqueleto de toda página HTML

**Objetivo do workshop:** construir uma página de livraria com cartões de livros, praticando organização de conteúdo com `div`, `class` e `id`. Este primeiro step prepara o terreno.

---

### 📖 Teoria

Toda página HTML começa por um **boilerplate** — a estrutura mínima obrigatória. Pense nele como a fundação de uma casa: sem ela, nada acima fica de pé.

| Peça | O que é | Por que existe |
|------|---------|----------------|
| `<!DOCTYPE html>` | Declaração do tipo de documento | Avisa o navegador: "interprete isto como HTML moderno (HTML5)". Sem ela, o navegador entra em "modo de compatibilidade" e pode renderizar tudo diferente. |
| `<html>` | Elemento raiz | É a caixa que envolve **tudo** da página. Todo o resto vive dentro dele. |
| `<head>` | Cabeçalho | Guarda configurações invisíveis ao usuário (título da aba, idioma, codificação). |
| `<body>` | Corpo | Guarda tudo que aparece na tela (virá nos próximos steps). |

**O atributo `lang`:** todo elemento `<html>` deve declarar em que idioma o conteúdo está escrito (ex.: `lang="en"` para inglês, `lang="pt-BR"` para português). Isso importa porque:

1. **Acessibilidade** — leitores de tela usam o idioma para pronunciar o texto corretamente;
2. **Tradução** — o navegador oferece traduzir só quando o idioma declarado difere do do usuário;
3. **Hifenização e busca** — corretor ortográfico e mecanismos de busca respeitam o valor.

Atributo sempre vai no **tag de abertura** e segue o formato `nome="valor"` — repare nas aspas ao redor do valor.

---

### 💡 Exemplo (contexto diferente — não copie, adapte!)

Estrutura mínima de uma página sobre **filmes**, em português:

```html
<!DOCTYPE html>
<html lang="pt-BR">
  <head></head>
</html>
```

Repare em três coisas:
- a declaração vem **antes de tudo**, fora das tags;
- `<head>` está **dentro** de `<html>` (elementos aninhados: o fechado vem primeiro);
- `lang` está na tag de abertura de `<html>`, com valor entre aspas.

---

### ✍️ Mão na massa

Sem colar nada do exemplo acima — escreva você mesmo, do zero, no seu arquivo `index.html`:

1. Declare o tipo de documento HTML5.
2. Abra e feche o elemento raiz da página.
3. Dentro dele, crie o elemento de cabeçalho (ainda vazio).
4. No elemento raiz, adicione o atributo de idioma com o valor `"en"`.

> Dica de digitação: tags de abertura e fechamento precisam **casar** (`<html>` … `</html>`). Se o navegador "engoliu" algo errado, confira o fechamento primeiro.

---

### ✅ Critérios de verificação do Step 1

- [ ] A primeira linha do arquivo é `<!DOCTYPE html>`
- [ ] Existe um elemento `<html>` com tag de fechamento
- [ ] Existe um `<head>` **dentro** do `<html>`
- [ ] O `<html>` tem `lang="en"` na tag de abertura

### 🧠 Antes de avançar, responda (oralmente ou no caderno)

1. O que muda na renderização se você esquecer o `<!DOCTYPE html>`?
2. Por que o `<head>` fica dentro do `<html>` e não antes dele?
3. Se sua livraria fosse em português, qual valor você daria ao `lang`?
