---
tags:
  - SQL
---
## Aggregate-Funktionen

Aggregate-Funktionen wie SUM, AVG, COUNT, MIN und MAX werden verwendet, um Berechnungen über eine Gruppe von Datensätzen durchzuführen, z.B. den Durchschnitt oder die Summe von Werten.

```sql
SELECT AVG(Gehalt) FROM Mitarbeiter;
```

## JOIN-Operationen

Die JOIN-Operation ermöglicht das Verknüpfen von Daten aus mehreren Tabellen basierend auf bestimmten Bedingungen. Es gibt verschiedene Arten von JOINs, darunter INNER JOIN, LEFT JOIN, RIGHT JOIN und FULL JOIN.

### INNER JOIN

Der INNER JOIN kombiniert Datensätze aus zwei Tabellen, basierend auf einer angegebenen Bedingung. In diesem Beispiel werden nur die Datensätze angezeigt, die in beiden Tabellen übereinstimmen.

```sql
SELECT Kunden.Name, Bestellungen.Bestelldatum FROM Kunden INNER JOIN Bestellungen ON Kunden.KundenID = Bestellungen.KundenID;
```

Hier werden Kundeninformationen mit Bestelldaten verknüpft, wobei nur Daten für Kunden angezeigt werden, die auch Bestellungen getätigt haben.

### LEFT JOIN

Der LEFT JOIN gibt alle Datensätze der linken Tabelle (in diesem Fall Kunden) und die übereinstimmenden Datensätze der rechten Tabelle (Bestellungen) zurück.

```sql
SELECT Kunden.Name, Bestellungen.Bestelldatum FROM Kunden LEFT JOIN Bestellungen ON Kunden.KundenID = Bestellungen.KundenID;
```

Dieses Beispiel zeigt alle Kunden an, unabhängig davon, ob sie Bestellungen getätigt haben.
### RIGHT JOIN

Der RIGHT JOIN gibt alle Datensätze der rechten Tabelle (in diesem Fall Bestellungen) und die übereinstimmenden Datensätze der linken Tabelle (Kunden) zurück.

```sql
SELECT Kunden.Name, Bestellungen.Bestelldatum
FROM Kunden
RIGHT JOIN Bestellungen ON Kunden.KundenID = Bestellungen.KundenID;
```

Dieses Beispiel zeigt alle Bestellungen an, unabhängig davon, ob sie einem Kunden zugeordnet sind.

### FULL JOIN

Der FULL JOIN gibt alle Datensätze zurück, wenn es eine Übereinstimmung in einer der beiden Tabellen gibt. Falls keine Übereinstimmung vorhanden ist, werden NULL-Werte für die nicht übereinstimmenden Spalten zurückgegeben.

```sql
SELECT Kunden.Name, Bestellungen.Bestelldatum
FROM Kunden
FULL JOIN Bestellungen ON Kunden.KundenID = Bestellungen.KundenID;
```

Hier werden alle Kunden und Bestellungen angezeigt, und NULL-Werte werden für nicht übereinstimmende Datensätze eingefügt.

## Unterabfragen (Subqueries)

Unterabfragen sind SELECT-Anweisungen, die in andere SELECT-Anweisungen eingebettet sind. Sie werden oft in WHERE-Klauseln verwendet, um Bedingungen zu verfeinern.

```sql
SELECT Name FROM Kunden WHERE KundenID IN (SELECT KundenID FROM Bestellungen WHERE Bestellbetrag > 1000);
```

Hier werden Kunden angezeigt, die Bestellungen mit einem Bestellbetrag über 1000 Euro getätigt haben.

## Indizes und Leistungsoptimierung

Indizes beschleunigen den Zugriff auf Daten, indem sie eine sortierte Reihenfolge der Daten bereitstellen. Ein Index kann auf einer oder mehreren Spalten erstellt werden, um die Abfrageleistung zu verbessern.

```sql
CREATE INDEX idx_Nachname ON Kunden (Nachname);
```

In diesem Beispiel wird ein Index auf der Spalte "Nachname" der Tabelle "Kunden" erstellt.

## Transaktionen

Transaktionen ermöglichen es, mehrere SQL-Anweisungen als eine atomare Einheit auszuführen, was bedeutet, dass alle Änderungen entweder vollständig durchgeführt oder rückgängig gemacht werden.

```sql
BEGIN TRANSACTION; UPDATE Konto SET Guthaben = Guthaben - 100 WHERE KontoID = 123; UPDATE Konto SET Guthaben = Guthaben + 100 WHERE KontoID = 456; COMMIT;
```

Hier werden zwei Updates als Teil einer Transaktion ausgeführt, und beide müssen erfolgreich sein, damit die Transaktion abgeschlossen wird.

## Gespeicherte Prozeduren

Gespeicherte Prozeduren sind vordefinierte SQL-Anweisungen, die unter einem Namen gespeichert und bei Bedarf aufgerufen werden können.

```sql
CREATE PROCEDURE GetKundenByLand (IN Land CHAR(2)) BEGIN     SELECT * FROM Kunden WHERE KundenLand = Land; END;
```

In diesem Beispiel wird eine gespeicherte Prozedur erstellt, die alle Kunden für ein bestimmtes Land zurückgibt.

## Weitere Ressourcen

- [SQL-Optimierungstechniken](Link zur Seite mit Optimierungstechniken)
- [Fortgeschrittene SQL-Funktionen](Link zu fortgeschrittenen Funktionen)