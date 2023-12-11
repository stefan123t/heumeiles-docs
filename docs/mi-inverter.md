## MI gewonnenen Information (danke an @rejoe2)
Seit Dev. version 0.5.70 unterstützt AhoyDTU auch (teilweise mit gewissen Einschränkungen) Inverter der älteren MI-Baureihe.

### Welche MI gehören zu welcher Generation?
Inverter mit Seriennummern beginnend mit 10x2 verwenden bereits das 3rd Gen. 
Protokoll und verhalten sich im übrigen wie die neueren HM-Modelle mit gleicher Leistung.

Die anderen, älteren MI Inverter (Seriennummern beginnend mit 10x1) verwenden eine etwas anders strukturierte Datenübertragung (2nd Gen. protocol), und liefern daher nicht genau dieselben Daten, so dass z.B. der Wert für AC power durch die  AhoyDTU selbst errechnet werden muss, andere Werte sind teilweise gar nicht verfügbar.

### Welche MI beherschen eine Leistungsbegrenzung?
Es scheinen 2nd Gen.-Geräte mit einem oder zwei Kanäle keine Möglichkeit zur Leistungsbegrenzung anzubieten!
Für 4-Kanal-Geräte gilt die Einschränkung, dass das untere limit mindestens 10% betragen muss (statt  2% für neuere Modele).

### Wie weit ist aktuell der Stand in Ahoy?
Weiter konnte der Code bisher nicht für 4-kanalige MI-Inverter getestet werden. Wer so ein Gerät hat, möge bitte in jedem Fall Rückmeldung auf dem discord-Kanal für MI geben ob bzw. inwieweit alles korrekt funktioniert.
