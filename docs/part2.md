# Teil 2 - Update Code

In der vorherigen Übung habt ihr ein Job-Template in der Automation Platform erstellt mit einem Survey zur Personalisierung des Webservers.  
Damit euer Name ebenfalls in der Auswahlliste des *Surveys* auftaucht, muss der *Code* (die *Listen*-Variable) angepasst werden.  
Ihr durchlauft dabei einen typischen *Entwicklungs-Workflow*, ihr verwendet das Versionskontroll-Tool *Git* und (den Git-Hosting-Service) *Github*, erstellt einen *Issue*, werdet auf der Kommandozeile den Code nach euren Wünschen anpassen und anschließend einen *Merge Request* (*Pull Request*) erstellen.

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

## 1. Vom Remote Repository zum lokalen Repository

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
[student1@ansible-1 qep]$ git status
On branch dev
Your branch is up to date with 'origin/dev'.

nothing to commit, working tree clean
```

> Du befindest dich auf dem `dev`-Branch. Dieser Branch ist *schreibgeschützt* (lediglich über einen Pull Request können Änderungen hinzugefügt werden).

Erstelle einen eigenen (lokalen) Branch mit eurem Namen, in der Form `feature/<dein-name>`:

```console
git checkout -b feature/name
```

!!! warning "Alles korrekt?"
    Hast du `name` gegen deinen eigenen Namen ausgetauscht?

Du hast vom `dev`-Branch einen weiteren Branch abgezweigt, auf diesem wirst du deine Änderungen hinterlegen. Du kannst mit `git status` erneut prüfen.

## 2. Variablen-Datei anpassen

Füge in der Datei `variables.yml` deinen Namen in der Liste hinzu, damit das *Survey* im *Controller Automation* Template diesen als Option für den personalisierten Webserver anbietet.  
Du kannst die Datei im *Explorer* links anklicken, sie wird *Code Editor* geöffnet und kann dort editiert werden:

![Variable File Opened](assets/images/CodeVariableFile.png)

Die Datei ist im sog. *YAML*-Format (ein Datenserialisierungsformat), füge in der Variablen `attendee_list` deinen Namen als weiteren Listeneintrag hinzu (beginnt mit einem *Minus* (*Dash*) Symbol), achte dabei auf die Einrückung (zwei Leerzeichen vor dem *Minus*-Symbol)

!!! abstract "Inhalt der Variablen-Datei vor der Anpassung"

    ```{ .yaml .no-copy }
    --8<-- "variables.yml"
    ```

Am Ende sollte die Datei folgendermaßen aussehen (mit eurem Namen natürlich):

```yaml
---
# variable file for Ansible playbooks
package: httpd

attendee_list:
  - Tim Grützmacher
  - Eslem Bayraktar
```
