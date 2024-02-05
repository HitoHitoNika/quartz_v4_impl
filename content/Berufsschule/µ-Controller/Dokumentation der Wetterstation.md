## Einleitung

In dem Projekt "Wetterstation" war das Ziel, Umweltparameter wie Temperatur, Luftfeuchtigkeit und Helligkeit zu messen und auf einem Display anzuzeigen. Wir sollten den DHT11-Sensor für Luftfeuchtigkeit und Temperatur sowie den LDR-Sensor für die Helligkeit verwenden. 

In der folgenden Dokumentation werde ich auf die Funktionen und die nötigen Schritte meines Projektes eingehen.

## Inhalt

- [[#Verwendete Bibliotheken]]
- [[#Grundlegende Funktionalitäten]]
- [[#Erweiterte Funktionalitäten]]
	- [[#Uhrzeit per Network Time Protocol (NTP)|Uhrzeit per Network Time Protocol (NTP)]]
	- [[#Webserver|Webserver]]
	- [[#Datenbankanbindung|Datenbankanbindung]]
- [[#Programmablauf|Programmablauf]]
	- [[#Globale Variablen|Globale Variablen]]
	- [[#Setup|Setup]]
	- [[#Loop|Loop]]

## Verwendete Bibliotheken

Neben den bereitgestellten Bibliotheken für bspw. den DHT11 oder des Displays habe ich weitere Bibliotheken verwenden um weitere Funktionen zu implementieren.

### ESP8266WiFi-Bibliothek
Für die WLAN-Konnektivität des ESP8266 habe ich die ESP8266WiFi-Bibliothek genutzt. Sie ermöglicht die einfache Verbindung mit einem WLAN-Netzwerk, welche für einige Funktionen wichtig war.

```cpp
#include <ESP8266WiFi.h>
```

### HTTPClient- und ESP8266WebServer-Bibliothek
Diese Bibliotheken wurden für die Kommunikation über HTTP und die Implementierung eines einfachen Webservers verwendet.
```cpp
#include <ESP8266HTTPClient.h>
#include <ESP8266WebServer.h>
```

### time.h
Diese Bibliothek ermöglicht die Arbeit mit Zeiten und wurde für die Konfiguration des Network Time Protocol (NTP) Servers verwendet
```cpp
#include <time.h>
```

## Grundlegende Funktionalitäten

Wie in den Anforderungen beschrieben kann die Wetterstation sowohl die Temperatur und Luftfeuchtigkeit als auch die Helligkeit messen. 
Diese werden auf dem Display dargestellt, mit:
- Aktuellen Wert
- Tagesdurchschnitt
- Uhrzeit
Außerdem wird anhand des aktuellen Werts ein Bild angezeigt. Die Wertebereiche hierfür sind:
- Temperatur 
	- kleiner 4°C zeigt einen Eiskristall
	- 4°C - 20°C zeigt eine Sonne
	- größer als 20°C zeigt einen Wasserkocher
- Luftfeuchtigkeit
	- kleiner 40% zeigt einen Kaktus
	- 40% - 80% zeigt einen Wassertropfen
	- größer 80% zeigt mehrere Wassertropfen
- Lichtlevel
	- kleiner 100 Lux zeigt einen Mond
	- 100 Lux  - 150 Lux zeigt eine Glühbirne
	- größer 150 Lux zeigt eine Sonne

Den detaillierten Code zeige ich bei Erklärung des [[#Loop|Loops]].
## Erweiterte Funktionalitäten

Abgesehen von den grundlegenden Funktionalitäten hat meine Wetterstation noch 3 weitere Funktionen welche den Umgang mit ihr stark vereinfachen. Ich werde diese hier grundlegend erklären, für detaillierte Codesnippets verweise ich auf [[#Programmablauf]].

>[!info] WLAN
>Für die 3 nachfolgenden Funktionen wird WLAN benötigt da diese sonst nicht verfügbar sind. Im Code müssen hierzu die richtige SSID und das Passwort gesetzt werden. Mehr dazu unter: [[#Setup]]

### Uhrzeit per Network Time Protocol (NTP)

Wie zuvor erwähnt wird die Uhrzeit auf meinem Display angezeigt. Diese wird über das Internet per NTP abgerufen. Dazu musste dieser zunächst hinterlegt werden mit unserer Zeitzone.
```cpp
configTime(3600,0,"pool.ntp.org");
```

Bei pool.ntp.org handelt es sich um einen Pool mehrerer NTP Server die man abfragen kann. Diese stehen kostenlos zur Verfügung.
### Webserver

Der Webserver bietet Clients die im selben Netz sind einen schnellen Zugriff zu den Daten der Wetterstation ohne diese über das Display auslesen zu müssen.
Die Webseite bietet Einblick über alle aktuellen Werte und Tagesdurchschnitte und ist erreichbar unter der IP des Geräts auf Port 80.

### Datenbankanbindung

Die Wetterstation schickt zyklisch ihre Daten an einen von mir geschriebenen Datenbank Endpunkt, welcher diese persistent speichert.
Die Daten werden alle 120 Bildschirmrotationen in einen JSON String verpackt und mit dem HTTPClient an meinen Server geschickt. 

>[!info] Bildschirmrotation
Eine Bildschirmrotation ist der Wechsel zwischen zwei Ansichten des Bildschirms. Also bspw. der Wechsel von der Temperaturansicht zur Luftfeuchtigkeitsansicht. 

## Programmablauf

Die wichtigsten Bestandteile meines Codes sind das erste Setup, der Loop und natürlich einige globale Variablen.

### Globale Variablen
Ich habe mehrere globale Variablen verwendet um den Zugriff zu erleichtern. Viele Dinge sind hier nicht spektakulär (bspw. die Ports für die Sensoren) daher werde ich nicht weiter auf diese eingehen.

#### Datenbankeinstellungen
Mehrere Werte die für den JSON Post gebraucht werden, sind hier eingepflegt.
```cpp
#define LOCATION_ID 1
#define DEVICE_ID 1
#define SERVER_URL "http://192.168.1.112:8080/api/weather/createEntry"
``` 
Die Location beschreibt den Raum in welcher die Station liegt, während die Device ID das genaue Gerät benennen soll.  Die Server URL gibt einfach die Adresse des Endpunktes an.

#### Screen State  
Hier habe ich Werte hinterlegt welche den Ansichten zu geordnet sind.
```cpp
int currentScreen = 0; 
#define SCREEN_TEMP 0
#define SCREEN_HUMIDITY 1
#define SCREEN_LIGHTLEVEL 2
```
### Setup
Viele erste Schritte im Setup habe ich in Hilfsmethoden ausgelagert um das Setup etwas lesbarer zu machen.
```cpp
void setup(){
  initSensor();
  initOLED();
  configTime(3600,0,"pool.ntp.org");
  Serial.begin(115200);
  connectToWiFi();
  if(WiFi.status()==WL_CONNECTED){
    configureServer();
  }
}
```

Hier wird:
- Der DHT11 und das Display eingerichtet
- Der NTP-Server hinterlegt
- Die Serielle Übertragung gestartet
- Eine Verbindung zu dem hinterlegenten WLAN gestartet
- Wenn das WLAN verfügbar wird zusätzlich der Webserver gestartet

#### connectToWiFi

Die Funktion connectToWiFi probiert 10x eine Verbindung herzustellen.
Wenn es ihr gelingt diese herzustellen dann wird eine Erfolgsnachricht auf dem Display angezeigt gefolgt von der IP-Adresse. 
Wenn es ihr nicht gelingen sollte kommt eine Fehlermeldung auf das Display.

```cpp
int tries = 0;
  updateDisplay("Starte Wifi....");
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED && tries != 10) {
    updateDisplay("Verbindung wird hergestellt... "+(String)tries+"/10");
    delay(1000);
    tries++;
  }
  if(tries!=10){
    updateDisplay("Verbunden mit "+(String)ssid);
    delay(500);
    updateDisplay("Die IP ist: " +WiFi.localIP().toString());
    delay(500);
  }else{
    updateDisplay("Verbindung fehlgeschlagen");
  }
  delay(500);
```

#### configureServer

Hier wird der Webserver eingerichtet, genauer werden 2 Routen hinterlegt.
- / verweist auf die Funktion handleRoot
	- Hier wird die grundlegende Weboberfläche angezeigt
- /data verweist auf die Funktion handleData
	- Diese dient der Datenbeschaffung

```cpp
void configureServer(){
  server.on("/",HTTP_GET,handleRoot);
  server.on("/data", HTTP_GET, handleData);
  server.begin();
}
```

Zu handleRoot und handleData gibt es mehr unter: [[#server.handleClient]].

### Loop
Der Loop stellt den Hauptablauf dar. Hier wird:
- Aufruf des Webservers verwaltet
- Werte gemessen
- Das Display entsprechend aktualisiert
- Post an die Datenbank geschickt

```cpp
void loop() {
  server.handleClient();
  unsigned long currentTime = millis();
  if (currentTime - lastUpdateTime >= INTERVAL) {
    lastUpdateTime = currentTime;
    measureValues();
    updateDisplay();
    loopCounter++;
    if (loopCounter == LOOP_LIMIT) {
      loopCounter = 0;
      sendPost();
    }
  }
}
```

Statt einem delay tracke ich hier die letzte Update Zeit und die aktuelle Zeit. Bei einem delay würde das ganze Programm pausieren, bei diesem Ansatz ist es aber noch möglich das der Server Client anfragen bearbeiten kann.
#### server.handleClient

Die Methode handleClient() sorgt dafür das User Anfragen an den Webserver aktzeptiert und entsprechend gemanaged werden. Bedeutet das die Methoden die zuvor bei [[#configureServer]] hinterlegt wurden ausgeführt werden.

##### handleRoot

handleRoot liefert eine simple Webseite zurück die die aktuellen Sensorwerte + den Durchschnittanzeigt. Diese ruft alle 2 Sekunden den Endpunkt /get auf um die Daten zuerhalten. 

```cpp
void handleRoot() {
  String html = "<!DOCTYPE html><html lang=\"en\"><head>";
  html += "<meta charset=\"UTF-8\"><meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">";
  html += "<title>Wetterstation</title><script>";
  html += "function updateValues() {var xhttp = new XMLHttpRequest();";
  html += "xhttp.onreadystatechange = function() {if (this.readyState == 4 && this.status == 200) {";
  html += "var data = JSON.parse(this.responseText);document.getElementById(\"temperature\").innerHTML = \"Temperatur: \" + data.current.temperature + \" &deg;C\";";
  html += "document.getElementById(\"humidity\").innerHTML = \"Luftfeuchtigkeit: \" + data.current.humidity + \" %\";";
  html += "document.getElementById(\"lightlevel\").innerHTML = \"Lichtstärke: \" + data.current.lightlevel + \" Lux\";";
  html += "document.getElementById(\"average-temperature\").innerHTML = \"Durchschnittstemperatur: \" + data.average.temperature + \" &deg;C\";";
  html += "document.getElementById(\"average-humidity\").innerHTML = \"Durchschnittsluftfeuchtigkeit: \" + data.average.humidity + \" %\";";
  html += "document.getElementById(\"average-lightlevel\").innerHTML = \"Durchschnittliche Lichtstärke: \" + data.average.lightlevel + \" Lux\";}};";
  html += "xhttp.open(\"GET\", \"/data\", true);xhttp.send();}setInterval(updateValues, 2000);</script></head>";
  html += "<body><h1>Wetterstation</h1>";
  html += "<p id=\"temperature\">Temperatur: -- &deg;C</p>";
  html += "<p id=\"humidity\">Luftfeuchtigkeit: -- %</p>";
  html += "<p id=\"lightlevel\">Lichtstärke: -- Lux</p>";
  html += "<h2>Durchschnittswerte</h2>";
  html += "<p id=\"average-temperature\">Durchschnittstemperatur: -- &deg;C</p>";
  html += "<p id=\"average-humidity\">Durchschnittsluftfeuchtigkeit: -- %</p>";
  html += "<p id=\"average-lightlevel\">Durchschnittliche Lichtstärke: -- Lux</p></body></html>";
  server.send(200, "text/html", html);
}
```
##### handleData
handleData wird unter /data aufgerufen und liefert die aktuellen Sensorwerte als JSON.
```cpp
void handleData() {
  String json = "{";
  json += "\"current\": {";
  json += "\"temperature\":" + String(currentTemp) + ",";
  json += "\"humidity\":" + String(currentHumid) + ",";
  json += "\"lightlevel\":" + String(currentLightlevel);
  json += "},";
  json += "\"average\": {";
  json += "\"temperature\":" + String(sumTemp/messungen) + ",";
  json += "\"humidity\":" + String(sumHumid/messungen) + ",";
  json += "\"lightlevel\":" + String(sumLightlevel/messungen);
  json += "}";
  json += "}";
  server.send(200, "application/json", json);
}
```

#### measureValues

measureValues liest die aktuellen Werte aus, bestimmt die aktuelle Uhrzeit und berechnet den neuen Durchschnitt.

```cpp
void measureValues(){
  if(getLocalTime(&timeinfo)){
    //Abrufen und speichern der aktuellen Uhrzeit
    strftime(date,sizeof(date),"%Y-%m-%dT%H:%M:%S",&timeinfo);  
  }
  currentTemp= dht.readTemperature();
  currentHumid= dht.readHumidity();
  currentLightlevel=analogRead(LDR);
  sumTemp+=currentTemp;
  sumHumid+=currentHumid;
  sumLightlevel+=currentLightlevel;
  messungen++;
}
```

#### updateDisplay

updateDisplay bestimmt den aktuellen Bildschirm und ruft den entsprechend nächsten Bildschirm auf. Die 3 Bildschirme für Temperatur, Luftfeuchtigkeit und Lichtlevel haben alle ihre eigene Funktion, welche diese anzeigen lässt:
- displayTemp
- displayHumidity
- displayLightlevel

```cpp
void updateDisplay(){
  //Switch der Anhand des aktuellen Bildschirms den nächsten auswählt
  switch(currentScreen){
    case SCREEN_TEMP:
    displayTemp();
    currentScreen++;
    break;
    case SCREEN_HUMIDITY:
    displayHumidity();
    currentScreen++;
    break;
    case SCREEN_LIGHTLEVEL:
    displayLightlevel();
    currentScreen=0;
    break;
    default:
    displayTemp();
    currentScreen=1;
    break;
  }
}
```

##### updateDisplay(String message)
Eine ähnliche Methode wie updateDisplay(). Hier wird jedoch eine Nachricht mitgegeben welche auf dem Display angezeigt wird.

```cpp
void updateDisplay(String message){
  resetDisplay();
  display.println(message);
  display.display();
}
```

