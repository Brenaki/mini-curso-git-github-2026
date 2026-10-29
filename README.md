# Versionamento de código com GIT e GITHUB

Mini curso introdutório e prático sobre Git e GitHub, com duração de 1h40
(19h00 às 20h40), voltado para acadêmicos de Análise e Desenvolvimento de
Sistemas (1º ao 5º período). Não é necessário conhecimento prévio de Git.

Os participantes aprendem por que o Git foi criado, a diferença entre Git e
GitHub e por que versionar código. Ao longo do mini curso configuram o Git,
criam um repositório, fazem commits, enviam para o GitHub, resolvem um conflito
entre branches, usam `stash` para receber um `pull` sem perder trabalho, e
terminam abrindo e fechando issues e Pull Requests no GitHub.

## Conteúdo do repositório

```
.
├── slides.md          # slides do mini curso (Marp)
├── pratica/
│   ├── perfil.md      # arquivo usado em todo o mini curso
│   └── .gitignore     # exercício: completar os padrões ignorados
└── README.md
```

## Pré-requisitos

- Git instalado (`git --version` deve mostrar a versão)
- No Windows: usar o **Git Bash**, instalado junto com o Git
- Um editor de texto (recomendado: VS Code)
- Conta no GitHub com e-mail verificado (pode ser criada no início do mini curso)

Sem Git instalado: https://git-scm.com/downloads

## Roteiro do mini curso

| Bloco | Tempo | Assunto |
|---|---|---|
| 0 | 5 min | Antes de começar: instalação e conta no GitHub |
| 1 | 10 min | Por que versionar e por que o Git existe |
| 2 | 10 min | Git x GitHub e como o Git pensa (três áreas, commit) |
| 3 | 10 min | Configuração inicial |
| 4 | 15 min | Primeiro repositório: `init`, `status`, `add`, `commit`, `log`, `diff`, `.gitignore` |
| 5 | 15 min | Enviando para o GitHub: repositório, token (PAT), `remote`, `push` |
| 6 | 15 min | Branches, `merge` e resolução de conflito |
| 7 | 10 min | `stash`, `pull` e `stash pop` |
| 8 | 8 min | Issues e Pull Requests: abrir e fechar |
| 9 | 2 min | Recapitulação e perguntas |

## Fio condutor da prática

Todo o mini curso usa um único arquivo, [`pratica/perfil.md`](pratica/perfil.md),
dentro de um repositório `meu-perfil`:

| Bloco | O que acontece com o `perfil.md` |
|---|---|
| 4 | criado, preenchido (Nome) e commitado duas vezes |
| 5 | enviado para o GitHub |
| 6 | a linha `Linguagem favorita` vira `Python` numa branch e `JavaScript` na `main` → conflito |
| 7 | "Sobre mim" é editado pelo GitHub (simula um colega); `Cidade` é adicionada localmente → `stash` |
| 8 | seção `Hobbies` entra por Pull Request, fechando a issue `#1` |

## Configuração usada no mini curso

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu-email@exemplo.com"
git config --global init.defaultBranch main
git config --global pull.rebase false
git config --global core.editor "code --wait"
git config --global credential.helper "cache --timeout=7200"   # Linux/macOS
```

## Gerando o token (PAT)

1. Foto do perfil → **Settings** → **Developer settings**
2. **Personal access tokens** → **Tokens (classic)**
3. **Generate new token** → **Generate new token (classic)**
4. **Note**: `minicurso`, **Expiration**: 7 days, escopo **`repo`**
5. **Generate token** e copiar (só aparece uma vez)

No `git push`, o token vai no lugar da senha. Em sala usamos o token
*classic* por ser mais rápido de configurar; no dia a dia prefira um token
*fine-grained* ou chave SSH.

## Comandos usados no mini curso

```bash
git config --global <chave> <valor>   # configura o Git
git init                              # cria repositório
git status                            # mostra o estado dos arquivos
git add <arquivo> / git add .         # prepara para o commit (staging)
git commit -m "mensagem"              # registra um commit
git commit -am "mensagem"             # add dos rastreados + commit
git log --oneline --graph             # histórico
git diff                              # diferenças ainda não preparadas
git remote add origin <url>           # liga ao repositório remoto
git push -u origin main               # primeiro envio da branch
git push / git pull                   # envia / recebe commits
git branch                            # lista branches
git switch -c <branch> / git switch   # cria e entra / troca de branch
git merge <branch>                    # junta branch na atual
git merge --abort                     # desiste de um merge com conflito
git stash / git stash list / git stash pop   # guarda / lista / devolve mudanças
git branch -d <branch>                # apaga branch já juntada
```

## Gerando os slides

Os slides estão em [`slides.md`](slides.md), no formato
[Marp](https://marp.app/). Podem ser lidos direto no GitHub como Markdown comum.

Apresentar ou exportar com o Marp CLI:

```bash
npx @marp-team/marp-cli slides.md --preview      # modo apresentação
npx @marp-team/marp-cli slides.md -o slides.pdf  # exportar PDF
npx @marp-team/marp-cli slides.md -o slides.html # exportar HTML
```

Alternativa: extensão **Marp for VS Code**, que mostra a pré-visualização e
exporta pelo próprio editor.

## Erros comuns

| Sintoma | Causa provável |
|---|---|
| `Authentication failed` | senha da conta no lugar do token, ou token sem escopo `repo` |
| `rejected (fetch first)` | o remoto tem commits que você não tem; `git pull` antes do push |
| `not a git repository` | comando rodado fora da pasta do projeto |
| `src refspec main does not match any` | push antes do primeiro commit |
| `local changes ... would be overwritten by merge` | mudanças sem commit; `git stash` antes do pull |
| `Need to specify how to reconcile divergent branches` | faltou `pull.rebase false` |
| Push recusado logo no primeiro envio | repositório criado no GitHub com README |
| Tela estranha ao commitar | editor Vim: `Esc`, `:wq`, Enter |

## Ao sair do laboratório

```bash
git credential-cache exit
```

E apagar o token em **Settings → Developer settings → Tokens (classic)**.

## Para praticar depois

1. Colocar um trabalho da faculdade no GitHub, com `.gitignore` e commits pequenos
2. Criar um repositório em grupo e adicionar colegas em **Settings → Collaborators**
3. Trabalhar cada um numa branch e entrar na `main` só por Pull Request
4. Provocar e resolver um conflito em dupla
5. Criar o repositório `seu-usuario/seu-usuario` e usar o `README.md` como capa do perfil

## Assuntos que ficaram de fora

`git restore`, `git revert` e `git reset`, `rebase`, fork, autenticação por
SSH, tags e releases, GitHub Actions e fluxos de trabalho (Git Flow,
trunk-based).

## Licença

Material livre para uso e adaptação em atividades educacionais.
