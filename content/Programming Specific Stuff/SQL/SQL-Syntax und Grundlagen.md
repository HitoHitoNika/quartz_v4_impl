---
tags:
  - SQL
---
Zurück zu [[Inhaltsübersicht Prog|Programmier Zeugs]]

- [[#SQL-Grundstruktur|SQL-Grundstruktur]]
- [[#Datentypen|Datentypen]]
- [[#Abfragen (SELECT-Anweisungen)|Abfragen (SELECT-Anweisungen)]]
- [[#Daten einfügen, aktualisieren und löschen|Daten einfügen, aktualisieren und löschen]]

## SQL-Grundstruktur

SQL-Anweisungen werden durch Semikolons beendet. Eine einfache SQL-Anweisung könnte folgendermaßen aussehen:

```SQL
SELECT Spalte1, Spalte2 FROM Tabelle WHERE Bedingung;
```

- `SELECT`: Wählt die angegebenen Spalten aus der Tabelle aus.
- `FROM`: Gibt an, aus welcher Tabelle die Daten ausgewählt werden sollen.
- `WHERE`: Setzt eine Bedingung fest, die erfüllt sein muss, damit die Daten ausgewählt werden.

## Datentypen

SQL verwendet verschiedene Datentypen, um den Typ von Daten in einer Tabelle zu definieren. Einige gängige Datentypen sind:

- **INT**: Ganzzahlen.
- **VARCHAR(n)**: Zeichenketten mit einer maximalen Länge von n Zeichen.
- **DATE**: Datumswerte.
- **BOOLEAN**: Wahrheitswerte (TRUE oder FALSE).

Beispiel:

```SQL
CREATE TABLE Mitarbeiter (     MitarbeiterID INT,     Name VARCHAR(50),     Geburtsdatum DATE,     Aktiv BOOLEAN );
```

## Abfragen (SELECT-Anweisungen)

### Einfache SELECT-Anweisung

```SQL
SELECT Spalte1, Spalte2 FROM Tabelle;
```

### Bedingte Abfrage

```SQL
SELECT * FROM Produkte WHERE Preis > 50;
```

### Sortieren der Ergebnisse

```SQL
SELECT * FROM Kunden ORDER BY Nachname ASC;
```

## Daten einfügen, aktualisieren und löschen

### Einfügen von Daten

```SQL
INSERT INTO Tabelle (Spalte1, Spalte2) VALUES (Wert1, Wert2);
```
### Aktualisieren von Daten

```SQL
UPDATE Tabelle SET Spalte1 = Wert1 WHERE Bedingung;
```
### Löschen von Daten

```SQL
DELETE FROM Tabelle WHERE Bedingung;
```
## Weitere Ressourcen
- [[SQL-Übersicht]]
- [[Weitere SQL Befehle]]
- [[Häufig gestellte Fragen]]