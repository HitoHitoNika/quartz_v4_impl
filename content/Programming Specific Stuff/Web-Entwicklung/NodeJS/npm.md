
npm (Node Package Manager) ist ein leistungsstarkes Paketverwaltungswerkzeug für JavaScript und Node.js. Es wird standardmäßig mit Node.js installiert und ermöglicht es Entwicklern, Open-Source-Pakete herunterzuladen, zu verwalten und in ihren Projekten zu verwenden. Hier ist ein Überblick über npm und ein Cheat Sheet mit häufig verwendeten Befehlen:

## Was ist npm?

npm ist das Standard-Paketverwaltungstool für JavaScript und Node.js. Es wurde entwickelt, um die Installation und Verwaltung von Drittanbieterpaketen und Abhängigkeiten in JavaScript-Projekten zu erleichtern. Mit npm können Entwickler Pakete aus einem zentralen Repository herunterladen, Abhängigkeiten verwalten und sicherstellen, dass ihre Projekte reibungslos funktionieren.

## Merkmale von npm

- **Paketverwaltung**: npm ermöglicht es Entwicklern, Pakete zu suchen, zu installieren und zu aktualisieren, die von der JavaScript-Community erstellt wurden. Diese Pakete können Bibliotheken, Frameworks, Tools und mehr umfassen.

- **Lokale Projektabhängigkeiten**: npm erlaubt es Entwicklern, Abhängigkeiten lokal für jedes Projekt zu installieren, um sicherzustellen, dass Projekte in verschiedenen Umgebungen konsistent ausgeführt werden können.

- **Skriptausführung**: Entwickler können in der `package.json`-Datei benutzerdefinierte Skripte definieren und mit npm ausführen. Dies ist nützlich für häufig verwendete Aufgaben wie das Kompilieren von Code oder das Ausführen von Tests.

- **Versionierung**: npm ermöglicht es Entwicklern, spezifische Versionen von Paketen zu installieren, um die Stabilität ihrer Projekte sicherzustellen.

- **Veröffentlichung von Paketen**: Entwickler können ihre eigenen JavaScript-Pakete über npm veröffentlichen und so zur Open-Source-Community beitragen.

## Cheat Sheet für npm

### Installation von Paketen

- **Paket installieren (lokal)**: `npm install <package-name>`

- **Paket installieren (global)**: `npm install -g <package-name>`

### Abhängigkeiten verwalten

- **Paket zur Abhängigkeitenliste hinzufügen**: `npm install <package-name> --save`

- **Paket zur Entwicklungsabhängigkeitenliste hinzufügen**: `npm install <package-name> --save-dev`

### Projektverwaltung

- **Projekt initialisieren (Erstellen einer package.json-Datei)**: `npm init`

- **Paket- und Abhängigkeitsaktualisierung**: `npm update`

### Verwendung von Skripten

- **Skript ausführen**: `npm run <script-name>`

### Paketveröffentlichung

- **Paket veröffentlichen**: `npm publish`

- **Paket aktualisieren**: `npm version <new-version>`
