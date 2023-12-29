## Aufgabe 1

**Tabelle "Auto":**

| Attribut            | Datentyp | Wertebereich                                   |
|---------------------|----------|------------------------------------------------|
| Hersteller          | String   | "Volkswagen", "Toyota", ...                    |
| Modell              | String   | "Golf", "Camry", ...                           |
| Modelljahr          | Integer  | Ganze Zahl, z. B. 2022                         |
| Motorleistung       | Float    | Dezimalzahl, z. B. 150.5                       |
| Farbe               | String   | "Blau", "Silber", ...                          |
| KFZ-Kennzeichen    | String   | Alphanumerisch, z. B. "M-AB 1234"             |

**Tabelle "Versicherung":**

| Attribut                   | Datentyp | Wertebereich                                          |
|----------------------------|----------|-------------------------------------------------------|
| Versicherungsgesellschaft  | String   | "Allianz", "HDI", ...                                 |
| Versicherungssparte        | String   | "Kfz-Haftpflicht", "Lebensversicherung", ...         |
| Versicherungsnummer        | String   | Alphanumerisch oder Integer, je nach Vergabepraxis    |
| Versicherungssumme         | Float    | Euro, z. B. 100000.0                                  |

**Tabelle "Person":**

| Attribut        | Datentyp | Wertebereich                                      |
|-----------------|----------|---------------------------------------------------|
| Name            | String   | Nachname, z. B. "Müller"                          |
| Vorname         | String   | "Anna", ...                                       |
| Geburtsdatum    | Date     | Datum im Format "YYYY-MM-DD", z. B. 1990-05-15    |
| Anschrift       | String   | Adresse, z. B. "Musterstraße 123, 12345 Musterstadt" |

---

## Aufgabe 2

```
100
Versicherungsgesellschaft,Versicherungssparte,Versicherungsnummer,Versicherungssumme
Allianz,Kfz-Haftpflicht,123456789,100000.00

101
Name,Vorname,Geburtsdatum,Anschrift
Müller,Anna,1990-05-15,"Musterstraße 123, 12345 Musterstadt"

102
Hersteller,Modell,Modelljahr,Motorleistung,Farbe,KFZ-Kennzeichen
Volkswagen,Golf,2022,150.5,Blau,M-AB 1234
```

--- 

## Aufgabe 3

**ERM (Entity-Relationship Model):**

1. Entitäten (Entities):
    
    - Person
    - Auto
    - Versicherung
    - Versicherungsgesellschaft
2. Beziehungen (Relationships):
    
    - Besitzt: Verbindung zwischen Person und Auto (1:N)
    - Gehört zu: Verbindung zwischen Auto und Person (N:1)
    - Versichert: Verbindung zwischen Person und Versicherung (N:M)
    - Bietet an: Verbindung zwischen Versicherungsgesellschaft und Versicherung (1:N)
3. Attribute (Attributes):
    
    - Person: Name, Vorname, Geburtsdatum, Anschrift
    - Auto: Hersteller, Modell, Modelljahr, Motorleistung, Farbe, KFZ-Kennzeichen
    - Versicherung: Versicherungssparte, Versicherungsnummer, Versicherungssumme
    - Versicherungsgesellschaft: Name

**ERD (Entity-Relationship Diagram):**

```
   +-----------------------+       +--------------------------+
   |      Person           |       |    Auto                  |
   +-----------------------+       +--------------------------+
   | PK    Name            |       | PK   KFZ-Kennzeichen     |
   |      Vorname          |       |     Hersteller           |
   |      Geburtsdatum     |       |     Modell               |
   |      Anschrift        |       |     Modelljahr           |
   |                       |       |     Motorleistung        |
   +-----------------------+       |     Farbe                |
                                   | FK  Besitzer (Person)    |
                                   +--------------------------+
  
   +------------------------+      +-------------------------+
   |    Versicherung        |      | Versicherungsgesellschaft|
   +------------------------+      +-------------------------+
   | PK   Versicherungsnummer|      | PK   Name               |
   |     Versicherungssparte|      +-------------------------+
   |     Versicherungssumme |     
   +------------------------+  

```

--- 

## Aufgabe 4

**a) Modell in Tabellendarstellung:**

1. Person
    
    - **PK** (Primärschlüssel): PersonID
    - Name
    - Vorname
    - Geburtsdatum
    - Anschrift
2. Auto
    
    - **PK**: KFZ-Kennzeichen
    - Hersteller
    - Modell
    - Modelljahr
    - Motorleistung
    - Farbe
    - **FK** (Fremdschlüssel): BesitzerID (verweist auf PersonID in der Tabelle Person)
3. Versicherung
    
    - **PK**: Versicherungsnummer
    - Versicherungssparte
    - Versicherungssumme
    - **FK**: Versicherungsgeber (verweist auf VersicherungsgeberID in der Tabelle Versicherungsgesellschaft)
4. Versicherungsgesellschaft
    
    - **PK**: VersicherungsgeberID
    - Name

