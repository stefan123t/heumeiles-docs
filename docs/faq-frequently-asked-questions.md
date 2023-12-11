# FAQ Häufig gestellte Fragen


* Die Wechselrichter senden nur bei Tag, wenn auch eine Stromproduktion durch die PV Module stattfindet (DC Spannung >16V an einem MPPT-Eingang). 

* Es ist ratsam, einen Elko größer 10µF an die Stromversorgung des nRF24L01+ Moduls zu löten.
 
* Beim Wemos D1 mini ESP8266 Modul sollte bei Problemen der IRQ Pin statt an D3 an D1 / D2 angelötet werden und dies auch in der System Config eingetragen werden.

* Bei Problemen am besten ein fertiges .bin aus den GitHub Actions verwenden.

* Die Sendeleistung nicht gleich auf HIGH oder gar MAX stellen. LOW oder MIN ist in den meisten Fällen die bessere Wahl, da es einen geringeren Einbruch der Versorgungspannung beim Senden bewirkt. 

* Binaries für AhoyDTU gibt es unter: https://github.com/lumapu/ahoy/actions/workflows/compile_esp8266.yml 
oder https://github.com/lumapu/ahoy/actions/workflows/compile_development.yml 

* Man muss für die o.g. Binaries bei GitHub eingeloggt sein. Die Anmeldung ist kostenlos.

* Das erste Flashen kann z.B. mit dem esp flasher erfolgen: https://www.espressif.com/sites/default/files/tools/flash_download_tool_3.9.3.zip

* Danach kann für Updates die .bin Datei einfach per OTA hochgeladen werden.

* Falls bei Jemandem der ESP nach dem Flashen nicht mehr startet, im Support melden.
  Es scheint bei neueren Versionen des esp flasher Tools bei manchen Leuten probleme zu geben (konnte ich bei mir nicht feststellen).

* Der Haken bei DoNotChgBin muss weg gemacht werden falls er da ist.

* Wenn gar Nichts geht, ein Erase Flash durchführen und von vorne beginnen.

* AhoyDTU und OpenDTU brauchen eine korrekte NTP Zeit um den Wechselrichter abzufragen.

* Man sollte also als erstes sein WLAN eintragen und zum Internet connecten.

* Man sollte auch etwas bei der max. Panel Power eintragen damit die Irradiation % richtig berechnet werden können.
 
* Not available heißt der Wechselrichter antwortet seit min. 5 Minuten nicht auf die üblichen Anfragen durch die AhoyDTU / OpenDTU.

* Not producing heißt der Wechselrichter hat keine aktuellen Werte zur Leistung übermittelt (d.h. die AC-Leistung <3W).

* Die Autodiscover Funktion in HomeAssistant wird nur getriggert, wenn auch MQTT Nachrichten gesendet werden, also der Wechselrichter auch Daten sendet.

*behoben / veraltet*

~~* Beim ESP32 Wroom32 (38pol.) ist die empfohlene GPIO-Belegung diese hier und im Setup unter Sytem Config, Pinout (Wemos) folgendermaßen einzutragen:~~
  * ~~CS=D1 (GPIO5)~~
  * ~~CE=D2 (GPIO4)~~
  * ~~IRQ=D0 (GPIO16 - no IRQ!)~~

~~* Die Warnmeldung "no IRQ" zu GPIO16 gilt nur für den kleinen Bruder ESP8266 (Wemos) und funktioniert beim ESP32 einwandfrei.~~

~~* Es kann bis zu 30 Minuten dauern, bis der Wechselrichter die erste Antwort auf Anfragen zurücksendet, also nicht gleich nach zwei / drei Minuten Sendeversuchen aufgeben.~~


**OpenDTU**

* Binaries für OpenDTU kann man hier laden: https://github.com/tbnobody/OpenDTU/actions/workflows/build.yml

* Bei OpenDTU: 
  * die opendtu-generic.bin,
  * die bootloader_dio_40m.bin kommt nach 0x1000,
  * die partitions.bin nach 0x8000,
  * die boot_app0.bin nach 0xe000 
  * und das eigentliche Programm dann nach 0x10000.
  Beim Update wird nur noch das eigentliche Programm geflasht. 

