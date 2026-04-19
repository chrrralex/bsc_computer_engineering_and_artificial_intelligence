# 0B. Fondamenti di Git

## 0B.01. Che cos'e' un sistema di controllo di versione?

Un VCS (Version Control System) tiene traccia delle modifiche ai file nel tempo.

Perche' e' utile?
- Keep history of changes.
- Restore old versions.
- Collaborate with others.
- Avoid overwriting work.

Esempi comuni di strumenti VCS sono Git, Subversion e Mercurial. In questo capitolo analizzeremo Git, tipicamente usato da riga di comando in ambienti Unix-like. Git e' il VCS piu' diffuso, anche perche' e' un progetto libero e open source.

## 0B.02. Cosa sono Git e GitHub?

Git e' un sistema di controllo di versione distribuito che puoi eseguire localmente sul tuo computer, in uno o piu' repository. Una volta installato, lo puoi usare direttamente da CLI, tipicamente tramite una shell come zsh, csh, bash o fish.

GitHub e' una piattaforma cloud che ospita repository Git e strumenti di collaborazione come issue, pull request, board e altro. Altri esempi di piattaforme simili sono GitLab e Bitbucket.

## 0B.03. Che cos'e' un repository?

Un repository, o repo, e' una cartella di progetto tracciata da Git.

A repository contains:

- The project files.
- The change history.
- The branches.

Puoi creare un repository Git con il seguente comando, che crea una cartella nascosta chiamata `.git` dove Git salva configurazione e metadati:

```bash
git init
```

Se hai un repository su una piattaforma cloud come GitHub, puoi clonarlo con `git clone`:

```bash
git clone <repositoryUrl>
```

dove tipicamente `<repositoryUrl>` e' un URL SSH o HTTP copiato dalla piattaforma.

Puoi clonare un repository in una cartella personalizzata specificando un percorso relativo o assoluto dopo `<repositoryUrl>`:

```bash
git clone <repositoryUrl> <path>
```

Se vuoi vedere alcune informazioni sul repository inizializzato, puoi usare `cat`:

```bash
cat .git/config
```

An example of its output is:

```txt
[core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        symlinks = false
        ignorecase = true
[remote "origin"]
        url = <repositoryUrl>
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "main"]
        remote = origin
        merge = refs/heads/main
        vscode-merge-base = origin/main
```

## 0B.04. Versione di Git

Per verificare se Git e' installato e quale versione e' presente sulla macchina locale, puoi usare `--version`, spesso abbreviato in `-v`:

```bash
git --version
# or
git -v
```

An example of output is:

```bash
git version 2.43.0
```

Questo e' utile sia per verificare l'installazione, sia per controllarne la compatibilita' con il sistema.

## 0B.05. Configurazione di Git

Se hai un account GitHub, o su un'altra piattaforma compatibile con Git, puoi configurare nome utente ed email con `git config`:

```bash
git config --global user.name "Mario Rossi"
git config --global user.email "mario@email.com"
```

Puoi vedere la configurazione corrente con `--list`:

```bash
git config --list
```

## 0B.06. Branch Git

Un branch e' una linea di sviluppo indipendente. In un repository con uno o piu' collaboratori, ogni membro del progetto puo' lavorare in un branch separato.

Puoi elencare i branch del repository corrente con `git branch`:

```bash
git branch
```

Oppure puoi creare un branch specificandone il nome:

```bash
git branch <branchName>
```

Per cambiare il branch su cui stai lavorando, puoi usare `git checkout`:

```bash
git checkout <branchName>
```

Per creare un branch e spostarti su di esso in un solo comando, usa l'opzione `-b`:

```bash
git checkout -b <branchName>
```

Per eliminare un branch, puoi usare:

```bash
git branch -d <branchName>
```

Fai attenzione ai comandi di eliminazione: una volta eseguiti, il branch viene rimosso.

Puoi forzare l'eliminazione con l'opzione maiuscola `-D`:

```bash
git branch -D <branchName>
```

## 0B.07. Commit Git

