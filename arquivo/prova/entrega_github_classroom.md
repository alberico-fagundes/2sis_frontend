# Entrega: GitHub + Classroom (passo a passo)

Siga exatamente. Se travar em algum passo, chame o professor — isso não tira
ponto.

---

## Parte 1 — Criar o repositório no GitHub (só uma vez, Dia 1, Aula 1)

**O que é?** Um repositório é o seu projeto salvo na nuvem do GitHub. Cada
*commit* é uma "cópia do momento" com data e mensagem — é o que permite ao
professor ver que o código foi feito aula a aula, por você.

1. Acesse `github.com` e faça login (crie a conta com seu e-mail institucional,
   se ainda não tiver).
2. Clique em **+** (canto superior direito) → **New repository**.
3. Preencha:
   - Repository name: `cat-photo-app`
   - Visibilidade: **Public**
   - **DESMARQUE** "Add a README file" (importante!)
4. Clique em **Create repository**.
5. Guarde a URL que aparecer, ex.: `https://github.com/maria-silva/cat-photo-app`

---

## Parte 2 — Ligar a pasta do projeto ao GitHub (só uma vez, Dia 1, Aula 1)

Abra a pasta da prova no VS Code e use o **terminal do VS Code**
(menu Terminal → New Terminal). Digite, uma linha por vez:

```bash
git init
git add index.html
git commit -m "Aula 1: estrutura de texto"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/cat-photo-app.git
git push -u origin main
```

- Troque `SEU-USUARIO` pela URL que você guardou no passo 1.5.
- Na primeira vez que der `git push`, o VS Code pedirá para **fazer login no
  GitHub** (abrirá o navegador) — autorize e pronto, não pedirá de novo.
- Confira no site: seu `index.html` deve aparecer no repositório.

> `git add` = selecionar arquivos · `git commit` = salvar um momento com
> mensagem · `git push` = enviar para o GitHub

---

## Parte 3 — Rotina de toda aula (fim de cada checkpoint)

Depois que o professor der o ✓ da aula, no terminal:

```bash
git add .
git commit -m "Aula 2: imagens e links"
git push
```

Use uma mensagem por aula (`Aula 1`, `Aula 2`...). Os 6 commits contam como
evidência de autenticidade da prova.

Na Aula 3, inclua o `respostas.md`; na Aula 6, o `estrutura.md` — o comando
`git add .` já pega tudo.

---

## Parte 4 — Envio no Classroom (fim da Aula 6)

1. Copie o link do repositório: `https://github.com/SEU-USUARIO/cat-photo-app`
2. Abra a tarefa da prova no **Google Classroom**.
3. Em **Seu trabalho → Adicionar → URL**, cole o link e clique em **Entregar**.
4. Entregue também se o prazo ainda estiver aberto — repositório aberto é
   melhor que entrega atrasada.

---

## Bônus (se sobrar tempo): página no ar

1. No repositório, aba **Settings** → menu **Pages** (esquerda).
2. Source: **Deploy from a branch** → branch `main` → pasta `/ (root)` → Save.
3. Em ~1 minuto, seu site abre em:
   `https://SEU-USUARIO.github.io/cat-photo-app/`
4. Poste esse link como **segunda URL** na entrega do Classroom — vale missão
   estrela (+0,5).

---

## Problemas comuns

| Erro | Causa | Solução |
|------|-------|---------|
| `remote origin already exists` | Você rodou `git remote add` 2x | `git remote remove origin` e refaça |
| `rejected ... fetch first` | Alguém (você de outro PC) enviou antes | `git pull --rebase origin main` e depois `git push` |
| VS Code não abre login | Popup bloqueado | Autorize popups ou use a extensão "GitHub Authentication" |
| Esqueci de fazer o commit da aula | — | Faça o commit atrasado no dia 2; o professor registra no checkpoint |
