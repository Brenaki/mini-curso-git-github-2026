---
marp: true
theme: default
paginate: true
size: 16:9
header: 'Versionamento de código com GIT e GITHUB'
style: |
  section {
    font-size: 26px;
    padding: 50px 60px;
  }
  section.lead {
    text-align: center;
  }
  h1 { font-size: 46px; }
  h2 { font-size: 36px; }
  pre {
    font-size: 22px;
    line-height: 1.35;
  }
  code { font-size: 0.95em; }
  table { font-size: 22px; }
  header { font-size: 16px; color: #888; }
  footer { font-size: 16px; color: #888; }
  .cols {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 30px;
  }
  .nota {
    font-size: 20px;
    color: #555;
    border-left: 4px solid #999;
    padding-left: 14px;
  }
---

<!-- _class: lead -->
<!-- _header: '' -->

# Versionamento de código com GIT e GITHUB

## Do primeiro commit ao primeiro Pull Request

Mini curso de 1h40 — Análise e Desenvolvimento de Sistemas

---

## Agenda

| Bloco | Tempo | Assunto |
|---|---|---|
| 0 | 5 min | Antes de começar |
| 1 | 10 min | Por que versionar e por que o Git existe |
| 2 | 10 min | Git x GitHub e como o Git pensa |
| 3 | 10 min | Configuração inicial |
| 4 | 15 min | Primeiro repositório e primeiros commits |
| 5 | 15 min | Enviando para o GitHub |
| 6 | 15 min | Branches e conflitos |
| 7 | 10 min | Stash e pull |
| 8 | 8 min | Issues e Pull Requests |
| 9 | 2 min | Recapitulação |

---

## Antes de começar

Abra o terminal (no Windows: **Git Bash**) e confirme que o Git está instalado:

```bash
git --version
```

```
git version 2.x.x
```

Sem Git: https://git-scm.com/downloads

<div class="nota">
Crie sua conta no GitHub <b>agora</b>, em https://github.com/signup.
O código de verificação chega por e-mail e às vezes demora — ele chega
enquanto falamos da história.
</div>

---

## Criando a conta no GitHub

1. Acesse https://github.com/signup
2. Informe **e-mail**, **senha** e **nome de usuário**
3. Resolva a verificação ("não sou robô")
4. Digite o código que chegou no e-mail
5. Pule as perguntas de personalização, se quiser

<div class="nota">
O nome de usuário aparece na URL de todos os seus projetos:
<code>github.com/seu-usuario/projeto</code>. Escolha algo que você
colocaria em um currículo.
</div>

---

<!-- _class: lead -->

# Bloco 1

## Por que versionar e por que o Git existe

---

## O problema que veio antes

Você termina um trabalho da faculdade. A pasta fica assim:

```
trabalho.zip
trabalho_v2.zip
trabalho_v2_corrigido.zip
trabalho_final.zip
trabalho_final_AGORAVAI.zip
trabalho_final_AGORAVAI_professor_pediu_mudar.zip
```

Qual é a versão certa? O que mudou entre elas? Quem mudou?

---

## Piora quando é em grupo

- cada um edita uma cópia e manda pelo WhatsApp
- alguém junta tudo "na mão" e apaga o código do colega sem querer
- funcionava ontem, hoje não funciona — e ninguém sabe o que mudou
- "quem apagou essa função?"

Resultado: **medo de mexer no código**.

---

## A raiz do problema

O código muda o tempo todo. Toda mudança tem:

- **o que** mudou
- **quem** mudou
- **quando** mudou
- **por que** mudou

Copiar pastas guarda, no máximo, o *o que*. O resto se perde.

---

## Tentativa 1: cópias e zip com data

`projeto_2026-10-29.zip`

- ocupa espaço repetindo tudo
- não diz o que mudou de um para o outro
- não diz por quê
- juntar o trabalho de duas pessoas continua manual

---

## Tentativa 2: Google Drive / Dropbox

Sincroniza a pasta entre as pessoas.

Funciona para documentos, mas no código:

- dois editam o mesmo arquivo → um sobrescreve o outro
- o histórico é "versão de 14:32", não "corrigi o login"
- não dá para testar uma ideia sem mexer na versão de todo mundo

Sincronizar não é versionar.

---

## Analogia: o save do videogame

Antes da fase difícil, você **salva o jogo**.

Deu errado? Volta para o save. Nada se perdeu.

Versionar é isso, para código:

- cada **save** tem nome ("antes do chefão")
- você pode voltar para **qualquer** save
- pode abrir um **save paralelo** para testar outro caminho

No Git, cada save se chama **commit**.

---

## Por que o Git foi criado

- **1991–2002** — o kernel do Linux era mantido trocando *patches* e arquivos compactados por e-mail
- **2002** — o projeto passa a usar o **BitKeeper**, ferramenta proprietária, de uso gratuito
- **2005** — a empresa do BitKeeper revoga a gratuidade
- **abril de 2005** — Linus Torvalds (criador do Linux) escreve o **Git** em poucos dias

Em poucas semanas o Git já versionava o próprio Git e o kernel Linux.

---

## Os objetivos do Git

O que Linus queria, depois de anos usando o BitKeeper:

- **velocidade**
- **design simples**
- suporte a **milhares de branches** em paralelo
- **totalmente distribuído** — cada cópia tem o histórico inteiro
- aguentar projetos **enormes**, como o kernel

O Git não inventou versionamento.
Tornou o versionamento distribuído rápido e confiável o bastante para o maior projeto open source do mundo.

---

<!-- _class: lead -->

# Bloco 2

## Git x GitHub e como o Git pensa

---

## Git não é GitHub

**Git** — um **programa** instalado no seu computador.
Funciona sem internet. Guarda o histórico na pasta do projeto.

**GitHub** — um **site** que hospeda repositórios Git na nuvem,
e adiciona colaboração: issues, pull requests, revisão de código.

<div class="nota">
Analogia: Git é a <b>câmera</b> que tira as fotos.
GitHub é o <b>álbum compartilhado na nuvem</b> onde a turma vê e comenta.
Dá para usar a câmera sem o álbum. O álbum não tira foto.
</div>

---

## Outros "álbuns"

O GitHub não é o único serviço que hospeda Git:

| Serviço | Observação |
|---|---|
| **GitHub** | o mais usado; lançado em 2008, da Microsoft desde 2018 |
| **GitLab** | muito usado em empresas; pode ser instalado no próprio servidor |
| **Bitbucket** | da Atlassian, integra com o Jira |
| **Gitea / Forgejo** | leves, para hospedar por conta própria |

Os comandos `git` são **os mesmos** em todos.

---

## Centralizado x distribuído

<div class="cols">
<div>

**Centralizado** (antigo)

```
      +----------+
      | servidor |  <- único histórico
      +----------+
       /   |    \
   [dev] [dev] [dev]
   (só a versão atual)
```

Servidor caiu → ninguém trabalha.

</div>
<div>

**Distribuído** (Git)

```
      +----------+
      |  GitHub  |  <- uma cópia
      +----------+
       /   |    \
   [dev] [dev] [dev]
 (histórico completo
     em cada um)
```

GitHub caiu → todo mundo segue.

</div>
</div>

---

## As três áreas do Git

```
 Diretório de      git add      Área de        git commit    Repositório
  trabalho      ----------->    staging     ------------->     (.git)
(seus arquivos)               (preparação)                   (histórico)
```

- **Diretório de trabalho** — os arquivos como você vê no editor
- **Staging** — o que vai entrar no próximo commit
- **Repositório** — os commits já salvos, dentro da pasta oculta `.git`

---

## Analogia: a foto da turma

1. A turma está espalhada pela sala — **diretório de trabalho**
2. O fotógrafo chama quem vai sair na foto — `git add` (**staging**)
3. *Click* — `git commit` (**repositório**)

Quem não foi chamado não sai na foto, mesmo estando na sala.

Por isso existe o `add`: você escolhe **o que** entra em cada commit.

---

## O que é um commit

Um commit é uma **foto do projeto inteiro** naquele momento, com:

- **autor** — nome e e-mail
- **data**
- **mensagem** — o *por quê* da mudança
- **hash** — identificador único, ex.: `a1be4f5`
- **pai** — o commit anterior

```
a1be4f5 <-- 8625f8a <-- df22bfe      (cada um aponta para o anterior)
```

O histórico é uma corrente de commits.

---

<!-- _class: lead -->

# Bloco 3

## Configuração inicial

---

## Quem é você

Todo commit é assinado. O Git precisa saber seu nome e e-mail:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu-email@exemplo.com"
```

<div class="nota">
Use o <b>mesmo e-mail da conta do GitHub</b>. É assim que o GitHub liga
os commits ao seu perfil (e pinta os quadradinhos verdes).
</div>

---

## Mais três configurações

```bash
git config --global init.defaultBranch main
git config --global pull.rebase false
git config --global core.editor "code --wait"
```

| Configuração | Para quê |
|---|---|
| `init.defaultBranch main` | branch principal se chama `main` (padrão do GitHub) |
| `pull.rebase false` | `git pull` junta com *merge* — evita um erro confuso mais tarde |
| `core.editor` | editor aberto pelo Git; sem VS Code use `nano` |

---

## Conferir

```bash
git config --list
```

```
user.name=Seu Nome
user.email=seu-email@exemplo.com
init.defaultbranch=main
pull.rebase=false
core.editor=code --wait
```

| Opção | Vale para |
|---|---|
| `--global` | todos os repositórios do seu usuário (`~/.gitconfig`) |
| sem `--global` | só o repositório atual (`.git/config`) |

---

<!-- _class: lead -->

# Bloco 4

## Primeiro repositório

---

## Criar o repositório

```bash
mkdir meu-perfil
cd meu-perfil
git init
```

```
Initialized empty Git repository in /home/voce/meu-perfil/.git/
```

```bash
ls -a
```

```
.  ..  .git
```

---

## A pasta `.git`

Todo o histórico mora dentro de `.git`.

- não edite nada lá dentro à mão
- apagar `.git` = apagar **todo o histórico** (os arquivos ficam, os saves somem)
- copiar a pasta do projeto com `.git` = copiar o histórico junto

<div class="nota">
Erro comum: rodar <code>git init</code> na pasta pessoal ou na Área de
Trabalho inteira. Sempre entre na pasta do projeto antes.
</div>

---

## Criar o primeiro arquivo

Crie `perfil.md` no editor, com este conteúdo:

```markdown
# Meu perfil

Nome: ____
Linguagem favorita: ____

## Sobre mim

Estudante de ADS.
```

Preencha o **Nome**. Deixe a **Linguagem favorita** com `____` — vamos brigar por ela no Bloco 6.

---

## `git status`: o comando que você mais vai usar

```bash
git status
```

```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	perfil.md
```

**Untracked** = o Git está vendo o arquivo, mas ainda não cuida dele.

<div class="nota">
Na dúvida, rode <code>git status</code>. Ele quase sempre diz o próximo passo.
Se seu sistema estiver em português, as mensagens aparecem traduzidas.
</div>

---

## `git add`: chamar para a foto

```bash
git add perfil.md
git status
```

```
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   perfil.md
```

O arquivo está no **staging**. Ainda não é um commit.

`git add .` adiciona tudo o que mudou na pasta atual.

---

## `git commit`: tirar a foto

```bash
git commit -m "Adiciona perfil"
```

```
[main (root-commit) a1be4f5] Adiciona perfil
 1 file changed, 8 insertions(+)
 create mode 100644 perfil.md
```

| Parte | Significado |
|---|---|
| `-m "..."` | mensagem do commit |
| `main` | branch onde o commit entrou |
| `root-commit` | primeiro commit do repositório |
| `a1be4f5` | início do hash do commit |

---

## Ver o histórico

```bash
git log
git log --oneline
```

```
a1be4f5 Adiciona perfil
```

<div class="nota">
Esqueceu o <code>-m</code> e caiu numa tela estranha? É o editor <b>Vim</b>.
Digite a mensagem, aperte <code>Esc</code>, digite <code>:wq</code> e Enter.
</div>

---

## Exercício: edite o arquivo

1. Altere o **Nome** em `perfil.md` (coloque o sobrenome) e salve
2. Rode `git status`
3. O arquivo aparece de novo. Por quê, se ele já foi commitado?

```
Changes not staged for commit:
	modified:   perfil.md
```

O commit guardou a foto **daquele momento**.
A mudança nova ainda não foi chamada para foto nenhuma.

---

## `git diff`: o que mudou

```bash
git diff
```

```diff
@@ -1,6 +1,6 @@
 # Meu perfil

-Nome: Ana
+Nome: Ana Souza
 Linguagem favorita: ____
```

`-` vermelho = linha que saiu. `+` verde = linha que entrou.

```bash
git add perfil.md
git commit -m "Completa o nome"
```

---

## Boas mensagens de commit

<div class="cols">
<div>

**Ruim**

```
update
arrumei
asdf
mudanças
final agora vai
```

Daqui a um mês, ninguém sabe o que é.

</div>
<div>

**Melhor**

```
Adiciona página de login
Corrige cálculo da média
Remove senha do código
Atualiza versão do Node
```

Verbo no presente, curto, diz o *quê*.

</div>
</div>

<div class="nota">
Teste: a frase "Este commit ___" precisa fazer sentido com a sua mensagem.
</div>

---

## `.gitignore`: o que não vai para a foto

Arquivo de texto na raiz do projeto, com padrões a ignorar:

```
node_modules/
.env
*.log
.vscode/
```

- dependências baixadas (`node_modules`, `venv`)
- **senhas e chaves** (`.env`)
- arquivos gerados e do editor

<div class="nota">
O <code>.gitignore</code> também é commitado, para valer para todo o grupo.
</div>

---

## Prática — 5 minutos

```bash
git status
echo "SENHA=123" > .env
git status                 # o .env aparece?
```

Crie o `.gitignore` com a linha `.env` e rode de novo:

```bash
git status                 # e agora?
git add .gitignore
git commit -m "Ignora arquivo .env"
git log --oneline
```

Pergunta: por que o `.env` sumiu do `git status` mas continua na pasta?

---

<!-- _class: lead -->

# Bloco 5

## Enviando para o GitHub

---

## Criar o repositório no GitHub

1. No GitHub, botão **+** (canto superior direito) → **New repository**
2. **Repository name**: `meu-perfil`
3. **Public**
4. **Não** marque *Add a README*, *.gitignore* nem *license*
5. **Create repository**

<div class="nota">
O repositório precisa nascer <b>vazio</b>: o histórico vem do seu computador.
Se marcar o README, o GitHub cria um commit que você não tem — e o push é recusado.
</div>

---

## A senha não funciona no terminal

Desde 2021 o GitHub **não aceita a senha da conta** no `git push`.

No lugar da senha, usa-se um **token de acesso pessoal** (PAT).

<div class="nota">
Analogia: o token é a <b>chave reserva</b> que você entrega ao manobrista.
Abre só o que você permitiu, vence numa data, e pode ser cancelado
sem trocar a fechadura (a sua senha).
</div>

---

## Gerar o token (PAT)

1. Foto do perfil → **Settings**
2. Barra lateral, no fim → **Developer settings**
3. **Personal access tokens** → **Tokens (classic)**
4. **Generate new token** → **Generate new token (classic)**
5. **Note**: `minicurso` — **Expiration**: 7 days
6. Marque o escopo **`repo`**
7. **Generate token** e **copie agora**: ele só aparece uma vez

<div class="nota">
Trate o token como senha: não cole no código, não mande no grupo.
</div>

---

## Ligar o repositório local ao GitHub

Copie a URL **HTTPS** que o GitHub mostra depois de criar o repositório:

```bash
git remote add origin https://github.com/seu-usuario/meu-perfil.git
git remote -v
```

```
origin  https://github.com/seu-usuario/meu-perfil.git (fetch)
origin  https://github.com/seu-usuario/meu-perfil.git (push)
```

`origin` é só um **apelido** para a URL. É o nome padrão do remoto principal.

---

## Lembrar o token por um tempo

Para não colar o token a cada `push`:

```bash
git config --global credential.helper "cache --timeout=7200"
```

Guarda na memória por 2 horas. Nada é gravado em disco.

<div class="nota">
No Windows, o Git já vem com o <b>Git Credential Manager</b>: no primeiro
push ele abre uma janela para entrar no GitHub — pode usar o navegador
ou colar o token.
</div>

---

## `git push`: enviar os commits

```bash
git push -u origin main
```

```
Username for 'https://github.com': seu-usuario
Password for 'https://seu-usuario@github.com':   <- cole o TOKEN
```

| Parte | Significado |
|---|---|
| `push` | envia commits locais para o remoto |
| `-u` | lembra a ligação `main` ↔ `origin/main` |
| `origin` | para qual remoto |
| `main` | qual branch |

Depois do primeiro, basta `git push`.

---

## Conferir no GitHub

```
To https://github.com/seu-usuario/meu-perfil.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

Atualize a página do repositório no navegador:

- o `perfil.md` aparece, já renderizado
- clique em **commits**: o histórico é o mesmo do `git log`
- o `.env` **não** está lá

---

<!-- _class: lead -->

# Bloco 6

## Branches e conflitos

---

## O que é uma branch

Uma **linha paralela** de commits.

```
main:       A --- B --- C
                         \
linguagem:                D --- E
```

Você testa uma ideia na branch sem mexer na `main`.
Deu certo → junta (**merge**). Deu errado → apaga a branch.

<div class="nota">
Analogia: o <b>save paralelo</b> do videogame. Você testa o caminho
arriscado sem estragar o save principal.
</div>

---

## Criar e trocar de branch

```bash
git branch                    # lista as branches (* = a atual)
git switch -c linguagem       # cria e já entra na branch
```

```
Switched to a new branch 'linguagem'
```

```bash
git switch main               # volta para a main
git switch linguagem          # vai para a linguagem
```

<div class="nota">
Em tutoriais antigos aparece <code>git checkout</code>. Ele faz isso e muito
mais; o <code>git switch</code> só troca de branch — mais difícil de errar.
</div>

---

## Montando um conflito de propósito

Na branch `linguagem`:

```bash
# em perfil.md:  Linguagem favorita: Python
git commit -am "Define Python como favorita"
```

Volte para a `main` e altere **a mesma linha**:

```bash
git switch main
# em perfil.md:  Linguagem favorita: JavaScript
git commit -am "Define JavaScript como favorita"
```

`-am` = `add` dos arquivos já rastreados + `commit`, num só comando.

---

## Juntar: `git merge`

Estando na `main`, traga a `linguagem`:

```bash
git merge linguagem
```

```
Auto-merging perfil.md
CONFLICT (content): Merge conflict in perfil.md
Automatic merge failed; fix conflicts and then commit the result.
```

As duas branches mudaram **a mesma linha** de jeitos diferentes.
O Git não sabe qual escolher.

---

## Conflito não é erro

```
Nome: Ana Souza
<<<<<<< HEAD
Linguagem favorita: JavaScript
=======
Linguagem favorita: Python
>>>>>>> linguagem
```

| Marcador | Significado |
|---|---|
| `<<<<<<< HEAD` | começo da versão da branch atual (`main`) |
| `=======` | divisória |
| `>>>>>>> linguagem` | fim da versão que está chegando |

O Git está pedindo uma **decisão humana**.

---

## Resolver

1. Abra `perfil.md` e deixe o arquivo **como deve ficar**
   (uma das duas, as duas, ou outra coisa)
2. Apague os três marcadores
3. Salve, marque como resolvido e conclua o merge:

```bash
git add perfil.md
git commit -m "Resolve conflito da linguagem favorita"
```

<div class="nota">
O VS Code mostra botões sobre o conflito: <i>Accept Current</i>,
<i>Accept Incoming</i>, <i>Accept Both</i>. Saída de emergência:
<code>git merge --abort</code> volta para antes do merge.
</div>

---

## Ver o que aconteceu

```bash
git log --oneline --graph
```

```
*   56c6dc7 Resolve conflito da linguagem favorita
|\
| * 0ba4926 Define Python como favorita
* | df22bfe Define JavaScript como favorita
|/
* 8625f8a Completa o nome
* a1be4f5 Adiciona perfil
```

A linha paralela foi e voltou. Envie para o GitHub:

```bash
git push
```

---

## Prática — 5 minutos

```bash
git switch -c teste
# mude a última linha de perfil.md e commite
git switch main
# mude a mesma linha de outro jeito e commite
git merge teste
git status
# resolva, add, commit
git log --oneline --graph
git branch -d teste
```

Pergunta: e se as duas branches tivessem mudado **linhas diferentes**?

---

<!-- _class: lead -->

# Bloco 7

## Stash e pull

---

## Exercício: alguém mudou o remoto

Simule um colega editando direto no GitHub:

1. No GitHub, abra `perfil.md` → ícone de **lápis** (Edit)
2. Mude a linha debaixo de **Sobre mim** (ex.: coloque seu período)
3. **Commit changes...** → **Commit changes**

Agora o GitHub tem um commit que o seu computador **não tem**.

---

## Enquanto isso, no seu computador

Sem commitar, adicione uma linha abaixo do **Nome**:

```
Cidade: ____
```

Tente trazer o commit do "colega":

```bash
git pull
```

```
error: Your local changes to the following files would be overwritten by merge:
	perfil.md
Please commit your changes or stash them before you merge.
Aborting
```

Nada foi perdido. O Git se recusou a sobrescrever o seu trabalho. Por quê?

---

## O dilema

Você tem uma mudança **pela metade** em `perfil.md`.
O `pull` quer atualizar **o mesmo arquivo**.

Opções:

- commitar algo que ainda não terminou — não
- apagar o que fez — não
- **guardar na gaveta**, atualizar, e tirar da gaveta — sim

Essa gaveta é o **stash**.

---

## `git stash`: guardar na gaveta

```bash
git stash
```

```
Saved working directory and index state WIP on main: 56c6dc7 Resolve conflito...
```

```bash
git status
```

```
nothing to commit, working tree clean
```

A mudança não sumiu: está guardada. A mesa está limpa.

---

## `git pull`: receber o que veio do remoto

```bash
git pull
```

```
Updating 56c6dc7..2397254
Fast-forward
 perfil.md | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

`git pull` = `git fetch` (baixa os commits) + `git merge` (junta na sua branch).

Abra o `perfil.md`: a mudança do "colega" está lá.

---

## `git stash pop`: tirar da gaveta

```bash
git stash list
```

```
stash@{0}: WIP on main: 56c6dc7 Resolve conflito...
```

```bash
git stash pop
```

```
Auto-merging perfil.md
	modified:   perfil.md
Dropped refs/stash@{0} (157fe7e0...)
```

Sua `Cidade` voltou, **por cima** da versão atualizada.

---

## Agora sim: commit e push

```bash
git add perfil.md
git commit -m "Adiciona cidade"
git push
```

Ciclo do dia a dia: **pull → trabalha → add → commit → push**.

<div class="nota">
Se o <code>stash pop</code> der conflito (você e o colega mexeram na mesma
linha), resolva igual ao Bloco 6: edite, <code>git add</code>, commit.
</div>

---

## Esqueceu o pull antes do push?

```
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/...'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. ...
```

O remoto tem commits que você não tem. O Git não deixa você apagá-los.

Solução: `git pull`, resolva se houver conflito, depois `git push`.

---

<!-- _class: lead -->

# Bloco 8

## Issues e Pull Requests

---

## Issue: a lista de tarefas do projeto

**Issue** = um registro de *algo a fazer*: bug, melhoria, dúvida.

1. Aba **Issues** → **New issue**
2. Título: `Adicionar seção de hobbies`
3. Descrição: o que você espera que seja feito
4. **Create**

A issue ganha um número: **`#1`**.

<div class="nota">
Para fechar uma issue sem código: botão <b>Close issue</b>, escolhendo
<i>completed</i> (feito) ou <i>not planned</i> (não vamos fazer).
</div>

---

## Pull Request: pedir para juntar

**Pull Request (PR)** = "fiz isto numa branch, revisem e juntem na `main`".

É o `git merge` com **revisão** e **conversa** antes.

```bash
git switch -c hobbies
# adicione a seção "## Hobbies" em perfil.md
git commit -am "Adiciona seção de hobbies"
git push -u origin hobbies
```

A branch agora existe no GitHub também.

---

## Abrir a PR

1. No repositório aparece o aviso **Compare & pull request** — clique
2. Confira: **base: `main`** ← **compare: `hobbies`**
3. Título: `Adiciona seção de hobbies`
4. Na descrição, escreva: `Closes #1`
5. **Create pull request**

Aba **Files changed**: o mesmo `diff` do terminal, agora com espaço
para comentários de revisão linha a linha.

---

## Fechar a PR: com merge

1. **Merge pull request** → **Confirm merge**
2. A PR fica roxa: **Merged**
3. Abra a aba **Issues**: a `#1` foi **fechada sozinha** por causa do `Closes #1`
4. **Delete branch** (opcional): a branch já cumpriu o papel

De volta no terminal:

```bash
git switch main
git pull
```

---

## Fechar a PR: sem merge

Nem toda PR é aceita.

1. Crie outra branch, mude algo, faça push e abra uma nova PR
2. Na PR, no fim da página: **Close pull request**
3. A PR fica vermelha: **Closed** — nada entrou na `main`

<div class="nota">
Fechada não é apagada: a conversa e o código continuam registrados.
Dá para reabrir com <b>Reopen pull request</b>.
</div>

---

<!-- _class: lead -->

# Bloco 9

## Recapitulação

---

## Comandos do mini curso — resumo

```bash
git config --global user.name / user.email   # quem é você
git init                       # cria repositório
git status                     # o que mudou (use sempre)
git add <arquivo> / git add .  # prepara para o commit
git commit -m "mensagem"       # salva a foto
git log --oneline --graph      # histórico
git diff                       # o que mudou, linha a linha
git remote add origin <url>    # liga ao GitHub
git push / git pull            # envia / recebe
git switch -c <branch>         # cria branch e entra
git merge <branch>             # junta branch na atual
git stash / git stash pop      # guarda / devolve mudanças
```

---

## Erros comuns

| Sintoma | Causa provável |
|---|---|
| `Authentication failed` | usou a senha da conta, não o token; ou token sem escopo `repo` |
| `rejected (fetch first)` | o remoto tem commits novos; faça `git pull` antes |
| `not a git repository` | você está fora da pasta do projeto |
| `src refspec main does not match any` | nenhum commit ainda; commite antes do push |
| `local changes would be overwritten` | mudanças sem commit; `git stash` antes do pull |
| `divergent branches` | faltou `git config --global pull.rebase false` |
| Tela estranha no commit | é o Vim: `Esc`, `:wq`, Enter |

---

## Ao sair do laboratório

Em computador compartilhado:

```bash
git credential-cache exit       # esquece o token da memória
```

No GitHub: **Settings → Developer settings → Tokens (classic)** → **Delete** no token do mini curso.

<div class="nota">
No seu computador, prefira um token <b>fine-grained</b> (restrito a
repositórios escolhidos) ou chave <b>SSH</b>.
</div>

---

## O que ficou de fora

- **`git restore` / `git revert` / `git reset`** — desfazer mudanças e commits
- **`git rebase`** — reescrever a linha do histórico
- **Fork** — contribuir com projetos de outras pessoas
- **SSH** — autenticar sem token
- **Tags e releases** — marcar versões (`v1.0`)
- **GitHub Actions** — testes e deploy automáticos a cada push
- **Fluxos de trabalho** — Git Flow, trunk-based

---

## Para praticar depois

1. Coloque um trabalho da faculdade no GitHub, com `.gitignore` e commits pequenos
2. Crie um repositório em grupo: **Settings → Collaborators** e adicione os colegas
3. Faça cada colega trabalhar numa branch e entrar na `main` só por PR
4. Provoque um conflito em dupla, editando a mesma linha
5. Crie um repositório com o seu usuário como nome (`seu-usuario/seu-usuario`): o `README.md` dele vira a capa do seu perfil

---

<!-- _class: lead -->
<!-- _header: '' -->

# Recapitulando

**Git** = histórico do projeto, no seu computador
**GitHub** = o histórico na nuvem, com colaboração
**Commit, branch, PR** = salvar, testar em paralelo, juntar com revisão

O código deixou de ser uma pasta e virou uma história.

Perguntas.