<!--
# FAQ  

## Inhaltsverzeichnis

- [FAQ Häufig gestellte Fragen](#faq-häufig-gestellte-fragen)
- [FAQ Frequently Asked Questions](#faq-frequently-asked-questions)
  - [Inhaltsverzeichnis](#inhaltsverzeichnis)
  - [Allgemeines](#allgemeines)
    - [Welche Modelle werden unterstützt](#welche-modelle-werden-unterstützt)
    - [Welche Geräte / Funktionen werden nicht unterstützt](#welche-geräte--funktionen-werden-nicht-unterstützt)
    - [Welche Kommandos werden von der DTU unterstützt](#welche-kommandos-werden-von-der-dtu-unterstützt)
    - [Welche Entfernung unterstützen die nRF24L01+ Funkmodule](#welche-entfernung-unterstützen-die-nrf24l01-funkmodule)
    - [Modbus via TCP oder RS485](#modbus-via-tcp-oder-rs485)
    - [Was sind SunSpec und Victron](#was-sind-sunspec-und-victron)
    - [Was ist DRM](#was-ist-drm)
    - [Was ist AntiReflux](#was-ist-antireflux)
    - [Welche Modbus Register unterstützt die DTU-Pro](#welche-modbus-register-unterstützt-die-dtu-pro)
    - [Was ist MQTT](#was-ist-mqtt)
    - [Welche MQTT Broker / Home Automation Systeme verwendet ihr](#welche-mqtt-broker--home-automation-systeme-verwendet-ihr)
  - [Hardware](#hardware)
    - [Welche Hardware brauche ich für die verschiedenen Software Projekte](#welche-hardware-brauche-ich-für-die-verschiedenen-software-projekte)
    - [Welche Hardware gibt es und welche Software läuft darauf](#welche-hardware-gibt-es-und-welche-software-läuft-darauf)
    - [Welches nRF24L01+ Modul verwendet ihr ?](#welches-nrf24l01-modul-verwendet-ihr-)
    - [Welchen Mikroprozessor empfehlt ihr ?](#welchen-mikroprozessor-empfehlt-ihr-)
    - [Wie ist das Gerät mit Spannung zu versorgen](#wie-ist-das-gerät-mit-spannung-zu-versorgen)
  - [Software / Installation](#software--installation)
    - [Welche Software gibt es und mit welcher Hardware läuft sie](#welche-software-gibt-es-und-mit-welcher-hardware-läuft-sie)
    - [BIN Files für Ahoy-DTU](#bin-files-für-ahoy-dtu)
    - [Platform IO installieren](#platform-io-installieren)
    - [Wie definiere ich die Serielle Schnittstelle für den ESP7266/ESP32](#wie-definiere-ich-die-serielle-schnittstelle-für-den-esp7266esp32)
    - [Wie kann ich den ESP8266 konfigurieren](#wie-kann-ich-den-esp8266-konfigurieren)
    - [Wo finde ich den original Source Code von Hoymiles](#wo-finde-ich-den-original-source-code-von-hoymiles)
    - [Welche **EXPERIMENTELLEN** Software Funktionen sind bisher noch nicht im Standard enthalten (Pull Request / Merge)](#welche-experimentellen-software-funktionen-sind-bisher-noch-nicht-im-standard-enthalten-pull-request--merge)
    - [Welche Software Funktionen sind geplant](#welche-software-funktionen-sind-geplant)
  - [Konfiguration](#konfiguration)
    - [Eintragen der Seriennummer](#eintragen-der-seriennummer)
    - [S/N eintragen, muss das "ULL" stehen bleiben (im Source) ?](#sn-eintragen-muss-das-ull-stehen-bleiben-im-source-)
    - [Wieviele Wechselrichter unterstützt die Software](#wieviele-wechselrichter-unterstützt-die-software)
    - [Warum antwortet der Wechselrichter nicht](#warum-antwortet-der-wechselrichter-nicht)

------------------------------------------------------------------------------------------
-->

## Allgemeines

Herzlich wilkommen zu den aktuellen Faqs, die aktuell noch in der Entwicklung sind und einen kleinen Überblick über das Projekt geben sollen 

Vielleicht könnt Ihr Bitte mal so die letzten Beiträge durchgehen und einiges als FAQs mit aufnehmen in der Hoffnung, dass es nicht täglich neu gefragt wird ?

Das könnte vielleicht auch jemand machen, der aktuell nicht mit entwickelt, aber sich gut mit github auskennt ?
Vielleicht auch 1 Dokument für alle Sourcen zusammen - denn einiges wäre ja Allgemeingültig ?

Bitte im entsprechenden Forums Beitrag Hilfe anbieten bzw. weitere Entwicklung hierzu diskutieren.

### Welche Modelle werden unterstützt

Tabelle der Hersteller & Modelle

Alles Wechselrichter die mit nRF24L01+ Modulen per 2.4GHz und ESB (Enhanced Shock Burst) von Nordic Semiconductors erreicht werden kann.

Aktuell unterstützte Modelle:
- ESP8266
- Arduino Nano (schon lange nicht mehr aktualisiert)
- Raspberry Pi

### Welche Geräte / Funktionen werden nicht unterstützt

* Werden Hoymiles HMT und HMS auch unterstützt ?

Nein HMT und HMS verwenden ein anderes Funkmodul und können daher (vorerst) auch nicht unterstützt werden.
Ob die beiden Modelle auch die selben Kommandos verwenden ist bisher unbekannt. 


* Wird DTU-Pro-S auch unterstützt ?

Die DTU-Pro S ist für die o.g. Hoymiles HMT & HMS Modelle gebaut und verwendet ebenfalls ein anderes Funkmodul.
Sie wird also ebenfalls auf absehbare Zeit nicht unterstützt.


### Welche Kommandos werden von der DTU unterstützt

* Statusabfrage
  - detaillierte Statusabfrage der aktuellen Werte
  - allgemeine Hardware / Software Informationen
* Alarmmeldungen
  - alle Meldungen seit der letzten Nacht
  - neue Meldungen
* Kontrollkommandos
  - Start des Wechselrichters (Boot)
  - Stop des Wechselrichters (Shutdown)
  - Restart des Wechselrichters (Reboot)
  - Power Limit (PowerLimit)
  - Power Factor (PowerFactor)
* Parameter setzen
  - Netz Profil (GridProfile)


### Welche Entfernung unterstützen die nRF24L01+ Funkmodule

Es sind scheint unterschiedliche Reichweiten, je nach Gegebenheit, zu geben.
Ich denke ein erster Richtwert wären Sichtkontakt bis zu 10m
Leichte Wände wie Holz, Ziegel etc. bis zu 3m
Alles weiteren Wände eventuell nur 1m

Der Abstand zwischen einem HM-600 war nur knapp 2 m, und durch die Holzdecke + Schindeln.


### Modbus via TCP oder RS485

Wird Modbus für Zähler auch unterstützt ?


### Was sind SunSpec und Victron

SunSpec ist das, was z.B. SMA und Fronius sprechen um die WR zu regeln, du bekommst Werte vom WR und eine Steuerung wie z.B. Victron kann entsprechend nach Batteriestand und Hausverbrauch die Leistung reduzieren, so dass du Nulleinspeisung fahren kannst basiert auf Modbus, hat aber noch einige Register zur Identifikation zusätzlich


### Was ist DRM

DRM ist ein Hardwareport, der für Australien entwickelt ist, da musst mit Widerständen und Schaltern gegen + und - Schalten, bisher keine vernünftigen Schaltungen gefunden, SunSpec ist nur möglich über RS485 wenn nicht Zero-Export aktiv ist, da der RS485 Port dann in den Slavemode geht und sonst mit dem Zähler/Messgerät als Master arbeitet

[DRM Control Box](faq/DRM-controlbox.png)
[DRM Modes](faq/DRM-status.png)

### Was ist AntiReflux


### Welche Modbus Register unterstützt die DTU-Pro

In der Dokumentation zum ModBus Protokoll [1] wird folgende Liste von 
Registern angegeben, hängt das eventuell miteinander zusammen ?

4.3.2 Microinverter Data Register List

The following registers provide a microinverter data register list, 
which can be read-only with the function code `0x03`

<details><summary>Table Microinverter Data Register List</summary>
<p>

| Registers | Name             | Decimal | Units | Remark |
| --------- | ---------------- | ------- | ----- | ------------------------------------------------------------ |
| 0x1000    | Data Type        | /       | /     | Default, 0x3C                                                |
| 0x1001    | Microinverter SN | /       | /     | 12-digit decimal number Big-Endian For example, 116151200012 |
| 0x1002    | Microinverter SN | /       | /     | 12-digit decimal number Big-Endian For example, 116151200012 |
| 0x1003    | Microinverter SN | /       | /     | 12-digit decimal number Big-Endian For example, 116151200012 |
| 0x1004    | Microinverter SN | /       | /     | 12-digit decimal number Big-Endian For example, 116151200012 |
| 0x1005    | Microinverter SN | /       | /     | 12-digit decimal number Big-Endian For example, 116151200012 |
| 0x1006    | Microinverter SN | /       | /     | 12-digit decimal number Big-Endian For example, 116151200012 |
| 0x1007    | Port Number      | /       | /     |                                                              |
| 0x1008    | PV Voltage       | 1       | V     |                                                              |
| 0x1009    | PV Voltage       | 1       | V     |                                                              |
| 0x100A    | PV Current       | 1/2     | A     | 1 for MI Series, 2 for HM Series                             |
| 0x100B    | PV Current       | 1/2     | A     | 1 for MI Series, 2 for HM Series                             |
| 0x100C    | Grid Voltage     | 1       | V     |                                                              |
| 0x100D    | Grid Voltage     | 1       | V     |                                                              |
| 0x100E    | Grid frequency   | 2       | Hz    |                                                              |
| 0x100F    | Grid frequency   | 2       | Hz    |                                                              |
| 0x1010    | PV Power         | 1       | W     |                                                              |
| 0x1011    | PV Power         | 1       | W     |                                                              |
| 0x1012    | Today Production | /       | Wh    |                                                              |
| 0x1013    | Today Production | /       | Wh    |                                                              |
| 0x1014    | Total Production | /       | Wh    |                                                              |
| 0x1015    | Total Production | /       | Wh    |                                                              |
| 0x1016    | Total Production | /       | Wh    |                                                              |
| 0x1017    | Total Production | /       | Wh    |                                                              |
| 0x1018    | Temperature      | 1       | °C    | Microinverter internal temperature                           |
| 0x1019    | Temperature      | 1       | °C    | Microinverter internal temperature                           |
| 0x101A    | Operating Status | /       | /     |                                                              |
| 0x101B    | Operating Status | /       | /     |                                                              |
| 0x101C    | Alarm Code       | /       | /     |                                                              |
| 0x101D    | Alarm Code       | /       | /     |                                                              |
| 0x101E    | Alarm Count      | /       | /     |                                                              |
| 0x101F    | Alarm Count      | /       | /     |                                                              |
| 0x1020    | Link Status      | /       | /     | Communication status with DTU                                |
| 0x1021    | /                | /       | /     | Fixed, 0x07                                                  |
| 0x1022    | Reserved         | /       | /     |                                                              |
| 0x1023    | Reserved         | /       | /     |                                                              |
| 0x1024    | Reserved         | /       | /     |                                                              |
| 0x1025    | Reserved         | /       | /     |                                                              |
| 0x1026    | Reserved         | /       | /     |                                                              |
| 0x1027    | Reserved         | /       | /     |                                                              |
| 0x1028    | Data Type        | /       | /     | Default, 0x3C                                                |
| 0x1029    |                  | /       | /     |                                                              |
</p>
</details>

Die Daten können offenbar mit dem entsprechenden `0x03` Kommando 
angefordert werden und aus der entsprechenden `0x03` Antwort entnommen 
werden:

4.2.3 Read Device Data

<details><summary>Tables Read Device Data</summary>
<p>

* Command sending format

| Name             | Length | Value | Remark        |
| ---------------- | ------ | ----- | ------------- |
| Address          | 1      |       | RS485 Address |
| Function Code    | 1      | 0x03  |               |
| Register Address | 2      |       | Big-Endian    |
| Register Count   | 2      |       | Big-Endian    |
| CRC              | 2      |       | CRC16         |

* Command response format (if success)

| Name            | Length | Value | Remark        |
| --------------- | ------ | ----- | ------------- |
| Address         | 1      |       | RS485 Address |
| Function Code   | 1      | 0x03  |               |
| Data Length     | 2      |       |               |
| Data 1          | 2      |       | Big-Endian    |
| Data 2          | 2      |       | Big-Endian    |
| ......          |        |       |               |
| CRC             | 2      |       | CRC16         |

* Command response format (if failed)

| Name            | Length | Value | Remark        |
| --------------- | ------ | ----- | ------------- |
| Address         | 1      |       | RS485 Address |
| Function Code   | 1      | 0x83  |               |
| Wrong Data Code | 1      | 0x01  |               |
| CRC             | 2      |       | CRC16         |
</p>
</details>

[1] 
https://www.mikrocontroller.net/attachment/552319/Technical-Note-Modbus-implementation-using-3Gen-DTU-Pro-V1.2.pdf



### Was ist MQTT

Das Protokoll ( Message Queuing Telemetry Transport ) ist ein offenes Netzwerkprotokoll für Machine-to-Machine-Kommunikation (M2M), das die Übertragung von Telemetriedaten in Form von Nachrichten zwischen Geräten ermöglicht, trotz hoher Verzögerungen oder beschränkter Netzwerke.
Es ermöglich dem Wechselrichter Inforamtionen an einen Dienst zu senden, die dort abgegriffen werden können.


### Welche MQTT Broker / Home Automation Systeme verwendet ihr

- Home Assistant
- Openhab
- InfluxDB

------------------------------------------------------------------------------------------


## Hardware

### Welche Hardware brauche ich für die verschiedenen Software Projekte

Reicht ein ESP8266 mit 1MB oder muss es unbedingt ein ESP8266 mit 4MB 
sein ?

- ESP8266 mit 4MB Flash ist empfohlen
- Raspberry Pi
- ESP32 mit OpentDTU
- Arduino Nano (aktuell nicht gepflegt, daher u.a. kein Active PowerLimit)

### Welche Hardware gibt es und welche Software läuft darauf 

| Hardware     | Software (Pfad)                |
| ------------ | ------------------------------ |
| Arduino nano | Ahoy DTU `tools/nano`          |
| ESP8266      | Ahoy DTU `tools/esp8266`       |
| ESP8266      | Ahoy DTU `tools/HoyDtuSim`     |
| ESP8266      | Ahoy DTU `tools/NRF24_SendRcv` |
| ESP32        | Open DTU [tbnobody/OpenDTU](https://github.com/tbnobody/OpenDTU/) |
| Raspberry Pi | Ahoy DTU `tools/rpi`           |

### Welches nRF24L01+ Modul verwendet ihr ?

Muß es ein nrf24L01+ sein oder funktioniert auch ein nrf24L01 (ohne Plus) ?

- nrf24L01+ 
- DollaTek 2Pcs NRF24L01 + PA + LNA Funk-Transceiver-Modul 2.4G

Nach den bisherigen Erfahrungen muß es ein `+` Modell sein.
Mit der NRF24 Bibliothek kann man das Modell mit printDetails() ausgeben lassen.

Ich will mir eines bestellen, wo gibt es eine sichere Quelle ?

Die Module die aktuell bei AZDelivery (Amazon) und Makershop (ebay) angeboten werden scheinen i.d.R. zu funktionieren.


### Welchen Mikroprozessor empfehlt ihr ?

ESP32 (OpenDTU) oder ESP8266 (Ahoy-DTU) sind beide zu empfehlen, da sie bereits eine WLAN / WiFi Antenne eingebaut haben.
Der Unterschied liegt ein wenig am Preis und welche Software man darauf laufen lassen möchte.
Wer bereits einen Raspberry Pi in Betrieb hat, der nahe genug an den Wechselrichtern ist, kann auch diesen direkt nutzen.
Auf dem Raspberry Pi sind Änderungen am Code nicht immer mit einem Software-Update (Flashen) verbunden.
Historisch wurde auch der Arduino nano für erste Scans beim Reverse-Engineering verwendet.

### Wie ist das Gerät mit Spannung zu versorgen

Stabile Stromversorgung ...

Am besten nimmt man ein Netzteil mit mindestens 1A Ausgangsstrom und einem Micro USB Kabel.
Am besten nimmt man originale Handyladegeräte z.B. von Samsung oder auch vom Raspberry.
Je besser die Qualität desto stabiler die Spannung und der Strom --> je stabiler der DTU.

Es wird empfohlen einen 10/100uF Elko zwischen +5V und GND des NRF24 Moduls zu löten um den entsprechend
hohen Strombedarf des Moduls beim Senden besser zu unterstützen. Manchmal wird auch empfohlen einen
10/100nF Tantalkondensator dazu parallel zu schalten um die Spannung zu glätten.

------------------------------------------------------------------------------------------


## Software / Installation

Die Software für den ESP32 (OpenDTU) ist ein bißchen übersichtlicher aufgebaut und wird von Thomas B. (@noby) vorbildlich gewartet.

### Welche Software gibt es und mit welcher Hardware läuft sie

Ahoy auf ESP8266 läuft bei mir mehrfach "im Produktiv-Einsatz" seit Wochen. Damit füttere ich die InfluxDB.

Software for ESP32 to talk to Hoymiles Inverters
https://github.com/tbnobody/OpenDTU/

Software for ESP8266, Raspberr
https://github.com/grindylow/ahoy

https://github.com/DanielR92/ahoy/tree/main/tools/rpi

| Software (Pfad)                | Hardware     |
| ------------------------------ | ------------ |
| Ahoy DTU `tools/nano`          | Arduino nano |
| Ahoy DTU `tools/esp8266`       | ESP8266      |
| Ahoy DTU `tools/HoyDtuSim`     | ESP8266      |
| Ahoy DTU `tools/NRF24_SendRcv` | ESP8266      |
| Open DTU [tbnobody/OpenDTU](https://github.com/tbnobody/OpenDTU/) | ESP32        |
| Ahoy DTU `tools/rpi`           | Raspberry Pi |

### BIN Files für Ahoy-DTU

Wo und wie kommt man direkt ohne Entwicklungsumgebung an die .bin ?

Wo liegen die verschiedenen Versionen der .bin´s ?

Den aktuellen Build bekommnt man für den ESP8266 unter: 
https://nightly.link/lumapu/ahoy/workflows/compile_esp8266/main/esp8266.zip

Dort im Bereich Actions findet man den Download, man muss man sich allerdings bei Github anmelden.
Ein Release wird aktuell noch nicht gebaut und die BIN Files sind auch im Master Branch mit Vorsicht zu genießen.
Man sollte ggf. die aktuellsten Commits / Merge Requests kontrollieren bzw. die Issues lesen.

### Platform IO installieren


### Wie definiere ich die Serielle Schnittstelle für den ESP7266/ESP32

* unter Linux

Mit `upload_port = /dev/ttyUSB0` in der platformio.ini unter `[env:d1_mini]` und/oder `[env:node_mcu_v2]`


Kommt der Fehler `could not open port` muß man noch die Berechtigung anpassen,
der Benutzer muss in der dialout Gruppe sein unter Linux. 

```bash
sudo adduser <mein_nutzer> dialout
```

Eventuell muss man sich sogar noch einmal abmelden und wieder anmelden, damit er die Berechtigungen aktualisiert.

* unter Mac OS


* unter Windows

Treiber installieren
COM1:


### Wie kann ich den ESP8266 konfigurieren

Der ESP8266 eröffnet einen eigenen AP (wie zum Beispiel die Fritz!Box) 
Mit diesem muss man sich verbinden wie mit jedem anderen WLAN, 
dann kann man auf die Einstellungen zugreifen und seine eigenen Zugangsdateien fürs Wlan eingeben.

`http://192.168.178.XXX/setup`


### Wo finde ich den original Source Code von Hoymiles

https://gitee.com/iotloves/hoymiles-DTU-PRO/


andycao1860-hoymiles-DTU-PRO.zip and 1 more file
https://we.tl/t-tn7OWR4VdR


### Welche **EXPERIMENTELLEN** Software Funktionen sind bisher noch nicht im Standard enthalten (Pull Request / Merge)

SD Card Support
https://github.com/grindylow/ahoy/compare/main...stefan123t:ahoy:sd_card

Power Limit via mqtt
https://github.com/grindylow/ahoy/pull/109

ESP8266 Async WebServer
https://github.com/grindylow/ahoy/pull/107


### Welche Software Funktionen sind geplant

* State Machine

<details><summary>List State Machine Resources</summary>
<p>

  EMBED WITH ELLIOT: PRACTICAL STATE MACHINES
  https://hackaday.com/2015/09/04/embed-with-elliot-practical-state-machines/

  Multithreading in C und Arduino
  http://stefanfrings.de/multithreading_arduino/index.html

  Using State Machines In Your Designs
  http://aqdi.com/articles/using-state-machines-in-your-designs-3/

  C and C++ Finite State Machine Framework
  http://block-net.de/Programmierung/cpp/fsm/fsm.html

  SMC The State Machine Compiler
  http://smc.sourceforge.net/

  Generate production ready source code from UML state diagrams – and activity diagrams!
  https://www.sinelabore.de/doku.php

  Qfsm - A graphical tool for designing finite state machines
  http://qfsm.sourceforge.net/

  Professioneller Arduino Code: Variablen, State-Machine und Klassen
  https://www.youtube.com/watch?v=MERB1lqqyl8

  STATE YOUR INTENTIONS MORE CLEARLY WITH STATE MACHINES
  https://hackaday.com/2018/04/06/state-your-intentions-more-clearly-with-state-machines/
  https://www.youtube.com/watch?v=v8KXa5uRavg

  Artikel über Finite State Machines
  https://www.mikrocontroller.net/topic/248837
</p>
</details>

------------------------------------------------------------------------------------------


## Konfiguration

### Eintragen der Seriennummer

Die Seriennummern des/der Wechselrichter findet man auf der Rückseite des WRs bzw. der Module.
Man sollte sich die Seriennummer notieren oder abfotografieren, da man manchmal 
nach Installation der Module nicht mehr an diese Information kommt.

### S/N eintragen, muss das "ULL" stehen bleiben (im Source) ?

The datasheet specifies the over-the-air packet format: "Most Significant Byte (MSB) to the left" (cf [datasheet figure 11][3])
```
Address := Byte_4, Byte_3, Byte_2, Byte_1, Byte_0
```
("LSByte must be unique") so `0x1946107301` results in `19 46 10 73 01` "on the air".

Old-style NRF Libraries take `uint64_t` addresses. 
In this case, the correct address to pass to the library would be `(uint64_t)0x1946107301ULL`.

Beispiel direkt im Souce als Kommentar z.B.

Format:
```c
#define DTU_RADIO_ID            ((uint64_t)0x1234567801ULL)
#define WR1_RADIO_ID ((uint64_t)0x1946107301ULL) // 0x1946107300ULL = WR1
#define WR2_RADIO_ID ((uint64_t)0x3944107301ULL) // 0x3944107301ULL = WR2
```



### Wieviele Wechselrichter unterstützt die Software

Ich habe mehr als 3 hoymiles HM-..., wird das auch Unterstützt ?
(muss im Source geändert werden - ich weiss - aber neue Nutzer eher 
nicht)

### Warum antwortet der Wechselrichter nicht

Antwortet der HM-.... auch ohne angeschlossene PV Module bzw. Nachts ?

Nein, für Nachts muss zum testen ein Netzteil für Gleichspannung angeschlossen werden.
Der Wechselrichter läßt sich nur bei einer Spannung von > 30V über das Funkmodul erreichen.

