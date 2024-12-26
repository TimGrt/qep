# Teil 2 - Update Code

Damit euer Name ebenfalls in der Auswahlliste des *Surveys* auftaucht, muss der *Code* (die *Listen*-Variable) angepasst werden.  
Ihr durchlauft dabei einen typischen *Entwicklungs-Workflow*, ihr verwendet das Versionskontroll-Tool *Git* und *Github*, erstellt einen *Issue*, werdet auf der Kommandozeile den Code nach euren Wünschen anpassen und anschließend einen *Merge Request* erstellen.

``` { .mermaid }
gitGraph
   commit
   commit
   branch dev
   checkout dev
   commit
   branch feature/name
   checkout feature/name
   commit
   checkout dev
   merge feature/name
   checkout main
   merge dev
   commit type:HIGHLIGHT
```

## Vom Remote Repository zum lokalen Repository

Das Projekt vom *Remote Repository* herunterladen (*klonen*):

```console
git clone https://github.com/TimGrt/qep.git
```

Ein neuer Ordner ist entstanden, in diesen wechseln (*cd* means *change directory*):

```console
cd qep
```

Du bist jetzt in einem *git-versionierten* Ordner, prüfe mit dem Kommando `git status`, der Output sollte folgendermaßen aussehen:

``` { .console .no-copy }
$ git status
On branch dev
Your branch is up to date with 'origin/dev'.

nothing to commit, working tree clean
```

