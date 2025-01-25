# Teil 2 - Arbeiten mit Git

In der vorherigen Übung hast du automatisiert ein Job-Template in der Ansible Automation Platform erstellt, welches über ein *Survey* (eine interaktive Abfrage) die Möglichkeit bietet, den Webserver (bzw. die vielen Webserver, es werden tatsächlich drei Webserver-Instanzen erstellt) zu personalisieren.  
Die Abfrage bietet aktuell nur einen einzelnen Namen an, damit auch dein Name dort auftaucht, musst du den Code selbst anpassen.  
Die Erstellung der Ressourcen war eine klassische *Ops*-Aufgabe, jetzt wirst eine *Developer*-Aufgabe übernehmen.  
Die Code-Anpassung erfordert, dass du dich mit dem Versionskontroll-Tool *Git* vertraut machst, die folgenden Schritte bereiten dich und deine Entwicklungsumgebung darauf vor.

## 1. VSCode Entwicklungsumgebung öffnen

Um den *Code* anzupassen, verwendest du VScode (eine IDE = Integrated Developer Environment), dort ist alles installiert was du zur Programmierung brauchst. Keine Sorge, wirklich programmieren musst du heute gar nicht.  

Auf der Übersichts-Seite des Workshops in der Red Hat Demo Umgebung den Link zu **VS Code** wählen, dein Trainer geht mit dir die einzelnen Schritte durch, um VSCode erstmalig einzurichten.

## 2. SSH-Schlüsselpaar erstellen

Um den notwendigen Code (das *Repository*) herunterladen zu können und, noch wichtiger, anpassen und wieder hochladen zu können, benötigst du ein *Schlüsselpaar*.  

Öffne ein Terminal in VSCode und gib das folgende Kommando ein:

```console
ssh-keygen -t ed25519
```

!!! tip
    Kopiere dir das Kommando über den *Copy*-Button rechts im Code-Fenster.

Die Abfragen kannst du einfach mit ++enter++ bestätigen (drei Mal bestätigen), die Ausgabe sieht in etwa so aus:

```{ .console .no-copy }
[student1@ansible-1 qep]$ ssh-keygen -t ed25519
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/student1/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/student1/.ssh/id_ed25519.
Your public key has been saved in /home/student1/.ssh/id_ed25519.pub.
The key fingerprint is:
SHA256:8HXsZw6mD5m6PNl6WHoiYy0B/Il+1zRHVrfcpR+rZpI student1@ansible-1.example.com
The key's randomart image is:
+--[ED25519 256]--+
|                 |
|           .  . o|
|   .  .   . o..o+|
|    o  o . oo .+.|
|     + .S  o+ o.o|
|    . +   +=.= ..|
|   .   o O=o. o  |
|    . *.O.=E +   |
|     o ==B  =    |
+----[SHA256]-----+
```

Du hast ein neues SSH (Secure Shell) Schlüsselpaar erstellt, einen *privaten* Schlüssel und einen *öffentlichen* Schlüssel (mit der Endung `.pub` für *public*), welchen du gefahrlos verbreiten darfst. Wir werden diesen öffentlichen Schlüssel im nächsten Schritt benötigen, du kannst ihn dir bereits einmal auf der Kommandozeile anzeigen lassen, von dort kannst du ihn gleich markieren und kopieren.

```console
cat ~/.ssh/id_ed25519.pub
```

??? example "Beispielausgabe"

    ```{ .console .no-copy }
    [student1@ansible-1 qep]$ cat ~/.ssh/id_ed25519.pub
    ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDt+WFoUBWhs77m/784FaT+eqqavHf/Jz/+8DW04l2fP student1@ansible-1.example.com
    ```

## 3. Öffentlichen Schlüssel in Github hinterlegen

Den **öffentlichen** Schlüssel (mit der `.pub`-Endung) musst du in deinem Github-Account hinterlegen.

Im Github-Browser-Fenster, klicke rechts oben auf dein Nutzer-Bild und wähle **Settings**.  

Auf der linken Seite (unter dem Punkt *Access**), klicke auf **SSH and GPG keys**. Noch sind keine Keys hinterlegt, klicke auf den Button **New SSH key**.  

Kopiere den Inhalt des **öffentlichen** Schlüssel, als Titel kannst du *QEP* hinterlegen. Wenn alles eingefügt ist, klicke unten auf den Button **Add SSH key**.

Du solltest von deinem Trainer als Entwickler zum Projekt hinzugefügt worden sein, in der folgenden Aufgabe lädst du dir den Code auf deine Entwicklungsumgebung.

## 4. Vom Remote Repository zum lokalen Repository

Das Projekt vom *Remote Repository* herunterladen (*klonen*):

```console
git clone git@github.com:TimGrt/qep.git
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

Erstelle einen eigenen (lokalen) Branch mit deinem Namen, in der Form `feature/<dein-name>`:

```console
git checkout -b feature/name
```

!!! warning "Alles korrekt?"
    Hast du `name` gegen deinen eigenen Namen ausgetauscht?

Du hast vom `dev`-Branch einen weiteren Branch abgezweigt, auf diesem wirst du deine Änderungen hinterlegen. Du kannst mit `git status` erneut prüfen.

Ok ,nach den ganzen Vorbereitungen kannst du im nächsten Schritt dann endlich die Code-Anpassungen vornehmen!

!!! tip
    Damit das Ganze in VScode noch etwas übersichtlicher wird, kannst du dir den Projektordner öffnen. Klicke im Menüband auf **File** und **Open Folder...**, wählen den `qep` Ordner (darin befindet sich dein versionkontrollierter Projekt-Ordner welchen du gerade erstellt hast).  
    Jetzt siehst du im Explorer nur noch den Inhalt des Projektordners, das Ganze hat noch ein paar weitere Vorteile, dein Trainer kann dir das Ganze noch näher erklären.
