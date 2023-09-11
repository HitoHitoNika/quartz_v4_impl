---
tags:
  - Berufsschule
  - LF9
Created: 07-09-2023, 09:11
---
## Was ist DNS?

Das Domain Name System ordnet lesbare/merkbare Name bzw. Adressen (google.com) zu IPs zu.
DNS ist ein weltweites, hierarchisches System mit Delegation.

Beispiel: moodle.bildung.koblenz.de.
. : Root-Zone
de: TopLevelDomain (TLD)
Koblenz: SecondLevelDomain
Bildung: Subdomain
Moodle: Hostname

## Resource Records

DNS hat mehrere Resource Records (DNS-RR), welche dazu dienen bei Abfragen an den DNS anzugeben, was man genau möchte. 

Type A ("Address")= IPv4-Adressen
Type AAAA = IPv6-Adressen
Type MX (Mail Exchange) = Mailserver
Type NS (Nameserver) = DNS-Server
Type SOA (Start of Authority) = Zuständigkeit
Type TXT = Kommentare etc.
Type TLSA ("TLS Authority") = Zertifikatsvalidierung

Diese kann man in der CMD anwenden, indem man zunächst "nslookup" öffnet.
Dann kann man set type=_Hier den gewünschten Typen_ eingeben, wonach man die gewünschte Domain eingeben kann und das Ergebnis erhält.

### Beispiele

IPv4 von Moodle: 
>82.115.104.42

IPv6 von Google: 
>2a00: 1450: 4001: 81c:: 200e

Mailserver von gibip.de: 
> MX preference = 10, mail exchanger = mx.mpma.de

Kommentar von gibip.de
>"v=spf1 mx ip4:94.130.176.143 ip6:2a01:4f8:c0c:a39a::1 -all"
gibip.de        text ="Hallo BSIT22c!"


### Root-Zone

Die Root-Zone wird von 13 Root-Nameservern bedient a.root-servers.net bis m.root-servers.net

```bash
nslookup
set type=NS
.
```

Zur Vermeidung von Ausfällen sind diese 13 Adressen sogenannte "Anycast-Adressen". Es gibt in Wahrheit also deutlich mehr als 13 Root-Server.


### Reverse DNS

Für den Reverse lookup gibt es ein eigenen Resource Record "PTR-Record".

Beispiel:   10.7.4.2 hat einen PTR-Eintrag in der Domain 2.4.7.10.in-addr.arpa. 

```
nslookup
set type=PTR
2.4.7.10.in-addr.arpa.
```

Bei IPv6 ist die Reverse-Zone ip6.arpa.