Un commit salva un'istantanea delle modifiche. E' l'unita' fondamentale della storia Git e una delle sue proprieta' piu' importanti e' il messaggio, cioe' una breve descrizione delle modifiche fatte.

Per prima cosa puoi aggiungere un file specifico al prossimo commit con `git add`:

```bash
git add <fileName>
```

Per aggiungere tutti i file, puoi usare il punto `.` al posto di `<fileName>`:

```bash
git add .
```

Puoi creare un commit con messaggio usando `git commit` e l'opzione `-m`:

```bash
git commit -m "<messageHere>"
```

Per creare rapidamente un commit su file gia' tracciati con messaggio inline, puoi usare `-am`:

```bash
git commit -am "<inlineMessageHere>"
```

Puoi aggiornare il messaggio dell'ultimo commit con `--amend`:

```bash
git commit --amend
```

Puoi vedere la storia dei commit con `git log`:

```bash
git log
```

Una versione compatta dell'output si ottiene con `--oneline`:

```bash
git log --oneline
```

Per vedere una vista a grafo piu' dettagliata puoi usare `--all`, `--graph` e `--oneline`:

```bash
git log --graph --oneline --all
```

## 0B.08. Git pull

Il comando `git pull` permette di scaricare e integrare modifiche da un repository remoto.

La sintassi piu' semplice e':

```bash
git pull
```

Puoi specificare anche il repository remoto e il branch:

```bash
git pull <repository> <branchName>
```

Spesso `<repository>` vale `origin`, cioe' il repository remoto principale.

Il seguente comando, con opzione `--rebase`:

```bash
git pull --rebase origin main
```

e' equivalente a questa sequenza di operazioni:

```bash
git fetch
git merge origin/main
```

## 0B.09. Git push

Il comando `git push` permette di inviare i commit locali a un repository remoto.

La sintassi di base e':

```bash
git push
```

Se vuoi inviare le modifiche su un branch specifico, puoi indicarlo cosi':

```bash
git push <repository> <branchName>
```

Se hai creato un nuovo branch in locale e vuoi pubblicare sia il branch sia le modifiche, puoi usare `-u`:

```bash
git push -u <repository> <branchName>
```

Puoi forzare un push con `--force`:

```bash
git push --force
```

Una variante piu' sicura del force push e' `--force-with-lease`:

```bash
git push --force-with-lease
```

## 0B.10. Git reset

`git reset` sposta il branch corrente a un altro commit.

Un reset soft mantiene le modifiche locali gia' preparate. Puoi eseguirlo con `--soft`:

```bash
git reset --soft HEAD~1
```

Un reset hard elimina tutte le modifiche locali e si ottiene con `--hard`:

```bash
git reset --hard HEAD~1
```

Puoi resettare anche un file specifico:

```bash
git reset <fileName>
```

In Git, ogni commit ha il proprio hash. Puoi specificarlo dopo `git reset --hard` per tornare a un commit preciso. Ecco un esempio:

```bash
git reset --hard <commitHash>
```

Normalmente Git riconosce il commit anche se ne specifichi solo i primi 8-10 caratteri, purche' siano sufficienti a identificarlo univocamente.

## 0B.11. Collaborazione con Git

Un flusso tipico di collaborazione e' il seguente:

1.  Clone repository

```bash
git clone https://github.com/org/project.git
```

2.  Create branch

```bash
git checkout -b feature-auth
```

3.  Work and commit

```bash
git add .
git commit -m "Add authentication"
```

4.  Push branch

```bash
git push origin feature-auth
```

5.  Open Pull Request on GitHub

6.  After review → merge into `main`

Update local repository:

```bash
git pull origin main
```

### 0B.12. Command Summary

Here is a quick command summary:

```bash
----------------------- ------------------------
Command                 Purpose
----------------------- ------------------------
git init                create repository
git clone               copy remote repository
git add                 stage changes
git commit              save snapshot
git push                upload commits
git pull                download changes
git branch              manage branches
git checkout            change branch
git reset               undo commits
git log                 show history
----------------------- ------------------------
```
