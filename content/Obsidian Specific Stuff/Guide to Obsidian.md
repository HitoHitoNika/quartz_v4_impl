---
tags:
  - Guide
Created: 29-08-2023, 20:44
---
# Funktionen
## Shortcuts
Strg+N öffnet eine neue Untiteld Note, während Strg+Shift+N eine neue Note in einem extra Tab öffnet.
## Verlinkungen zu anderen Notizen
Eines der wichtigsten Tools in Obsidian ist es auf andere Notizen zu verweisen.
Beispielsweise kann ich wenn ich einen [[01. Angular Installation Guide]] schreibe auf eine Notiz  verlinken in dem ich den Titel mit doppelten Eckigen Klammern umrunde. Dann werden diese unterstrichen und highlightet. Mit Strg+Linke Maustaste (Schreibeview) oder nur linke Maustaste(Leseview) kann man direkt zu dieser Notiz kommen. 
## Möglichkeit Ordner zu erstellen
Ordner bieten eine Möglichkeit die Notes strukturiert zu hinterlegen. Hierfür kann man sich beispielsweise Oberthemen suchen.
## Views
Es gibt eine Lese- und Schreibview zwischen welchen man mit Strg+E wechseln kann.
Tipp: Man kann zweimal die selbe Datei aufhaben, eine in Lese- und die andere in Schreibview haben und diese dann linken, indem man rechts klick auf den Tab macht "Link with tab"
## Tags
Tags sind genaue wie Hashtags. Sie bieten Filtermöglichkeiten mit welchen man seine Notizen weiter strukturieren kann. 
## Bilder/Gifs
Bilder/Gifs können per Drag + drop hinzugefügt werden 	:
![[Example Gif - Gear 5.gif]]


# Style
## Überschriften
Wie in Markdown üblich kann man mit der # eine Überschrift erzeugen. ACHTUNG: Im Gegensatz zu den Hashtags muss nach der Raute in den Überschriften ein Leerzeichen gesetzt werden !

## Formatierungsmöglichkeiten
Wie in jedem Texteditor gibt es die Möglichkeiten **Fett** , *kursiv* oder ==markiert==  zu schreiben.
Dafür einfach Strg+B oder ** (Fett), Strg + I oder * (kursiv) und == (markiert) entsprechend verwenden.

## Zitate und Abtrennungen
> Um solchen coolen Zitate zuschreiben, beginnt man einen neuen Absatz mit > 

--- 
Für solche Abtrennungen schreibt man in eine sonst leere Zeile --- und schreibt in der nächsten weiter 

## Listen
Es gibt diverse Listen die man schreiben kann.
- Bulletpoints schreibt man mit einem - am Anfang einer Zeile
1. und eine nummerierte Liste schreibt man mit der entsprechenden Zahl + . am Anfang der Zeile
# Templates
Templates bieten die Möglichkeit ein einheitliches Design zu erschaffen. 
## Templates erstellen 
### Hinterlegen der Templates
Zunächst müssen wir einen Ordner für unsere Custom Templates erstellen.
Nachdem wir dies getan haben, müssen wir diesen hinterlegen.
Dafür gehen wir in die Einstellungen:
- Core Plugins
	- Templates
Hier können wir einen Beispielordner hinterlegen, Datum- und Zeitformat einstellen.
### Einrichten der Template
Jetzt können wir in unserem Ordner eine Note erstellen und dann bestimmte Syntax verwenden um die gewünschte Struktur zu haben. Beispielsweise können wir {{title}} verwenden um den Titel der Note , welche auf dieser Template basiert, zureferenzieren. Ähnlich gibt es {{date}} und {{time}}.

## Templates verwenden

Nachdem wir unsere Templates erstellt haben, können wir eine neue Note erstellen. Dann klicken wir in der linken Menüleiste auf "Insert Template" und können nun eine unserer Templates verwenden.

# Graph View

Die Graph View ist ein sehr uniques und cooles Feature. Hier werden alle Dokumente die untereinander verlinken visuell dargestellt. Dazu geht man in der linken Menüleiste auf Graph View, fertig.
Um diese effektiv zu nutzen muss man jedoch die oben beschriebenen Verlinkungen verwenden.

