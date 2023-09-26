# GitHub Productivity Tipps

## GitHub Web-UI

- Tastenkombinationen: [GitHub Keyboard Shortcuts](https://docs.github.com/en/get-started/using-github/keyboard-shortcuts)
    - `?` öffnet die Hilfe für alle Tastenkombinationen
    - `esc` schließt UI-Fenster und Pop-ups
    - `gn` geht zu Benachrichtigungen 
    - `Ctrl-K` und `Ctrl-Shift-K` für einfache Navigation
    - `/` durchsucht das Repository
    - `t` zeigt eine Dateibaumansicht und erleichtert die Suche nach Dateien
    - `.` und `>` öffnen VS Code im Browser
    - `gc`, `gp` und `gi` gehen zu Code, Pull Requests und Issues
        - `j` geht in der Liste nach unten
        - `k` geht in der Liste nach oben
        - `enter` oder `o` öffnet den Pull Request
        - `.` oder `>` öffnet den Pull Request im Editor

- [Vorschläge in Pull Requests](https://docs.github.com/de/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/commenting-on-a-pull-request)

- [Gespeicherte Antworten in Pull Requests](https://docs.github.com/en/get-started/writing-on-github/working-with-saved-replies/using-saved-replies)

- Notifier für GitHub ([Browser-Erweiterung](https://github.com/sindresorhus/notifier-for-github))

- [Markdown-Formatierungstipps](https://github.blog/2020-04-09-github-protips-tips-tricks-hacks-and-secrets-from-lee-reilly/#6-must-have-markdown-formatting-tips)

## GitHub CLI

### `gh repo`

  - list 
    ```shell
    # Zeigt eine einfache Liste aller Repositories mit Python an
    $ gh repo list -l python
    ```
  - create
    ```shell
    # Erstellt ein Repository Schritt für Schritt
    $ gh create repo
    ```
  - delete
    ```shell
    # Löscht das Repository im Repository-Verzeichnis selbst: 
    gh repo delete
    ```
  - edit
    ```shell
    # Geht einige Einstellungen in der Konsole interaktiv durch
    $ gh repo edit
    ```

### `gh pr`

- list
    ```shell
    # Zeigt Pull Requests an, die von Ihnen erstellt wurden
    $ gh pr list --author "@me"

    # Zeigt nur Pull Requests mit allen angegebenen Labels an
    $ gh pr list --label bug --label "priority 1"

    # Filtert Pull Requests mit Suchsyntax nach erfolgreichem Status und erforderlicher Überprüfung
    $ gh pr list --search "status:success review:required"

    # Findet einen Pull Request, der einen bestimmten Commit eingeführt hat
    $ gh pr list --search "<SHA>" --state merged
    ```

- create
    ```shell
    # Erstellt einen neuen Pull Request mit einem interaktiven Dialog
    $ gh pr create

    # Erstellt einen neuen Pull Request mit dem Titel "Mein neuer Feature" und der Beschreibung "Dies ist eine Beschreibung"
    $ gh pr create --title "Mein neuer Feature" --body "Dies ist eine Beschreibung"

    # Erstellt einen neuen Pull Request und stellt ihn von dem Branch "mein-feature-branch" zum Branch "main"
    $ gh pr create --base main --head mein-feature-branch

    # Erstellt einen neuen Pull Request und fügt "monalisa" und "hubot" als Reviewer hinzu
    $ gh pr create --reviewer monalisa,hubot

    # Erstellt einen neuen Pull Request mit Labels "bug" und "help wanted"
    $ gh pr create --label bug,help-wanted
    ``````

- edit
    ```shell
    # Öffnet den Pull Request mit der Nummer 123 im Editor
    $ gh pr edit 123
    
    # Bearbeitet den Titel und die Beschreibung des Pull Requests mit der Nummer 23
    $ gh pr edit 23 --title "Ich habe einen Fehler gefunden" --body "Nichts funktioniert"
    
    # Fügt die Reviewer "monalisa" und "hubot" zum Pull Request mit der Nummer 23 hinzu und entfernt den Reviewer "myorg/team-name"
    $ gh pr edit 23 --add-reviewer monalisa,hubot --remove-reviewer myorg/team-name

    # Fügt "@me" (user vom gh tool) zum Pull Request mit der Nummer 23 hinzu und entfernt die Assignees "monalisa" und "huboe"
    $ gh pr edit 23 --add-assignee "@me" --remove-assignee monalisa,huboe
    ```

- view
    ```shell 
    # Zeigt Kommentare zu einem Pull Request an:
    $ gh pr view --comments 123

    # Öffnet im Webbrowser: 
    $ gh pr view -w 123
    ```
- review
    ```shell
    # Genehmigt einen Pull Request
    $ gh pr review --approve
    
    # Hinterlässt einen Review-Kommentar für den aktuellen Branch
    $ gh pr review --comment -b "interessant"
    
    # Fügt einen Review für einen bestimmten Pull Request hinzu
    $ gh pr review 123
    
    # Fordert Änderungen an einem bestimmten Pull Request an
    $ gh pr review 123 -r -b "braucht mehr ASCII-Kunst"
    ```
- merge
    
    ```shell
    # Mergt den Pull Request mit der Nummer 123 automatisch, ohne dass eine manuelle Bestätigung erforderlich ist
    $ gh pr merge 123 --auto

    # Squasht die Commits im Pull Request mit der Nummer 123 und fügt den Kommentar "Dies ist der Kommentar des Squash-Commits" hinzu
    $ gh pr merge 123 --squash -s "Dies ist der Kommentar des Squash-Commits"

    # Rebaset den Pull Request mit der Nummer 124 und fügt die Option `--admin` hinzu, um sicherzustellen, dass der Merge als Administrator durchgeführt wird.
    $ gh pr merge 124 --rebase --admin

    # Mergt den Pull Request mit der Nummer 123 automatisch und löscht den Branch nach dem Merge.
    $ gh pr merge 123 --auto --delete-branch    
    ```

### `gh issue`

- list
    ```shell
    # Zeigt eine Liste aller Issues an
    $ gh issue list
    
    # Zeigt alle offenen oder geschlossenen Issues an
    $ gh issue list -s all/closed/open
    ```
    
- create
    ```shell
    # Erstellt ein Issue
    $ gh issue create --title "Ich habe einen Fehler gefunden" --body "Nichts funktioniert" --label "bug,help wanted" --assignee "@me"
    ```
    
- edit
    ```shell
    # Bearbeitet das Issue mit der Nummer 123 im Editor
    $ gh issue edit 123
    
    # Fügt die Labels "bug" und "help wanted" zum Issue mit der Nummer 23 hinzu und entfernt das Label "core"
    $ gh issue edit 23 --add-label "bug,help wanted" --remove-label "core"
    
    # Fügt "@me" zum Issue mit der Nummer 23 hinzu und entfernt die Assignees "monalisa" und "hubot"
    $ gh issue edit 23 --add-assignee "@me" --remove-assignee monalisa,hubot
    ```
    
- close
    ```shell
    # Schließt das Issue mit der Nummer 23 mit einem Kommentar
    $ gh issue close 23 -c "Duplicated issue."
    ```
    
- develop
    ```shell
    # Erstellt und wechselt zu einem Branch für das Issue mit der Nummer 123
    $ gh issue develop 123 --checkout
    ```

### `gh gist`

- **list**
    ```shell
    # Zeigt eine Liste aller öffentlichen Gists an
    $ gh gist list --public
    ```
    
- **create**
    ```shell
    # Veröffentlicht die Datei `hello.py` als öffentlichen Gist
    $ gh gist create --public hello.py
    
    # Erstellt einen Gist mit einer Beschreibung
    $ gh gist create hello.py -d "Mein Hello-World-Programm in Python"
    
    # Erstellt einen Gist mit mehreren Dateien
    $ gh gist create hello.py world.py cool.txt
    
    # Erstellt einen Gist aus der Standardeingabe
    $ gh gist create -
    
    # Erstellt einen Gist aus der Ausgabe eines anderen Befehls
    $ cat cool.txt | gh gist create
    ```
    
- **view**
    ```shell
    # Zeigt einen Gist an
    $ gh gist view 939849392843
    ```
    
- **edit**
    ```shell
    # Fügt eine `readme.md`-Datei zu einem Gist hinzu
    $ gh gist edit 939849392843 -a readme.md
    
    # Bearbeitet den Inhalt eines Gists direkt
    $ gh gist edit 939849392843 -f readme.md
    ```
