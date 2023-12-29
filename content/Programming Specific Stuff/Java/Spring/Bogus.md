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

## Aufgabe 3

**ERM (Entity-Relationship Model):**

![[ERM.png]]

1. Entitäten:
    - Person
    - Auto
    - Versicherung
    - Versicherungsgesellschaft
2. Beziehungen:
    - Besitzt: Verbindung zwischen Person und Auto (1:N)
    - Gehört zu: Verbindung zwischen Auto und Person (N:1)
    - Versichert: Verbindung zwischen Person und Versicherung (N:M)
    - Bietet an: Verbindung zwischen Versicherungsgesellschaft und Versicherung (1:N)
3. Attribute:
    - Person: Name, Vorname, Geburtsdatum, Anschrift
    - Auto: Hersteller, Modell, Modelljahr, Motorleistung, Farbe, KFZ-Kennzeichen
    - Versicherung: Versicherungssparte, Versicherungsnummer, Versicherungssumme
    - Versicherungsgesellschaft: Name 

## Aufgabe 4

**a) Modell in Tabellendarstellung:**

1. **Tabelle "Person":**

| Attribut        | Datentyp | Wertebereich                                      |
|-----------------|----------|---------------------------------------------------|
| PersonID (PK)   | Integer  | Eindeutige ID für jede Person                     |
| Name            | String   | Nachname                                          |
| Vorname         | String   | Vorname                                           |
| Geburtsdatum    | Date     | Datum im Format "YYYY-MM-DD"                      |
| Anschrift       | String   | Adresse                                           |

2. **Tabelle "Auto":**

| Attribut | Datentyp | Wertebereich |
| ---- | ---- | ---- |
| KFZ-Kennzeichen (PK) | String | Alphanumerisch, eindeutiges Kennzeichen |
| Hersteller | String | Alphanumerisch, z. B. "Volkswagen" |
| Modell | String | Alphanumerisch, z. B. "Golf" |
| Modelljahr | Integer | Ganze Zahl, 1885-9999 |
| Motorleistung | Integer | Ganze Zahl 0-1999 |
| Farbe | String | "Blau", "Rot", ... |


3. **Tabelle "Versicherung":**

| Attribut | Datentyp | Wertebereich |
| ---- | ---- | ---- |
| Versicherungsnummer (PK) | String | Alphanumerisch, eindeutige Versicherungsnummer |
| Versicherungssparte | String | Art der Versicherung, z. B. "Kfz-Haftpflicht" |
| Versicherungssumme | Float | Euro, z. B. 100000.0 |


4. **Tabelle "Versicherungsgesellschaft":**

| Attribut               | Datentyp | Wertebereich                                          |
|------------------------|----------|-------------------------------------------------------|
| VersicherungsgeberID (PK)| Integer  | Eindeutige ID für jede Versicherungsgesellschaft      |
| Name                   | String   | Name der Versicherungsgesellschaft, z. B. "Allianz"    |

**b) In 3. Normalform:**

1. **Person**

|Attribut|Datentyp|Wertebereich|
|---|---|---|
|PersonID (PK)|Integer|Eindeutige ID für jede Person|
|Name|String|Nachname|
|Vorname|String|Vorname|
|Geburtsdatum|Date|Datum im Format "YYYY-MM-DD"|
|Anschrift|String|Adresse|
|Versicherungsnummer (FK)|String|Fremdschlüssel, verweist auf Versicherungsnummer in Tabelle "Versicherung"|
2. **Auto:**

| Attribut | Datentyp | Wertebereich |
| ---- | ---- | ---- |
| KFZ-Kennzeichen (PK) | String | Alphanumerisch, eindeutiges Kennzeichen |
| Hersteller | String | Alphanumerisch, z. B. "Volkswagen" |
| Modell | String | Alphanumerisch, z. B. "Golf" |
| Modelljahr | Integer | Ganze Zahl, 1885-9999 |
| Motorleistung | Integer | Ganze Zahl 0-1999 |
| Farbe | String | "Blau", "Rot", ... |
| BesitzerID (FK) | Integer | Fremdschlüssel, verweist auf PersonID in Tabelle "Person" |

3. **Versicherung:**

|Attribut|Datentyp|Wertebereich|
|---|---|---|
|Versicherungsnummer (PK)|String|Alphanumerisch, eindeutige Versicherungsnummer|
|Versicherungssparte|String|Art der Versicherung, z. B. "Kfz-Haftpflicht"|
|Versicherungssumme|Float|Euro, z. B. 100000.0|
|VersicherungsgeberID (FK)|Integer|Fremdschlüssel, verweist auf VersicherungsgeberID in Tabelle"Versicherungsgesellschaft"|


4. **Versicherungsgesellschaft:**

|Attribut|Datentyp|Wertebereich|
|---|---|---|
|VersicherungsgeberID (PK)|Integer|Eindeutige ID für jede Versicherungsgesellschaft|
|Name|String|Name der Versicherungsgesellschaft, z. B. "Allianz"|

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
|LV67890 |Lebensversicherung|50000.0 |2|

**Versicherungsgesellschaft:**

|VersicherungsgeberID|Name|
|---|---|
|1|Allianz|
|2|Debeka |

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
- **Zeile:** Ein Zeile in einer Tabelle, repräsentiert einen vollständigen Datensatz.
- **Spalte:** Ein Attribut in einer Tabelle, repräsentiert eine bestimmte Eigenschaft der gespeicherten Daten.
- **Tupel:** Eine Tupel in einer Tabelle, repräsentiert einen vollständigen Datensatz.
- **Attribut:** Eine Spalte in einer Tabelle, repräsentiert eine bestimmte Eigenschaft der gespeicherten Daten.
- **Datensatz:** Ein Tupel in einer Tabelle, repräsentiert einen vollständigen Datensatz.

**Synonyme:**

- Die Begriffe **Tupel** und **Datensatz** werden oft synonym verwendet.
