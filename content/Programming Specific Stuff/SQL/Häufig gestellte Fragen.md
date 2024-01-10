---
tags:
  - SQL
---
## 1. Was ist der Unterschied zwischen SQL und MySQL?

SQL steht für Structured Query Language und ist die Sprache, die zur Kommunikation mit relationalen Datenbanken verwendet wird. MySQL hingegen ist ein konkretes relationales Datenbankmanagementsystem (RDBMS), das SQL als Abfragesprache verwendet.

## 2. Wie erstelle ich eine Datenbank in SQL?

Um eine Datenbank zu erstellen, verwenden Sie den Befehl `CREATE DATABASE` gefolgt vom Namen der Datenbank. Beispiel:

```sql
CREATE DATABASE MeineDatenbank;
```

## 3. Was sind Indizes und warum sind sie wichtig?

Indizes sind Datenstrukturen, die den Datenzugriff beschleunigen, indem sie eine sortierte Reihenfolge der Daten bereitstellen. Sie sind wichtig, um Abfragen effizienter zu gestalten.

## 4. Wie erstelle ich eine Tabelle in SQL?

Verwenden Sie den Befehl `CREATE TABLE` gefolgt von den Spalten und ihren Datentypen. Beispiel:

```sql
CREATE TABLE Kunden (
    KundenID INT PRIMARY KEY,
    Vorname VARCHAR(50),
    Nachname VARCHAR(50)
);
```

## 5. Was ist der Unterschied zwischen INNER JOIN und LEFT JOIN?

INNER JOIN gibt nur die übereinstimmenden Datensätze beider Tabellen zurück, während LEFT JOIN alle Datensätze der linken Tabelle und die übereinstimmenden Datensätze der rechten Tabelle zurückgibt.

## 6. Wie füge ich Daten in eine Tabelle ein?

Verwenden Sie den Befehl `INSERT INTO` gefolgt von der Tabelle und den Werten. Beispiel:

```sql
INSERT INTO Kunden (Vorname, Nachname) VALUES ('Max', 'Mustermann');
```

## 7. Was ist eine gespeicherte Prozedur?

Eine gespeicherte Prozedur ist eine vordefinierte SQL-Anweisung, die unter einem Namen gespeichert und bei Bedarf aufgerufen werden kann. Sie erleichtert die Wiederverwendung von Code und die Organisation komplexer Abläufe.

## 8. Wie kann ich Duplikate in einer Tabelle vermeiden?

Sie können die Eindeutigkeit von Daten sicherstellen, indem Sie einen Primärschlüssel auf einer oder mehreren Spalten festlegen.

Diese Fragen bieten eine gute Grundlage für die FAQ-Seite. Sie können sie an die Bedürfnisse Ihrer Zielgruppe anpassen und bei Bedarf weitere Fragen hinzufügen.

Natürlich, hier sind weitere Fragen, die Sie zu Ihrer SQL-FAQ-Seite hinzufügen können:

## 9. Wie lösche ich Daten aus einer Tabelle?

Um Daten aus einer Tabelle zu löschen, verwenden Sie den Befehl `DELETE FROM` gefolgt von der Tabelle und der WHERE-Klausel, um die zu löschenden Datensätze auszuwählen.

```sql
DELETE FROM Kunden WHERE KundenID = 123;
```

## 10. Was sind Trigger in SQL?

Trigger sind spezielle gespeicherte Prozeduren, die automatisch ausgeführt werden, wenn bestimmte Ereignisse in einer Tabelle eintreten, wie z.B. das Einfügen, Aktualisieren oder Löschen von Datensätzen.

## 11. Wie ändere ich die Struktur einer bestehenden Tabelle?

Sie können die Struktur einer Tabelle mit dem Befehl `ALTER TABLE` ändern. Zum Beispiel, um eine Spalte hinzuzufügen:

```sql
ALTER TABLE Mitarbeiter ADD COLUMN Geburtsdatum DATE;
```

## 12. Was sind Aggregate-Funktionen in SQL?

Aggregate-Funktionen wie SUM, AVG, COUNT, MIN und MAX werden verwendet, um Berechnungen über eine Gruppe von Datensätzen durchzuführen, z.B. den Durchschnitt oder die Summe von Werten.

```sql
SELECT AVG(Gehalt) FROM Mitarbeiter;
```

## 13. Wie gruppiere ich Datensätze in SQL?

Die GROUP BY-Klausel wird verwendet, um Datensätze zu gruppieren, basierend auf den Werten einer oder mehrerer Spalten.

```sql
SELECT Abteilung, AVG(Gehalt) FROM Mitarbeiter GROUP BY Abteilung;
```
