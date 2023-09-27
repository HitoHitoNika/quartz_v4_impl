Zurück zu [[Inhaltsübersicht Prog|Programming Shit]]

Git-Submodule sind eine Möglichkeit, andere Git-Repositories in ein Hauptrepository einzubinden, sodass Sie Teile eines anderen Repositories als Unterordner in Ihrem Hauptrepository verwenden können. Dies ist besonders nützlich, wenn Sie Abhängigkeiten von externen Projekten verwalten möchten oder wenn Sie ein Modulsystem für Ihre Projekte benötigen. Hier ist eine detaillierte Erklärung, wie Git-Submodule funktionieren:

<h3 align="center">Hinzufügen eines Submodules </h3>

Um ein Submodul zu Ihrem Hauptrepository hinzuzufügen, verwenden Sie den Befehl `git submodule add`. Die allgemeine Syntax lautet:

```bash
git submodule add <URL zum Submodul-Repository> <Zielverzeichnis>
```

Dieser Befehl fügt das externe Repository als Submodul im angegebenen Zielverzeichnis in Ihrem Hauptrepository hinzu.

<h3 align="center"> Initialisieren und Aktualisieren von Submodulen </h3>

Nachdem Sie ein Submodul hinzugefügt haben, müssen Sie es initialisieren und die Daten abrufen. Verwenden Sie dazu die folgenden Befehle:

```bash
git submodule init  # Initialisiert die Submodule (nur einmal notwendig)

git submodule update --remote  # Aktualisiert die Submodule auf die neueste Version
```

Diese Befehle sorgen dafür, dass das Submodul in seinem aktuellen Zustand auf Ihren lokalen Arbeitsbereich angewendet wird.

<h3 align="center"> Arbeiten mit Submodulen </h3>

In Ihrem Hauptrepository verhalten sich Submodule wie eigenständige Git-Repositories. Sie können in das Verzeichnis des Submoduls wechseln, Änderungen vornehmen, committen und pushen, genauso wie Sie es in einem normalen Git-Repository tun würden.

<h3 align="center">Aktualisieren von Submodulen in Ihrem Hauptrepository</h3>

Wenn Sie Änderungen im Submodul-Repository vornehmen und diese in Ihrem Hauptrepository verwenden möchten, müssen Sie in Ihrem Hauptrepository das Submodul aktualisieren. Gehen Sie dazu in das Hauptrepository-Verzeichnis und verwenden Sie den Befehl:

```bash
git submodule update --remote
```

Dies wird das Submodul auf den neuesten Stand bringen und die Referenz auf den bestimmten Commit aktualisieren, den das Submodul in Ihrem Hauptrepository verwendet.

<h3 align="center">Commiten von Änderungen in Ihrem Hauptrepository</h3>

Nachdem Sie das Submodul aktualisiert haben, müssen Sie in Ihrem Hauptrepository einen Commit erstellen, um die aktualisierte Submodul-Referenz festzuhalten. Führen Sie dazu die folgenden Schritte aus:

```bash
git add Pfad/zu/Unterverzeichnis
git commit -m "Aktualisieren des Submoduls auf die neueste Version"
```

Dadurch wird die Aktualisierung des Submoduls in Ihrem Hauptrepository festgehalten.

