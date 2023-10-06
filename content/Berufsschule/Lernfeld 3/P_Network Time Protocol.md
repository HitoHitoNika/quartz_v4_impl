---
tags:
  - Berufsschule
  - LF3
aliases:
  - NTP
  - NetworkTimeProtocol
  - Network Time Protocol
title: Network Time Protocol
---
Zurück zu [[Berufsschulstoff|Berufsschul-Inhaltsüberischt]]

- [[#Was ist NTP?|Was ist NTP?]]
- [[#Funktionsweise|Funktionsweise]]
- [[#Relevanz|Relevanz]]

## Was ist NTP?

Das Network Time Protocol (NTP) dient der Synchronisation der Uhrzeit zwischen mehreren Systemen.

## Funktionsweise

1. **Zeitquellen**: In einem NTP-Netzwerk gibt es Zeitquellen, die hochpräzise Uhren sind. Diese Zeitquellen sind oft Server, die von vertrauenswürdigen Organisationen oder Atomuhren betrieben werden. Sie dienen als Referenzpunkt für die genaue Zeit.
    
2. **Client-Geräte**: Auf den meisten Computern und Netzwerkgeräten, die NTP verwenden, befinden sich sogenannte NTP-Clients. Diese Geräte fragen regelmäßig die Zeit bei den Zeitquellen ab.
    
3. **Zeitsynchronisierung**: Wenn ein NTP-Client die Zeit von einer Zeitquelle anfordert, vergleicht er sie mit seiner eigenen Uhrzeit. Dann berechnet er den Zeitunterschied (die Abweichung) und den Offset (wie viel die Uhr abweicht).
    
4. **Korrektur**: Basierend auf diesen Informationen passt der NTP-Client seine eigene Uhrzeit an, um sie mit der genauen Zeitquelle zu synchronisieren. Dadurch wird die Uhrzeit des Geräts genau und zuverlässig gehalten.
    
5. **Hierarchie**: NTP arbeitet normalerweise in einer Hierarchie. Einige Geräte sind näher an den Hauptzeitquellen und dienen als "Stratum-1"-Server. Andere Geräte synchronisieren sich mit diesen Servern und werden als "Stratum-2"- oder höhere Server bezeichnet.

## Relevanz

NTP ist entscheidend in Computernetzwerken aus verschiedenen Gründen:

- **Synchronisation**: Es stellt sicher, dass alle Geräte im Netzwerk dieselbe Zeit haben, was für koordinierte Aktionen und Protokolle wie Datumsstempel in E-Mails und Protokolldateien entscheidend ist.
    
- **Sicherheit**: NTP hilft auch bei Sicherheitsmaßnahmen, da genaue Zeitstempel bei der Erkennung von Angriffen und beim Protokollieren von Sicherheitsereignissen helfen.
    
- **Datenaufzeichnung**: In vielen Anwendungen ist eine genaue Zeiterfassung wichtig, um sicherzustellen, dass Daten und Transaktionen korrekt protokolliert werden.



