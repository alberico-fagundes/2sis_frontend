# Folha do Professor — Prova Prática CatPhotoApp

## Cronograma e checkpoints

| Aula | Passos | Entrega ao fim da aula (checkpoint ✓) |
|------|--------|----------------------------------------|
| 1 | 1–6 | `index.html` com h1→h2→comentário→p dentro de `main` indentado, preview ok |
| 2 | 7–15 | Imagem visível com `alt`, link de texto abre nova aba, comentário removível |
| 3 | 16–18 | Duas `section` + `respostas.md` com 1 frase coerente |
| 4 | 19–23 | `ul` com bolinhas, primeira figura com legenda em itálico |
| 5 | 24–28 | `ol` numerada, negrito na legenda, `footer` com link funcional |
| 6 | 29–33 | Documento validado + `estrutura.md` feito sem a folha |

## Regras de conduta
- Digitação apenas: sem copia-e-cola (Ctrl+C/V é falta de conduta).
- Sem IA e sem internet livre. Consulta permitida: a folha do aluno.
- Erro de digitação não desconta; o que vale é o código funcionar no preview.
- Quem terminar cedo os passos da aula: missão estrela opcional (abaixo).

## Missões estrela (bônus, +0,5 cada, máx. +1,0)
1. `section` extra de invenção própria (ex: "Curiosidades") com `h3` + lista.
2. Terceiro `figure` com imagem e legenda usando `em` **e** `strong`.
3. Link interno (âncora): `a href="#galeria"` apontando para `section id="galeria"`.

## Rubrica — 14 itens (1,0 pt cada = 10,0 com arredondamento 14→10)

| # | Item avaliado | Como conferir no preview/código | Nota parcial |
|---|---------------|--------------------------------|--------------|
| 1 | Documento completo | `html lang="pt-BR"`, `head` com `title`+`meta charset`, `body` | ___ |
| 2 | `main` presente e único | envolve só o conteúdo principal | ___ |
| 3 | Semântica de seções | 2 `section` fechadas corretamente | ___ |
| 4 | `footer` correto | após o `main`, com `p` e link | ___ |
| 5 | Hierarquia de headings | h1 → h2 → h3, nenhum h3 fora de section com h2 | ___ |
| 6 | `ul` válida | 3 `li` aninhados | ___ |
| 7 | `ol` válida | 3 `li`, numerada no navegador | ___ |
| 8 | `figure`/`figcaption` | 2 figuras, legenda dentro do `figure` | ___ |
| 9 | `img` acessível | 3 imagens, todas com `src` e `alt` | ___ |
| 10 | Links | 3 âncoras com `href` válido | ___ |
| 11 | `target="_blank"` | link "fotos de gatos" abre nova aba | ___ |
| 12 | Imagem-link | `img` aninhado dentro de `a` | ___ |
| 13 | Ênfase | `em` em "amam", `strong` em "odeiam", comentário presente | ___ |
| 14 | Indentação | recuo de 2 espaços consistente em todo o arquivo | ___ |

**Nota final = (soma ÷ 14) × 10.** Bônus soma direto na nota final, teto 10.

## Respostas esperadas — questões de justificativa

**Passo 18 (respostas.md):** aceita qualquer resposta que expresse que o `h3`
representa uma subseção do `h2` — sem o `h2` anterior, a hierarquia de
sumário quebra, e leitores de tela/perfis de SEO não conseguem navegar o
documento. Resposta mínima: "porque o h3 depende de um h2 para existir".

**Passo 33 (estrutura.md):** ver `resposta_modelo/estrutura.md`.
Valoriza-se: ordem correta das tags, indentação e fechamentos — não o conteúdo.

## Correção pelo link do GitHub (recebido no Classroom)

Checklist rápido por entrega, antes de aplicar a rubrica:

1. **Abrir o repo** — o link deve ser `https://github.com/usuario/cat-photo-app`.
   Repo com outro nome ou organizado diferente: desconta 0,5 (seguir instruções).
2. **Ver os 3 arquivos:** `index.html`, `respostas.md`, `estrutura.md`.
   `estrutura.md` feito antes da Aula 6 (timestamp do commit) = cola indevida →
   zera o Passo 33.
3. **Histórico de commits** (aba *Commits*): esperar ~6 commits com mensagens
   "Aula 1..6", distribuídos nos 2 dias (olhe data/hora).
   - 1 único commit com tudo → sem evidência de processo: −1,0.
   - Commits nos horários das aulas → ✓ autenticidade.
4. **Ver o site funcionando** — abra o arquivo no repo: o GitHub renderiza
   HTML com aviso de segurança, ou use o link do GitHub Pages (bônus) que
   alguns enviaram como segunda URL.
5. **Plágio:** dois repos com código idêntico (incluindo os mesmos erros de
   digitação) → entreviste os dois em 5 min pedindo que expliquem um item da
   rubrica à sua escolha.

## Tolerâncias (defina antes e anuncie na prova)
- Tags void com ou sem `/` final (`<img ...>` / `<img ... />`): ambas corretas.
- Texto dos parágrafos: acentuação pode variar; conteúdo não.
- URLs erradas que não carregam imagem: desconta item 9, não item 14.
