---
tags:
  - Java
---
JUnit ist ein Test-Framework, welches Entwicklern hilft automatisierte Test für Projekte zu erstellen.

## Einbindung ins Projekt

Es gibt 2 Arten JUnit einzubinden. Ich werde hier auf den einfacheren eingehen mit [[Maven]].

Dafür fügen wir unserer pom.xml einfach folgende Dependency hinzu:

```xml
<dependencies>
    <!-- Andere Abhängigkeiten -->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>5.0.0</version> <!-- Beispielversion, verwenden Sie die gewünschte Version -->
        <scope>test</scope>
    </dependency>
</dependencies>

```