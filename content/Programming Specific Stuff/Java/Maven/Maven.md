---
tags:
  - Java
  - Guide
---
Zurück zu [[Inhaltsübersicht Prog|Programming Shit]]
## Was ist Maven?

Maven ist ein Buildtool für Java, welches den Bau des Programmes übernimmt. Darunter fallen unteranderem die Anschaffung von außen stehenden Bibliotheken.

## Wofür nutzt man Maven ?

Maven bietet viele Möglichkeiten Unterstützung im Java Build Prozess zu bieten. Das wichtigste ist jedoch die Möglichkeit, Bibliotheken von außen sich dazu zu ziehen ohne diese von Hand hinzuzufügen. 
Außerdem kann man mit Maven die Java Version des Projekts festlegen, um Versionskonflikte zu vermeiden..

## Wie wird das ganze umgesetzt?

Für die Umsetzung muss man zunächst ein Maven Projekt anlegen (Wird in dem meisten IDE´s angeboten). Wenn man dieses angelegt hat findet man in der Ordnerstruktur eine "pom.xml" Datei.
In dieser können wir Abhängigkeiten etc definieren. 
<hr>

==Klicke [hier](https://www.jrebel.com/blog/maven-cheat-sheet) um auf ein Cheatsheet zu gelangen.== 


## Wie sieht ein Maven Projekt aus ?

Die Grundstruktur des Projekts sieht so aus:

![[Spring Project Aufbau.png]]

Wir sehen jedoch noch 2 "mvnw" Dateien. Diese sind dafür da um Maven local starten zu können, ohne das Maven installiert ist. Genauer ist
- mvnw.cmd
	- Für Windows
- mvnw 
	- Für Mac und Linux