**b) In 3. Normalform:**

1. **Person:**
    
    - **PK**: PersonID
    - Name
    - Vorname
    - Geburtsdatum
    - Anschrift
    - **FK**: Versicherungsnummer
1. **Auto:**
    
    - **PK**: KFZ-Kennzeichen
    - Hersteller
    - Modell
    - Modelljahr
    - Motorleistung
    - Farbe
    - **FK**: BesitzerID
3. **Versicherung:**
    
    - **PK**: Versicherungsnummer
    - Versicherungssparte
    - Versicherungssumme
    - **FK**: VersicherungsgeberID
4. **Versicherungsgesellschaft:**
    
    - **PK**: VersicherungsgeberID
    - Name

**c) Tabellen mit Datensätzen:**

**Person:**

| PersonID | Name | Vorname | Geburtsdatum | Anschrift | Versicherungsnummer |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 1 | Müller | Anna | 1990-05-15 | Musterstraße 123, Musterstadt | 12345 |
| 2 | Schmidt | Peter | 1985-08-22 | Hauptweg 456, Beispielstadt | 67890 |

**Auto:**

|KFZ-Kennzeichen|Hersteller|Modell|Modelljahr|Motorleistung|Farbe|BesitzerID|
|---|---|---|---|---|---|---|
|M-AB 1234|Volkswagen|Golf|2022|150.5|Blau|1|
|K-KL 5678|Toyota|Camry|2021|180.0|Schwarz|2|

**Versicherung:**

|Versicherungsnummer|Versicherungssparte|Versicherungssumme|VersicherungsgeberID|
|---|---|---|---|
|12345|Kfz-Haftpflicht|100000.0|1|
|67890|Lebensversicherung|LV50000.0 |2|

**Versicherungsgesellschaft:**

|VersicherungsgeberID|Name|
|---|---|
|1|Allianz|
|2|HDI|

**d) ERM und ERD Vergleich:**

Das ERD und ERM repräsentieren die gleichen Informationen wie zuvor in Aufgabe 3 beschrieben. Der Hauptunterschied besteht darin, dass das ERD auf Tabellenebene detaillierter ist und die Fremdschlüssel-Beziehungen zwischen den Tabellen deutlicher zeigt. Das Modell in 3. Normalform stellt sicher, dass Redundanzen minimiert werden und die Daten effizient und konsistent gespeichert werden können.

---

## Aufgabe 5

**Tabelle "Buch":**

|ISBN|Titel|Autor|Erscheinungsjahr|
|---|---|---|---|
|978-3-12345-6|"Datenbanken kompakt"|Müller, Anna|2021|
|978-3-78901-2|"Programmieren lernen"|Schmidt, Peter|2020|

**Kennzeichnung:**

- **TITEL:** Spaltenüberschrift "Titel"
- **Zeile:** Eine Zeile in der Tabelle, z. B., die Zeile für "Datenbanken kompakt"
- **Spalte:** Eine Spalte in der Tabelle, z. B., die Spalte "Titel"
- **Tupel:** Eine Zeile in der Tabelle, z. B., die Zeile für "Datenbanken kompakt"
- **Attribut:** Eine Spalte in der Tabelle, z. B., die Spalte "Titel"
- **Datensatz:** Eine Zeile in der Tabelle, z. B., die Zeile für "Datenbanken kompakt"
- **Attributwert:** Der Wert in einer Zelle, z. B., der Titel "Datenbanken kompakt"
- **Datenfeld:** Ein einzelnes Feld in der Tabelle, z. B., das Feld für den Titel "Datenbanken kompakt"
- **Attributwert:** Der Wert in einer Zelle, z. B., der Titel "Datenbanken kompakt"

**Begriffe eher in der Relationalen Welt:**

- **TITEL:** Attribut in einer Tabelle, repräsentiert einen bestimmten Aspekt der gespeicherten Informationen.
- **Zeile:** Ein Tupel in einer Tabelle, repräsentiert einen vollständigen Datensatz.
- **Spalte:** Ein Attribut in einer Tabelle, repräsentiert eine bestimmte Eigenschaft der gespeicherten Daten.
- **Tupel:** Eine Zeile in einer Tabelle, repräsentiert einen vollständigen Datensatz.
- **Attribut:** Eine Spalte in einer Tabelle, repräsentiert eine bestimmte Eigenschaft der gespeicherten Daten.
- **Datensatz:** Ein Tupel in einer Tabelle, repräsentiert einen vollständigen Datensatz.

**Synonyme:**

- Die Begriffe **Tupel** und **Datensatz** werden oft synonym verwendet.
- Die Begriffe **Attribut** und **Datenfeld** können in einigen Kontexten synonym verwendet werden.

Die Begriffe, die eher in der relationalen Welt verwendet werden, sind eng miteinander verbunden und werden oft als Synonyme verwendet. Der Begriff **Datenfeld** wird manchmal als allgemeinere Bezeichnung für ein Element in einer Datenbank verwendet.