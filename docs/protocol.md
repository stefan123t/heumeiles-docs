<!--
  - [Protokoll](#protokoll)
    - [Welche Kanäle werden für Senden / Empfangen verwendet](#welche-kanäle-werden-für-senden--empfangen-verwendet)
    - [Was ist Channel Hopping](#was-ist-channel-hopping)
    - [Wie sehen Kommandos oder gesendete / empfangene Frames aus](#wie-sehen-kommandos-oder-gesendete--empfangene-frames-aus)
    - [Was ist eine SingleFrameID / sind MultiFrameIDs](#was-ist-eine-singleframeid--sind-multiframeids)
    - [Welche Prüfsummen (CRC = Cyclic Redundancy Check) gibt es und über welchen Teil der Nachrichten werden sie gebildet](#welche-prüfsummen-crc--cyclic-redundancy-check-gibt-es-und-über-welchen-teil-der-nachrichten-werden-sie-gebildet)
    - [Wie wird die CRC16 bzw. CRC-Modus berechnet](#wie-wird-die-crc16-bzw-crc-modus-berechnet)
    - [Wie wird die CRC8 berechnet](#wie-wird-die-crc8-berechnet)
    - [Wie kann man einen Zeitstempel berechnen](#wie-kann-man-einen-zeitstempel-berechnen)
    - [Was sind Backward/ForwardSubstitution](#was-sind-backwardforwardsubstitution)
    - [Welche Kommandos (MainCmd) und Sub Kommandos (SubCmd) gibt es ?](#welche-kommandos-maincmd-und-sub-kommandos-subcmd-gibt-es-)
      - [Traces der DTU Pro](#traces-der-dtu-pro)
        - [MI Kommandos](#mi-kommandos)
      - [BROADCAST 0x02](#broadcast-0x02)
        - [HM Kommandos](#hm-kommandos)
    - [Welche Device Info REQ_ARW_DAT_ALL (0x15) Sub Kommandos gibt es](#welche-device-info-req_arw_dat_all-0x15-sub-kommandos-gibt-es)
    - [Wie funktioniert das Status selbst Prüfen GetSelfCheckState (0x1E) Sub Kommando](#wie-funktioniert-das-status-selbst-prüfen-getselfcheckstate-0x1e-sub-kommando)
      - [InverterDevInform_Simple | 0x00](#inverterdevinform_simple--0x00)
      - [InverterDevInform_All | 0x01](#inverterdevinform_all--0x01)
      - [HardWareConfig | 0x03](#hardwareconfig--0x03)
      - [SimpleCalibrationPara | 0x04](#simplecalibrationpara--0x04)
      - [SystemConfigPara | 0x05](#systemconfigpara--0x05)
    - [Wie kann man den Device Status prüfen](#wie-kann-man-den-device-status-prüfen)
      - [RealTimeRunData_Debug | 0x0B](#realtimerundata_debug--0x0b)
      - [RealTimeRunData_Reality | 0x0C](#realtimerundata_reality--0x0c)
    - [Wie sieht das Device Info Kommando Alarm Data 0x11 / Alarm Update 0x12 aus ?](#wie-sieht-das-device-info-kommando-alarm-data-0x11--alarm-update-0x12-aus-)
      - [InternalData | 0x14](#internaldata--0x14)
      - [GetLossRate | 0x15](#getlossrate--0x15)
      - [GetSelfCheckState | 0x1E](#getselfcheckstate--0x1e)
      - [InitDataState | 0xFF](#initdatastate--0xff)
    - [Welche Device Control DEVCONTROL_ALL (0x51) Sub Kommandos gibt es](#welche-device-control-devcontrol_all-0x51-sub-kommandos-gibt-es)
    - [Wie sieht ein Device Control Kommando aus ?](#wie-sieht-ein-device-control-kommando-aus-)
    - [Wie kann man das Passwort setzen / zurücksetzen](#wie-kann-man-das-passwort-setzen--zurücksetzen)
    - [Wie funktioniert das Active Power Limit (0x0B) Sub Kommando](#wie-funktioniert-das-active-power-limit-0x0b-sub-kommando)
    - [Wie funktioniert das Reactive Power Limit Setzen (0x0D) Kommando](#wie-funktioniert-das-reactive-power-limit-setzen-0x0d-kommando)
    - [Wie funktioniert das Power Faktor Setzen (0x0D) Kommando](#wie-funktioniert-das-power-faktor-setzen-0x0d-kommando)
    - [Welche Parameter Setzen PARASET_ALL (0x52) Kommandos gibt es](#welche-parameter-setzen-paraset_all-0x52-kommandos-gibt-es)
    - [Welche File Multi-Package Kommandos gibt es](#welche-file-multi-package-kommandos-gibt-es)
    - [Wie wird das DOWN_PRO (0x0E) / DOWN_DAT (0x0A) verwendet](#wie-wird-das-down_pro-0x0e--down_dat-0x0a-verwendet)
      - [File Name: **AT_TOR_Erzeuger_default**](#file-name-at_tor_erzeuger_default)
      - [File Name: **DE_VDE4105_2011**](#file-name-de_vde4105_2011)
      - [File Name: **DE_VDE4105_2018**](#file-name-de_vde4105_2018)
      - [File Name: **AT-OVE-E-8001**](#file-name-at-ove-e-8001)
      - [File Name: **Germany_VDE4105**](#file-name-germany_vde4105)
      - [File Name: **LN_50Hz**](#file-name-ln_50hz)
    - [Was bedeutet die Antwort ANSWER_EXCEPTION_MULTI_ONE 0xF1 bzw. ANSWER_EXCEPTION_ONE_MULTI 0xFF](#was-bedeutet-die-antwort-answer_exception_multi_one-0xf1-bzw-answer_exception_one_multi-0xff)
  - [Funkverbindung](#funkverbindung)
    - [Wird Auto-ACK vom Wechselrichter beim nRF24L01+ unterstützt](#wird-auto-ack-vom-wechselrichter-beim-nrf24l01-unterstützt)
  - [Reverse Engineering](#reverse-engineering)
    - [Wo und wie kann das Protokoll mitgeschnitten werden](#wo-und-wie-kann-das-protokoll-mitgeschnitten-werden)
    - [Was ist ein Scanner und welche gibt es](#was-ist-ein-scanner-und-welche-gibt-es)

------------------------------------------------------------------------------------------
-->

## Protokoll



### Welche Kanäle werden für Senden / Empfangen verwendet

Soviel ich weiß haben die nrf24l01 nur bis zu 126 Kanäle.

// Depending on the program, the module can work on 2403, 2423, 2440, 2461 or 2475MHz.
// Channel List      2403, 2423, 2440, 2461, 2475MHz


* Senden
  - Kanal ~~2.403, 2.423,~~ 2.440, ~~2.461, 2.475~~ GHz

* Empfangen
  - Kanal 2.403, 2.423, 2.440, 2.461, 2.475 GHz

### Was ist Channel Hopping

* Channel Hopping
  - Empfangen, auf allen Kanälen 
  - Senden, meist auf Kanal 2,403 GHz

ich wurde gerade hierauf verwiesen:
https://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.sdk51.v9.0.0%2Fgzll_02_user_guide.html&cp=4_1_0_5_0

Kann es sein das dieses Gazell unser Channel hopping ist?
Auch wenn sich oben genannte Doku auf einen nRF52833 bezieht steht bei 
den Features: Backward compatible with legacy nRF24L Series Gazell.

hier scheint wohl so eine Implementierung des gzll Protokolls zu sein
https://github.com/wangdong/cpod/blob/master/lib/nrf24/gazell/common/gzll.c
Leider kann das wohl die nRF24 lib nicht.

Das Kommunikationsschema von Gazell sieht aber IMHO anders aus. Das ist 
Device-getriggert und der Host lauscht erstmal nur und antwortet auf 
Anfragen der Devices.

Insofern müssten die HMs von sich aus auf einem Anker-Kanal "ungefragt" 
vor sich hin senden.
Das tun sie aber nach aktuellem Kenntnisstand nicht, sondern antworten 
auf Anfragen des Hosts. Das Kommunikationsschema stellt sich für mich 
eher "klassisch" dar, also Anfrage Host->Device, dann Antwort 
Device->Host.
Die max. Anzahl der für die DTUs spezifizierten "Solarmodule" ist mit 99 
auch deutlich höher, als die für Gazell maximal spezifizierten 8 
Teilnehmer.

zu den genutzten Frequenzen.
Bei meinem HM-600 ist es immer so:
Wenn ich ein 80 Telegramm sende auf 2403, dann antwortet der WR mit den 
Antworten 01,02,83  auf den möglichen Frequenzen 2423,2440,2461 MHz.
also bei TX 2403, Antworten auf 2423,2440,2461
     bei TX 2423, Antworten auf 2403,2440,2475
     bei TX 2440, Antworten auf 2403,2423,2475
     bei TX 2461, Antworten auf 2403,2423,2475
     bei TX 2475, Antworten auf 2403,2423,2440
Wenn man die möglichen Frequenzen scannt nach dem Senden, dann empfängt 
man alle Antworten. Andere Antworten als 01,02,83 habe ich bisher nie 
empfangen.


### Wie sehen Kommandos oder gesendete / empfangene Frames aus

`0x7E` `0x15` `0x76 0x54 0x32 0x10` `0x78 0x56 0x34 0x12` `0x80` `0x0B` `0x00` `0xXY` .. [`0x12 34`] `0xCD` `0x7F`

`<SOF>` `<Cmd>` `<WR Serial Id>` `<DTU Serial Id>` `<Frm>` `<SubCmd>` `<Rev>` `<User data>` [`<CRC16>`] `<CRC8>` `<EOF>`

### Was ist eine SingleFrameID / sind MultiFrameIDs

* Single Frame ID

  Die Single Frame ID ist `0x80`

* Multi Frame ID

  Multi Frame IDs werden für Nachrichten >12 Byte Payload verwendet.

  Multi Frame IDs beginnen mit `0x01`, `0x02`, ..., das letzte Paket enthält die Ende-Kennung `0x8N` (`0x80 | 0x0N` Frame ID).

  Es darf also maximal `0x7F` < 127 Pakete in einer Nachricht / Payload oder 1524 Bytes geben.

### Welche Prüfsummen (CRC = Cyclic Redundancy Check) gibt es und über welchen Teil der Nachrichten werden sie gebildet

```text
                  |<-------------------------------------------------------CRC8----------------------------------------------->|
                                                            |<-------------CRC16 'modbus' für CRC_M----------------->|
             7E   15   72 22 02 00      72 22 02 00      80 0B 00     62 09 04 9b      00 00     00 00   00 00   00 00     F2 68    F0    7F
             ^^   ^^   ^^^^^^^^^^^      ^^^^^^^^^^^      ^^           ^^^^^^^^^^^                                          ^^^^^    ^^    ^^
Bedeutung    SOF  MID  WR ser#          WR ser#          CMD  ?       TIME (UTC)                                           CRC_M    CRC8  EOF
```



### Wie wird die CRC16 bzw. CRC-Modus berechnet

[CRC-Berechnung, Einstellungen für HxD](faq/crc_modbus.png)

```text
Erzeuge Prüfsummen
Verfügbare Algorithmen: Benutzerdefiniertes CRC (16-Bit)
(*) Markierte Daten
Benutzerdefiniertes CRC...

Benutzerdefiniertes CRC
Bitbreite: (*) 16
Polynom: 8005
Startwert: FFFF
Ausgabe XOR: 0000
Reflexion:
[x] Eingabe
[x] Ausgabe
Ok
```

Die CRC16 geht mit folgenden Einstellungen:
[CRC16](faq/CRC16-CRC-Modbus.png)

```text
CRC width
Bit length: (*) CRC-16

CRC parametrization
(*) Custom

CRC detailed parameters
Input reflected: [ ] Result reflected: [x]
Polynomial: 0x8005
Initial Value: 0xFFFF
Final Xor Value: 0x0000

CRC Input Data
(*) Bytes
0x00 0x00

Result CRC value: 0xB001
```

Oder kurz https://crccalc.com/?crc=0x0000&method=CRC-16/MODBUS&datatype=hex&outtype=0 


CRC-16 über die Daten nach der MultiFrameID berechnen:

```c
    for(i = 10; i < 24; i++)
    {
        if((i - 10) % 2 == 1)
        {
            TempCrc = (u16)(temp_dat[i - 1] << 8) | (temp_dat[i]);
            DatCrc =  CalcCRC16t(TempCrc, DatCrc);
        }
    }

    temp_dat[24] = (u8)(DatCrc >> 8);
    temp_dat[25] = (u8)(DatCrc);
```

CRC16_MODBUS_POLYNOM 0xA001 ist in crc.h definiert, das ist wohl ein reversed CRC-16-IBM Polynomial.
Wird u.a. für Bisync, **Modbus**, USB, ANSI X3.28, many others; also known as CRC-16 and CRC-16-ANSI verwendet.


### Wie wird die CRC8 berechnet

Die CRC8 läßt sich z.B. auf http://www.sunshine2k.de/coding/javascript/crc/crc_js.html berechnen:
[CRC8](faq/CRC8.png)

```text
CRC width
Bit length: (*) CRC-8

CRC parametrization
(*) Custom

CRC detailed parameters
Input reflected: [ ] Result reflected: [ ]
Polynomial: 0x01
Initial Value: 0x00
Final Xor Value: 0x00

CRC Input Data
(*) Bytes
0x51 0x81 0x10 0x15 0x07 0x81 0x10 0x15 0x07 0x81 0x00 0x00 0xB0 0x01

Result CRC value: 0x61
```

Oder ganz einfach mit https://crccalc.com/?crc=0x518110150781101507810000B001&method=CRC-8/ITU&datatype=hex&outtype=0 


CRC8 über alles berechnen

```c
    temp_dat[26] = Get_crc_xor((u8 *)temp_dat, 26);
```

```c
#define CRC8_INIT 0x00
#define CRC8_POLY 0x01

#include "crc.h"

uint8_t crc8(uint8_t buf[], uint8_t len)
{
    uint8_t crc = CRC8_INIT;
    for (uint8_t i = 0; i < len; i++) {
        crc ^= buf[i];
        for (uint8_t b = 0; b < 8; b++) {
            crc = (crc << 1) ^ ((crc & 0x80) ? CRC8_POLY : 0x00);
        }
    }
    return crc;
}
```

### Wie kann man einen Zeitstempel berechnen

0x627b69fe = 1652255230
```bash
$ date --date='@1652255230'
Wed 11 May 2022 09:47:10 AM CEST
```

62D80183 ist der Timestamp im UNIX Epoch Format: 
```bash
$ date --date="@$(echo 'ibase=16; 62D80183'|bc)" '+%F %H:%M:%S'
2022-07-20 15:22:11
```

Geht auch umgekehrt:
```bash
$ echo "obase=16; $(date --date='2022-07-01 00:00:00' +%s)"|bc
62BE1CE0
```

bash commands mal in alias einbauen^^

```bash
$ date --date="@$(echo 'ibase=16; 62D80707'|bc)" '+%F %H:%M:%S'
2022-07-20 14:45:43
```


### Was sind Backward/ForwardSubstitution

ForwardSubstitution und BackwardSubsitution sind eine Escape- und Unescape-Verfahren für die nRF24 Schnittstelle.

Da die Bytes Start of Frame <SOF> `0x7E` und End of Frame <EOF> `0x7F` reservierte Zeichen sind muß ggf. deren Auftreten ersetzt werden.
Da `0x7E` und `0x7F` Steuerzeichen (Start Of Frame und End Of Frame) sind müssen diese Escaped werden. Dafür muss das Zeichen `0x7D` herhalten, daher muss es auch Escaped werden. Rückwärts gehts eben genau umgekehrt.

Dies erfolgt anhand folgender Übersetzungstabelle:

| Backward | ForwardSubstitution |
| -------- | ------------------- |
| `0x7D`   | `0x7D5D`            |
| `0x7E`   | `0x7D5E`            |
| `0x7F`   | `0x7D5F`            |

Hier wird `0x7D5F` anstelle von `0x7F` bzw. `0x7D5E` anstelle von `0x7E` und `0x7D5D` anstelle von `0x7D` verwendet.
Ich hatte mich schon gewundert warum manche Pakete länger sind als andere =^D

### Welche Kommandos (MainCmd) und Sub Kommandos (SubCmd) gibt es ?

MainCmd: `0x51` DEVCONTROL_ALL
SubCmd / Control Type: Type_TurnOff = `0x01` + `0x00` wegen den Bitshifts bei der Übergabe des Parameters ?

Verbindungsstatus HM 
```text
7E 06 81101507 81101507 00 06 7F
7E 06 81101507 81101507 00 06 7F
```

Verbindungsstatus MI
```text
7E 06 63500316 63500316 00 06 7F // MainCmd REQ_RF_SVERSISON 0x06 
7E 06 63500316 63500316 00 06 7F
7E 06 63500316 63500316 00 06 7F
```

Autoscan und Scan nach dem MI
```text
7E 01 73600117 73600117 00 01 7F // MainCmd CHANGE_MOD_2M_250K 0x01 Change Baud rate to 250kHz, SubCmd = 0x00
```

Autoscan und Scan nach dem MI
```text
7E 02 63500316 63500316 00 02 7F // MainCmd BROADCAST 0x02, SubCmd = 0x00
```

Suche nach HM-WR ID aus dem System:
```text
7E 02 81101507 81101507 00 02 7F // MainCmd BROADCAST 0x02, SubCmd = 0x00
```

```text
   51 63500316 63500316 5A5A 34 0C60 09 52  3168  // MainCmd CONTROL_LOCK_MI__LIMIT_POWER_ONOFF 0x51, SubCmd CONTROL_LIMIT_POWER_SUB 0x5A5A 
```

danke für die Traces

Für MI-WR: MainCmd:
```text
0x01 CHANGE_MOD_2M_250K
0x02 BROADCAST
0x06 REQ_RF_SVERSISON 
0x07 REQ_RF_RVERSISON mit SubCmd = 0x00 alle in UsartNrf_Send_NetCmdToNrfCmd().
0x0F REQ_VERSISON in UsartNrf_Send_PackNrfCmd() bzw. UsartNrf_Send_PackBaseCommand()
```

Ausgewertet wird bei
```text
0x81 ANSWER_CHANGE_MOD_2M_250K direkt in UsartNrf_Process_Loop() und 
0x02 BROADCAST in UsartNrf_Process_Inverter_NetCmd_SearchId() 
0x86 ANSWER_REQ_RF_SVERSISON in UsartNrf_Process_Inverter_Version() bzw. UsartNrf_Process_Inverter_Version_InverterRf
0x87 ANSWER_REQ_RF_RVERSISON in UsartNrf_Process_Inverter_Version_DtuRf(),
0x8F ANSWER_REQ_VERSISON in UsartNrf_Process_Version_Inverter(),
```

Für den HM-WR: `UsartNrf3_Send_Mi_Nrf_VER()` mit `temp_dat[0] = 0x06` (= MainCmd)
die Auswertung erfolgt in `UsartNrf_Process_Inverter_Version_InverterRf()` 

Seriennummer Deiner DTU-PRO posten, damit ich mir mal die CRC Prüfsummen ansehen kann. 
Ich bekomme die nämlich noch nicht sauber hin.
`10F873600117`

Die müssten noch in die Markdown Dokumentation auf `grindylow-ahoy/docs/hoymiles-format-description.md`
aber ich würde das vermutlich erst machen, wenn ich die anderen Kommandos ebenfalls verstanden habe.

Wenn Du willst kannst Du es aber gerne schon mal anfangen / weitermachen. 
Ich habe vor einiger Zeit auch schon mal angefangen mit [wavedrom](https://github.com/wavedrom/wavedrom) einzelne Pakete bzw. Kommandos zu dokumentieren.
Aber bisher war ja außer dem `0x0B` RealTimeRunData_Debug bzw. "Zeit setzen" und damit Werte abfragen noch nicht so viel bekannt.


#### Traces der DTU Pro

Verschiedene Leistungen, ganzes File folgt in Kürze, das ist unformatiert
zum Schluss hin ist es maximale Leistung, davor etwa 350-450W schwankend

    63500316 ist der MI-600 (Klon) @Ichirou
    81101507 ist der HM-1500 @Ichirou
112172615582 ist ein HM-600 @klahus1

##### MI Kommandos
Device Info:
```text
7E 09 63500316 63500316 00 09 7F // ??? Data A
7E 11 63500316 63500316 00 11 7F // ??? Data B
```

Device Control:
```text
7E 51 63500316 63500316 5A5A 25 08CC B0 7F // Power Limit 37% ???
7E 51 63500316 63500316 5A5A 5D 15CC D5 7F // Power Limit 93% ???
```


#### BROADCAST 0x02

BROADCAST ist MainCmd 0x02 und SubCmd 0x00. Also m.E. 02 72615582 78563412 00 CRC8 
Tausche mal noch die DTU ID gegen die richtige, sonst antwortet der WR sich selbst.

<details><summary>traces</summary>
<p>

```
23:01:43.299 > Fetch inverter: 112172615582
23:01:43.299 > sendCommand: BROADCAST
23:01:43.302 >  >>> Command BROADCAST <<<
23:01:43.305 > 
23:01:43.305 > sendStatsRequest
23:01:43.308 > sendAlarmLogRequest
23:01:43.308 > sendEsbPacket
23:01:43.310 > TX 02 72 61 55 82 78 56 34 12 00 CE 
23:01:45.341 > RX Period End
23:01:45.342 > All missing
23:01:45.342 > Nothing received, resend whole request
23:01:45.347 > TX 02 72 61 55 82 78 56 34 12 00 CE 
23:01:47.373 > RX Period End
23:01:47.373 > All missing
23:01:47.373 > Nothing received, resend whole request
23:01:47.378 > TX 02 72 61 55 82 78 56 34 12 00 CE 
23:01:49.404 > RX Period End
23:01:49.404 > All missing
23:01:49.404 > Nothing received, resend whole request
23:01:49.409 > TX 02 72 61 55 82 78 56 34 12 00 CE 
23:01:51.434 > RX Period End
23:01:51.435 > All missing
23:01:51.435 > Nothing received, resend count exeeded
```
</p>
</details>

TX 02 72615582 78563412 00 CE 

###### 

Es gibt im Original Code eine Methode um die Baudrate zu ändern: `GetInveterBaudType` und `CHANGE_MOD_2M_250K` bzw. 
```c
typedef enum
{
    Device_250K = 1,
    Device_2M = 0,
    Device_INIT_BAUD = 3
} BaudType;
```

die Definition des `BROADCAST` Command
```c
#define BROADCAST                           0x02                        //Query network terminal device ID
#define ANSWER_REQHOST                      (BROADCAST | 0x80 | 0x40)
#define ANSWER_BROADCAST                    (BROADCAST | 0x80)

#define BROADCAST_ON                        0x18                        //Query the status of terminal A channel
#define ANSWER_BROADCAST_ON                 (BROADCAST_ON | 0x80)

#define REQ_NUB_BROADCAST                   0x03                        // Request the number of broadcast commands
#define ANSWER_REQ_NUB_BROADCAST            (REQ_NUB_BROADCAST | 0x80)  //83
```

und hier die Methode `UsartNrf_Process_Inverter_NetCmd_SearchId`:
```c
/***********************************************
** Function name: Second-generation protocol, broadcast command, search id, receive receipt processing
** Descriptions:
** input parameters:
** output parameters:
** Returned value:
*************************************************/
void UsartNrf_Process_Inverter_NetCmd_SearchId(u8 *pBuffer)
{
    static vu16 PortCnt = 0;
    vu16 i;

    if(PortCnt == 0)
    {
        PortCnt = Dtu3Detail.Property.PortNum;//Total number of connections
    }

    for(i = 0; i < PortCnt; i++)
    {
        if(((memcmp(&(pBuffer[10]), (u8 *)MIMajor[i].Property.Pre_Id, 2) != 0) || (memcmp(&(pBuffer[12]), (u8 *)MIMajor[i].Property.Id, 4) != 0)) && ((pBuffer[11] & 0xf0) <= 0x60))
        {
            memcpy((u8 *)MIMajor[PortCnt].Property.Pre_Id, (&pBuffer[10]), 2);
            memcpy((u8 *)MIMajor[PortCnt].Property.Id, (&pBuffer[2]), 4);// The original network id remains unchanged, and the subsequent insert id

            if(UsartNrf_GetInvterType((u8 *)MIMajor[PortCnt].Property.Pre_Id) == Inverter_500)
            {
                if((MIMajor[PortCnt].Property.Port != MI_500W_A) && (MIMajor[PortCnt].Property.Port != MI_500W_B))
                {
                    memcpy((u8 *) & (MIMajor[PortCnt + 1].Property.Id[0]), (u8 *)&MIMajor[PortCnt].Property.Id[0], sizeof(MIMajor[PortCnt].Property.Id));
                    memcpy((u8 *) & (MIMajor[PortCnt + 1].Property.Pre_Id[0]), (u8 *)&MIMajor[PortCnt].Property.Pre_Id[0], sizeof(MIMajor[PortCnt].Property.Pre_Id));
                    MIMajor[PortCnt].Property.Port = MI_500W_A;
                    MIMajor[PortCnt + 1].Property.Port = MI_500W_B;
                    Dtu3Detail.Property.PortNum = Dtu3Detail.Property.PortNum + 2;
                }
            }
            else if(UsartNrf_GetInvterType((u8 *)MIMajor[PortCnt].Property.Pre_Id) == Inverter_1000)
            {
                if((MIMajor[PortCnt].Property.Port != MI_1000W_A) && (MIMajor[PortCnt].Property.Port != MI_1000W_B) && (MIMajor[PortCnt].Property.Port != MI_1000W_C) && (MIMajor[PortCnt].Property.Port != MI_1000W_D))
                {
                    memcpy((u8 *)&MIMajor[PortCnt + 1].Property.Id[0], (u8 *)&MIMajor[PortCnt].Property.Id[0], sizeof(MIMajor[PortCnt].Property.Id));
                    memcpy((u8 *)&MIMajor[PortCnt + 1].Property.Pre_Id[0], (u8 *)&MIMajor[PortCnt].Property.Pre_Id[0], sizeof(MIMajor[PortCnt].Property.Pre_Id));
                    memcpy((u8 *)&MIMajor[PortCnt + 2].Property.Id[0], (u8 *)&MIMajor[PortCnt].Property.Id[0], sizeof(MIMajor[PortCnt].Property.Id));
                    memcpy((u8 *)&MIMajor[PortCnt + 2].Property.Pre_Id[0], (u8 *)&MIMajor[PortCnt].Property.Pre_Id[0], sizeof(MIMajor[PortCnt].Property.Pre_Id));
                    memcpy((u8 *)&MIMajor[PortCnt + 3].Property.Id[0], (u8 *)&MIMajor[PortCnt].Property.Id[0], sizeof(MIMajor[PortCnt].Property.Id));
                    memcpy((u8 *)&MIMajor[PortCnt + 3].Property.Pre_Id[0], (u8 *)&MIMajor[PortCnt].Property.Pre_Id[0], sizeof(MIMajor[PortCnt].Property.Pre_Id));
                    MIMajor[PortCnt].Property.Port = MI_1000W_A;
                    MIMajor[PortCnt + 1].Property.Port = MI_1000W_B;
                    MIMajor[PortCnt + 2].Property.Port = MI_1000W_C;
                    MIMajor[PortCnt + 3].Property.Port = MI_1000W_D;
                    Dtu3Detail.Property.PortNum = Dtu3Detail.Property.PortNum + 4;
                }
            }
            else if(UsartNrf_GetInvterType((u8 *)MIMajor[PortCnt].Property.Pre_Id) == Inverter_250)
            {
                MIMajor[PortCnt].Property.Port = MI_250W; // 0x01
                Dtu3Detail.Property.PortNum = Dtu3Detail.Property.PortNum + 1;
            }

            if(UsartNrf_GetInvterType((u8 *)MIMajor[PortCnt].Property.Pre_Id) == Inverter_250)
            {
                PortCnt = PortCnt + 1;
                i  = i + 1;
            }
            else if(UsartNrf_GetInvterType((u8 *)MIMajor[PortCnt].Property.Pre_Id) == Inverter_500)
            {
                PortCnt = PortCnt + 2;
                i = i + 2;
            }
            else if(UsartNrf_GetInvterType((u8 *)MIMajor[PortCnt].Property.Pre_Id) == Inverter_1000)
            {
                PortCnt = PortCnt + 4;
                i = i + 4;
            }

            MIReal[PortNO].Data.NetStatus = (u8)((PortCnt * 100) / PORT_LEN);

            if(PortCnt >= PORT_LEN)
            {
                return;
            }

            return;
        }
    }

    return ;
}
```

##### HM Kommandos
```text
7E 15 81101507 81101507 FF EA 7F ???
```

Retransmits:
```text
7E 15 81101507 81101507 82 97 7F
7E 15 81101507 81101507 83 96 7F
7E 15 81101507 81101507 84 91 7F
7E 15 81101507 81101507 85 90 7F
7E 15 81101507 81101507 86 93 7F
7E 15 81101507 81101507 87 92 7F
7E 15 81101507 81101507 88 9D 7F
7E 15 81101507 81101507 89 9C 7F
7E 15 81101507 81101507 8A 9F 7F
7E 15 81101507 81101507 8B 9E 7F
```

Device Info:
`RealTimeRunData_Debug` `0x0B` mit verschiedenen Zeitstempeln
```text
7E 15 81101507 81101507 80 0B00 62D806F7 0000 259C 00000000 2C4F 0F 7F
7E 15 81101507 81101507 80 0B00 62D806F9 0000 259C 00000000 4C03 2D 7F
7E 15 81101507 81101507 80 0B00 62D806FA 0000 259C 00000000 BC17 CA 7F
7E 15 81101507 81101507 80 0B00 62D806FB 0000 259C 00000000 2C1A 56 7F
```

AlarmData `0x11`
```text
7E 15 81101507 81101507 80 1100 62D806FC 0000 259C 0000 0000 C627 9C 7F
```

Device Control:
```text
7E 51 81101507 81101507 81 0B00 2B98 0000 6B89 8A 7F // Active Power Limit 0x0B; 0x2B98 = 1116.0 W
```


### Welche Device Info REQ_ARW_DAT_ALL (0x15) Sub Kommandos gibt es

<details><summary>source code</summary>
<p>

```c
typedef enum
{
    InverterDevInform_Simple = 0, // 0x00
    InverterDevInform_All = 1, // 0x01
    GridOnProFilePara = 2, // 0x02
    HardWareConfig = 3, // 0x03
    SimpleCalibrationPara = 4, // 0x04
    SystemConfigPara = 5, // 0x05
    RealTimeRunData_Debug = 11, // 0x0b
    RealTimeRunData_Reality = 12, // 0x0c
    RealTimeRunData_A_Phase = 13, // 0x0d
    RealTimeRunData_B_Phase = 14, // 0x0e
    RealTimeRunData_C_Phase = 15, // 0x0f
    //Alarm data - all unsent alarms
    AlarmData = 17, // 0x11
    //Alarm data - all pending alarms
    AlarmUpdate = 18, // 0x12
    RecordData = 19, // 0x13
    InternalData = 20, // 0x14
    GetLossRate = 21, // 0x15
    GetSelfCheckState = 30, // 0x1e
    InitDataState = 0xff, // 0xFF
} DataType;
```
</p>
</details>

SubCmd =
* InverterDevInform_Simple (0x00)
* GridOnProFilePara (0x02)
* HardWareConfig (0x03) ???
* SimpleCalibrationPara (0x04) ???
* SystemConfigPara (0x05) ???
* RealTimeRunData_Debug (0x0B)
* RealTimeRunData_Reality (0x0C)
* RealTimeRunData_A_Phase (0x0D) ???
* RealTimeRunData_B_Phase (0x0E) ???
* RealTimeRunData_C_Phase (0x0F) ???
* AlarmData (0x11)
* AlarmUpdate (0x12)
* RecordData (0x13)
* InternalData (0x14) ???
* ~~GetLossRate (0x15) ???~~
* ~~GetSelfCheckState (0x1E) ???~~

Bei allen anderen Anfragen erfolgt vorher ein CurNetCmd = NET_INIT, 
also MainCmd = REQ_ARW_DAT_ALL (0x15) und SubCmd = RealTimeRunData_Reality (0x0c) bzw. RealTimeRunData_Debug (0x0b).
Wir verwenden ja schon länger den zweiten Fall 0x0b für die Status Meldungen

```
15 72 61 55 82 78 56 34 12 80 0X00 <timestamp> 0000 0000 00000000 CRC16 CRC8 für X 0, 1, 2, 3, 4, 5 ?
```

Auf irgendeinen dieser DevInform Anfragen muss der WR doch antworten ?
Das selbe verwenden wir ja schon lange mit RealTimeRunData_Debug 0x0B.
Ja, dass wäre schön. Vorallem HW Rev und FW Rev sind relevant.

```
15 72 61 55 82 78 56 34 12 80 0000 <timestamp> 0000 0000 00000000 CRC16 CRC8 // InverterDevInform_Simple 0x00
15 72 61 55 82 78 56 34 12 80 0100 <timestamp> 0000 0000 00000000 CRC16 CRC8 // InverterDevInform_All 0x01
15 72 61 55 82 78 56 34 12 80 0200 <timestamp> 0000 0000 00000000 CRC16 CRC8 // GridOnProFilePara 0x02
15 72 61 55 82 78 56 34 12 80 0300 <timestamp> 0000 0000 00000000 CRC16 CRC8 // HardWareConfig 0x03
15 72 61 55 82 78 56 34 12 80 0400 <timestamp> 0000 0000 00000000 CRC16 CRC8 // SimpleCalibrationPara 0x04
15 72 61 55 82 78 56 34 12 80 0500 <timestamp> 0000 0000 00000000 CRC16 CRC8 // SystemConfigPara 0x05
15 72 61 55 82 78 56 34 12 80 0C00 <timestamp> 0000 0000 00000000 CRC16 CRC8 // RealTimeRunData_Reality 0x0C
15 72 61 55 82 78 56 34 12 80 1400 <timestamp> 0000 0000 00000000 CRC16 CRC8 // InternalData 0x14
15 72 61 55 82 78 56 34 12 80 1500 <timestamp> 0000 0000 00000000 CRC16 CRC8 // GetLossRate 0x15
15 72 61 55 82 78 56 34 12 80 1E00 <timestamp> 0000 0000 00000000 CRC16 CRC8 // GetSelfCheckState 0x1E
```

welches Format hat der TimeStamp?
Timestamp sind 4 Byte wie üblich.
Unix Epoch Format



@drschiffler hier sind schon mal die ersten DevInform Anfragen und Antworten interpretiert anhand des DTU-Pro Source Codes.
Falls Du neben dem DevControl auch die o.g. DevInform Pakete einbauen möchtest ?
Speziell das -vvv- u.g. InverterDevInform_Simple ist hilfreich, da es u.a. die Hardware und Firmware Version beinhaltet!



### Wie funktioniert das Status selbst Prüfen GetSelfCheckState (0x1E) Sub Kommando

Interessant wäre auch:
`GetSelfCheckState: // 0x1e`
Da kann man die Serial ID und SW/HW Version des Wechselrichters auslesen...


```text
15 74403329 78563412 80 1100 62D80183 0000 0000 00000000 0765 FE --- AlarmData 0x11
15 74403329 78563412 80 1200 62D80183 0000 0000 00000000 FFC4 2A --- AlarmUpdate 0x12
15 74403329 78563412 80 1E00 62D80183 0000 0000 00000000 086A 0E --- GetSelfCheckState 0x1E
^^------------------------------------------------------------------ MainCmd 0x15 REQ_ARW_DAT_ALL
   ^^^^^^^^--------------------------------------------------------- WR Serial ID
            ^^^^^^^^------------------------------------------------ DTU Serial ID
                     ^^--------------------------------------------- MultiFrameID 0x80
                        ^^------------------------------------------ SubCmd bzw. DataType: 0x11 = AlarmData, 0x12 AlarmUpdate
                          ^^---------------------------------------- rev Protocol Revision ?
                             ^^^^^^^^------------------------------- UNIX timestamp 62BE1CE0 -> 2022-07-01 00:00:00
                                      ^^^^-------------------------- Gap always 0x0000
                                           ^^^^--------------------- 0x0000, nur bei AlarmData: WarnSerNub (Warning Serial Number)  
                                                ^^^^^^^^------------ Password always 0x0000
                                                         ^^^^------- CRC16 / CRC-Modbus über die UserData, excl. Frame ID!
                                                              ^^---- CRC8
```

MainCmd `0x15`, `0x80` MultiFrameID, SubCmd GetSelfCheckState `0x1E`, 
Timestamp wie oben, Gap ist `0x0000` und Password ist `0x00000000`

Probiere mal: `15 74403329 78563412 80 1E00 62D80183 0000 0000 00000000 086A 0E` --- GetSelfCheckState `0x1E`

```text
Transmit 27 | 15 74 40 33 29 78 56 34 12 80 1E 00 62 D8 01 83 00 00 00 00 00 00 00 00 08 6A F7
Received 21 bytes channel 23: 95 74 40 33 29 74 40 33 29 81 00 01 00 00 00 00 00 00 CB 50 8E
Payload: 00 01 00 00 00 00 00 00 cb 50
```

Das erste Byte `0x95` ist die Antwort `0x15 | 0x80 = 0x95`

#### InverterDevInform_Simple | 0x00

<details><summary>traces</summary>
<p>

```
23:41:51.618 > Fetch inverter: 112172615582
23:41:51.618 > sendCommand: InverterDevInform_Simple
23:41:51.623 > sendEsbPacket
23:41:51.623 > TX 15 72 61 55 82 78 56 34 12 80 00 00 62 E6 F7 1F 00 00 00 00 00 00 00 00 24 A3 B2 
23:41:51.683 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 81 27 1A 10 10 10 15 02 00 03 00 20 01 00 00 6C 17 77 
23:41:51.871 > RX Period End
23:41:51.871 > Success
```
</p>
</details>

jetzt geht es ans parsen...
@klahus1 Danke fürs loggen, hier die Antwort, da kann jetzt jeder seine HW Version und Firmware Version überprüfen!

```
TX 15 72615582 78563412 80 0000 62E6F71F 0000 00000000 0000 24A3 B2    InverterDevInform_Simple 0x00
RX 95 72615582 72615582 81 271A 1010 1015 0200 0300 2001 0000 6C17 77  
                           ^^^^--------------------------------------- AppFWBuild_VER Application version
                                ^^^^---------------------------------- HW_PNH Hardware part number
                                     ^^^^----------------------------- HW_PNL Hardware part number
                                          ^^^^------------------------ HW_VER Hardware version
                                               ^^^^------------------- GPFCode Grid-connected protection file code
                                                    ^^^^-------------- GPFVer Grid-connected protection file version
                                                         ^^^^⁻-------- ReservedPara Reserved parameters
```

Weiter gehts:

#### InverterDevInform_All | 0x01

<details><summary>traces</summary>
<p>

```
23:55:48.318 > Fetch inverter: 112172615582
23:55:48.318 > sendCommand: InverterDevInform_All
23:55:48.323 > sendEsbPacket
23:55:48.323 > TX 15 72 61 55 82 78 56 34 12 80 01 00 62 E6 FA 64 00 00 00 00 00 00 00 00 ED 24 8B 
23:55:48.386 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 81 27 1A 07 E4 02 C3 05 84 00 66 00 00 00 00 84 F4 9C 
23:55:48.570 > RX Period End
23:55:48.570 > Success
```
</p>
</details>

Hier scheint irgendwas mit der Antwort noch nicht ganz zu passen, u.a. ist bereits die HW_PNH eine andere als bei der InverterDevInform_Simple Antwort.
Die laut DTU-Pro vorhandenen Details danach sind offenbar auch nicht enthalten. Hmm.
```
TX 15 72615582 78563412 80 0100 62E6FA64 0000 00000000 0000 ED24 8B    InverterDevInform_All 0x01
RX 95 72615582 72615582 81 271A 07E4 02C3 0584 0066 0000 0000 84F4 9C  UsartNrf3_Process_DevInform_All()
                           ^^^^--------------------------------------- AppFWBuild_VER Application version
                                ^^^^---------------------------------- AppFWBuild_YYYY Application firmware compilation time-year
                                     ^^^^----------------------------- AppFWBuild_MMDD Application firmware compilation time-month. day
                                          ^^^^------------------------ AppFWBuild_HHMM Application version
                                               ^^^^------------------- USFWBuild_VER Hardware part number
                                                    ^^^^-------------- HW_PNH Hardware part number
                                                         ^^^^--------- AppFW_PNL Hardware part number
                                                         ^^^^--------- AppFW_PNL Hardware part number ???
                                                         ^^^^--------- HWSPECVER Hardware version ???
                                                         ^^^^--------- GPFCode Grid-connected protection file code ???
                                                         ^^^^--------- GPFVer Grid-connected protection file version ???
```

Was bedeutet hier eigentlich nochmals 95 als Byte?

F1 bedeutet ja, das er die Anfrage verworfen hat.
Und 95?
Das ist die Antwort auf die Anfrage mit 0x15. Es ist immer +0x80 zw. Anfrage und Antwort.
0x51 -> 0xD1
You are right 😅




#### HardWareConfig | 0x03

<details><summary>traces 1</summary>
<p>

```
22:02:09.582 > Fetch inverter: 112172615582
22:02:09.583 > 
22:02:09.583 >  >>> sendCommand: HardWareConfig | 0x03 | 3
22:02:09.588 > 
22:02:09.588 > sendEsbPacket
22:02:09.588 > TX 15 72 61 55 82 78 56 34 11 80 03 00 62 E8 31 41 00 00 00 00 00 00 00 00 8F C1 ED 
22:02:09.643 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 01 00 01 10 10 10 15 02 00 10 10 00 00 27 10 00 B0 15 
22:02:09.678 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 02 00 01 A7 F0 3D 46 66 66 3E 66 29 5F 3B 4B 33 9C 4B 
22:02:09.740 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 03 3C 22 D7 0A 3C A3 B3 68 3E 2A F8 38 3D 42 00 00 BA 
22:02:09.794 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 04 40 60 00 00 40 C0 66 66 3F A6 CC CD 41 2C EB 85 AA 
22:02:09.835 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 05 3F 91 00 00 42 3C 00 00 43 11 00 00 43 E1 00 00 B0 
22:02:09.897 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 06 43 66 00 00 43 52 7A E1 3F 74 00 00 41 80 00 00 B6 
22:02:09.933 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 07 42 70 00 00 41 B0 00 00 42 70 00 00 41 38 F5 C3 2C 
22:02:09.992 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 88 3F 88 00 00 42 B4 5C 29 3E 0F 00 00 42 BE 44 FE 5E 
22:02:10.634 > RX Period End
22:02:10.634 > Middle missing
22:02:10.634 > Request retransmit: 5
22:02:10.637 > TX 15 72 61 55 82 78 56 34 11 85 5F 
22:02:10.687 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 05 3F 91 00 00 42 3C 00 00 43 11 00 00 43 E1 00 00 B0 
22:02:10.725 > RX Period End
22:02:10.726 > Middle missing
22:02:10.726 > Request retransmit: 5
22:02:10.728 > TX 15 72 61 55 82 78 56 34 11 85 5F 
22:02:10.774 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 05 3F 91 00 00 42 3C 00 00 43 11 00 00 43 E1 00 00 B0 
22:02:10.817 > RX Period End
22:02:10.817 > Middle missing
```
</p>
</details>


Hier war es anscheinend nicht möglich eine erfolgreiche Nachricht vom WR zu erhalten. Hast du es öfters probiert?
nein, nur einmal
Ok danke. :) ich versuche gerade was daraus zu lesen.

<details><summary>traces 2</summary>
<p>

```
22:49:42.341 > Fetch inverter: 112172615582
22:49:42.341 > 
22:49:42.341 >  >>> sendCommand: HardWareConfig | 0x03 | 3
22:49:42.346 > 
22:49:42.346 > sendEsbPacket
22:49:42.346 > TX 15 72 61 55 82 78 56 34 11 80 03 00 62 E8 3C 66 00 00 00 00 00 00 00 00 84 EF E2 
22:49:42.414 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 01 00 01 10 10 10 15 02 00 10 10 00 00 27 10 00 B0 15 
22:49:42.453 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 02 00 01 A7 F0 3D 46 66 66 3E 66 29 5F 3B 4B 33 9C 4B 
22:49:42.494 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 03 3C 22 D7 0A 3C A3 B3 68 3E 2A F8 38 3D 42 00 00 BA 
22:49:42.531 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 04 40 60 00 00 40 C0 66 66 3F A6 CC CD 41 2C EB 85 AA 
22:49:42.590 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 05 3F 91 00 00 42 3C 00 00 43 11 00 00 43 E1 00 00 B0 
22:49:42.647 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 06 43 66 00 00 43 52 7A E1 3F 74 00 00 41 80 00 00 B6 
22:49:42.687 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 07 42 70 00 00 41 B0 00 00 42 70 00 00 41 38 F5 C3 2C 
22:49:42.747 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 88 3F 88 00 00 42 B4 5C 29 3E 0F 00 00 42 BE 44 FE 5E 
22:49:45.392 > RX Period End
22:49:45.393 > Middle missing
22:49:45.393 > Request retransmit: 5
22:49:45.395 > TX 15 72 61 55 82 78 56 34 11 85 5F 
22:49:45.441 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 05 3F 91 00 00 42 3C 00 00 43 11 00 00 43 E1 00 00 B0 
22:49:45.484 > RX Period End
22:49:45.484 > Middle missing
22:49:45.484 > Request retransmit: 5
22:49:45.487 > TX 15 72 61 55 82 78 56 34 11 85 5F 
22:49:45.575 > RX Period End
22:49:45.575 > Middle missing
22:49:45.575 > Request retransmit: 5
22:49:45.578 > TX 15 72 61 55 82 78 56 34 11 85 5F 
22:49:45.615 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 05 3F 91 00 00 42 3C 00 00 43 11 00 00 43 E1 00 00 B0 
22:49:45.666 > RX Period End
22:49:45.666 > Middle missing
22:49:45.666 > Request retransmit: 5
22:49:45.669 > TX 15 72 61 55 82 78 56 34 11 85 5F 
22:49:45.703 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 05 3F 91 00 00 42 3C 00 00 43 11 00 00 43 E1 00 00 B0 
22:49:45.757 > RX Period End
22:49:45.757 > Middle missing
22:49:45.757 > Request retransmit: 5
22:49:45.760 > TX 15 72 61 55 82 78 56 34 11 85 5F 
22:49:45.848 > RX Period End
22:49:45.848 > Middle missing
22:49:45.848 > Retransmit timeout
```
</p>
</details>

Hmm 🤔
Die Ahoy DTU hat aktuell ein Limit für max. 5 Antwort Pakete im Source Code, daher ist nach dem 5ten empfangenen Paket Schluss.
@klahus1 hat aber im ersten Anlauf bereits alle 8 Pakete mitgeloggt.


Für die HardWareConfig 0x03 ist der Parser UsartNrf3_Process_DevInform_SystemConfig nicht im DTU-Pro Source code.
```
TX 15 72615582 78563411 80 0300 62E83141 0000 00000000 0000 8FC1 ED    HardWareConfig 0x03
RX 95 72615582 72615582 01 0001 1010 1015 0200 1010 0000 2710 00B0 15 
RX 95 72615582 72615582 02 0001 A7F0 3D46 6666 3E66 295F 3B4B 339C 4B 
RX 95 72615582 72615582 03 3C22 D70A 3CA3 B368 3E2A F838 3D42 0000 BA 
RX 95 72615582 72615582 04 4060 0000 40C0 6666 3FA6 CCCD 412C EB85 AA 
RX 95 72615582 72615582 05 3F91 0000 423C 0000 4311 0000 43E1 0000 B0 
RX 95 72615582 72615582 06 4366 0000 4352 7AE1 3F74 0000 4180 0000 B6 
RX 95 72615582 72615582 07 4270 0000 41B0 0000 4270 0000 4138 F5C3 2C 
RX 95 72615582 72615582 88 3F88 0000 42B4 5C29 3E0F 0000 42BE 44FE 5E  UsartNrf3_Process_DevInform_SystemConfig()
```


#### SimpleCalibrationPara | 0x04

<details><summary>traces</summary>
<p>

```
22:53:57.406 > Fetch inverter: 112172615582
22:53:57.406 > 
22:53:57.406 >  >>> sendCommand: SimpleCalibrationPara | 0x04 | 4
22:53:57.412 > 
22:53:57.412 > sendEsbPacket
22:53:57.414 > TX 15 72 61 55 82 78 56 34 11 80 04 00 62 E8 3D 65 00 00 00 00 00 00 00 00 76 AC 56 
22:54:00.457 > RX Period End
22:54:00.457 > All missing
22:54:00.457 > Nothing received, resend whole request
22:54:00.463 > TX 15 72 61 55 82 78 56 34 11 80 04 00 62 E8 3D 65 00 00 00 00 00 00 00 00 76 AC 56 
22:54:00.517 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 81 00 01 03 E9 03 EE 03 EB FF EC 65 9D 11 
22:54:03.509 > RX Period End
22:54:03.509 > Success
```
</p>
</details>

Auch die Funktion UsartNrf3_Process_DevInform_Calibration() ist nicht im Source Code enthalten.
Es bleibt also auch die SimpleCalibrationPara Antwort zu interpretieren.

```
TX 15 72615582 78563411 80 0400 62E83D65 0000 00000000 0000 76AC 56    SimpleCalibrationPara | 0x04
RX 95 72615582 72615582 81 0001 03E9 03EE 03EB FFEC 659D 11            UsartNrf3_Process_DevInform_Calibration()
                           ^^^^--------------------------------------- 
                                ^^^^---------------------------------- 
                                     ^^^^----------------------------- 
                                          ^^^^------------------------ 
                                               ^^^^------------------- 
```

#### SystemConfigPara | 0x05

<details><summary>traces</summary>
<p>

Damit setze ich aktuell das Limit:

```
11:25:28.070 > Limit Non-Persistent: 98 %
11:25:28.070 > TX Channel: 61 --> 51 71 60 35 46 78 56 34 12 81 0B 00 03 D4 00 01 DC 80 3B 
11:25:28.130 > RX D1 71 60 35 46 71 60 35 46 81 00 00 0B 00 14 07 48 
11:25:30.103 > RX Period End
11:25:30.103 > Success
```

und das ist SytemConfigPara:

```
11:25:37.358 > TX Channel: 61 --> 15 71 60 35 46 78 56 34 12 80 05 00 63 30 1E 8B 00 00 00 00 00 00 00 00 16 A7 8D 
11:25:37.416 > RX 95 71 60 35 46 71 60 35 46 81 00 01 03 D4 00 00 03 E8 FF FF FF FF 01 68 2D 38 55 
11:25:37.596 > RX Period End
11:25:37.596 > Success
```
</p>
</details>

03 D4 = 98.0 % und in der SystemConfigPara steht auch 03 D4 gefolgt von 03 E8 = 100.0 %
Im ersten sind es 98%. also 03 D4... im 2. ist es auch 03 D4 (es ist das 3. und 4. Byte der Antwort)

Für die MI-Modelle wurde auch eine längere Zeit gemessen, bis das neue Limit überhaupt erreicht wird und greift.
Obwohl der SystemConfigPara m.E. dem Namen nach eigentlich den Soll-Zustand abbilden sollte.

Wenn man das SystemConfigPara zu schnell nach dem ActivePowerLimit schickt bekommt man im EventLog neue Einträge

Das oben sind 10 Sekunden Unterschied, heißt also Du musst 15-20 Sekunden warten oder das waren mehrere Versuche ?
Das interessante ist, ich bekomme teilweise 5 Sek nach ActivePowerLimit setzen schon eine Antwort aber erhalte dann eben Log Einträge. 
Bei 5 Min Differenz habe ich keine Log Einträge. Während der 5min kann ich problemlos die Stats lesen.

Der SystemConfigPara Kommando ist im original DTU Pro Source Code leider nur in Ansätzen implementiert. 
So fehlt u.a. die dafür vorgesehene UsartNrf3_Process_DevInform_SystemConfig() Methode.
Diese wird übrigens auch für HardWareConfig vorgesehen, aber das ist halt auch nur ein Kommentar / Stub.


### Wie kann man den Device Status prüfen

#### RealTimeRunData_Debug | 0x0B


```text
7E 15 81101507 81101507 80 0B00 62D806FB 0000 259C 00000000 2C1A 56 7F
^^--------------------------------------------------------------------- SOF Start of Frame 0x7E
   ^^------------------------------------------------------------------ MainCmd 0x15 REQ_ARW_DAT_ALL
      ^^^^^^^^--------------------------------------------------------- WR Serial ID
               ^^^^^^^^------------------------------------------------ DTU Serial ID
               ^^^^^^^^--------------------- DTU Serial ID wird vom NRF24 überschrieben, da initial vom Treiber gesetzt
                        ^^--------------------------------------------- MultiFrameID 0x80 = SingleFrame
                           ^^------------------------------------------ SubCmd bzw. DataType: 0x0B = RealTimeRunData_Debug, 0x0C RealTimeRunData_Reality
                             ^^---------------------------------------- rev Protocol Revision ?
                           ^^^^---------------------------------------- Control Mode ? immer zwei Byte im Gen3 Protokoll
                                ^^^^^^^^------------------------------- UNIX timestamp 62BE1CE0 -> 2022-07-01 00:00:00
                                         ^^^^-------------------------- Gap always 0x0000
                                              ^^^^--------------------- 0x0000, nur bei AlarmData: WarnSerNub (Warning Serial Number)
                                                                         // User data: the latest alarm serial number received on the same day
                                                   ^^^^^^^^------------ Password always 0x00000000
                                                            ^^^^------- CRC16 / CRC-Modbus über die UserData, excl. Frame ID!
                                                            ^^^^------- CRC16 / CRC-Modbus über die Daten, nach und excl. Frame ID!
                                                                 ^^---- CRC8
                                                                    ^^- EOF End of Frame 0x7F
```

Die Funktion UsartNrf3_Process_DevRunReality() ist etwas komplexer, je nach Inverter Typ
* Inverter_HM_OneToFour
  diese Kondition ist etwas verwirrend da hier teilweise der selbe Wert zweimal gelesen und z.B. sowohl in PV1&PV2 oder PV3&PV4 Voltage geschrieben wird. 
* Inverter_HM_OneToTwo
* Inverter_HM_OneToOne
* Inverter_Pro
* >= Inverter_Pro


#### RealTimeRunData_Reality | 0x0C

<details><summary>traces</summary>
<p>

```
22:08:29.683 > Fetch inverter: 112172615582
22:08:29.683 > 
22:08:29.683 >  >>> sendCommand: RealTimeRunData_Reality | 0x0C | 12
22:08:29.689 > 
22:08:29.689 > sendEsbPacket
22:08:29.691 > TX 15 72 61 55 82 78 56 34 11 80 0C 00 62 E8 32 BD 00 00 00 00 00 00 00 00 8B 6F B7 
22:08:29.754 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 01 00 01 01 06 01 2F 03 1C 00 02 D4 A3 0D 14 08 EB 2C 
22:08:29.768 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 82 13 86 02 F8 00 01 00 22 03 E8 00 B9 15 94 90 00 18 
22:08:30.736 > RX Period End
22:08:30.737 > Success
```
</p>
</details>

Die Funktion UsartNrf3_Process_DevRunReality() ist etwas komplexer, je nach Inverter Typ
* Inverter_HM_OneToFour
  diese Kondition ist etwas verwirrend da hier teilweise der selbe Wert zweimal gelesen und z.B. sowohl in PV1&PV2 oder PV3&PV4 Voltage geschrieben wird. 
* Inverter_HM_OneToTwo
* Inverter_HM_OneToOne
* Inverter_Pro
* >= Inverter_Pro

Bei dem o.g. Inverter 1121 handelt es sich also um einen Inverter_HM_OneToOne

```
TX 15 72615582 78563411 80 0C00 62E832BD 0000 00000000 0000 8B6F B7    RealTimeRunData_Reality 0x0C
RX 95 72615582 72615582 01 0001 0106 012F 031C 0002 D4A3 0D14 08EB 2C  UsartNrf3_Process_DevRunReality()
                           ^^^^--------------------------------------- DataVer Data version
                                ^^^^---------------------------------- PVVol PV1 voltage
                                     ^^^^----------------------------- PVCur PV1 current
                                          ^^^^------------------------ PVPower PV1 power
                                               ^^^^------------------- HistoryEnergyH PV1 Historical cumulative power generation 
                                                    ^^^^-------------- HistoryEnergyL
                                                         ^^^^--------- DailyEnergy
                                                              ^^^^---- GridVol AC voltage
RX 95 72615582 72615582 82 1386 02F8 0001 0022 03E8 00B9 1594 9000 18  
                           ^^^^--------------------------------------- Freque AC frequency
                                ^^^^---------------------------------- GridActivePower AC active power
                                     ^^^^----------------------------- GridReactivePower Reactive power
                                          ^^^^------------------------ GridCurrent AC current
                                               ^^^^------------------- PowerFactor Power factor
                                                    ^^^^-------------- Temper temperature
                                                         ^^^^--------- DataAarnNub 
```

//If the total is greater than 20, store the alarms in the alarm pool first
if(RealAlarmDataNO + DataAarnNub - WarnSerNub[PortNO] >= 20)

//If the number of alarms for a single micro-inverse is greater than 20, subcontracting processing is required
if(DataAarnNub - WarnSerNub[PortNO] > 20)



### Wie sieht das Device Info Kommando Alarm Data 0x11 / Alarm Update 0x12 aus ?

REQ_ARW_DAT_ALL `0x15` mit SubCmd: AlarmData = 17, // `0x11`

suche mal nach `NET_ALARM_DATA` / `NET_ALARM_UPDATE` bzw. dem anderen `AlarmUpdate`
das findet sich nicht überall als Substring wie `AlarmData`.

```text
15 74403329 78563412 80 1100 627b69fe 0000 0000 00000000 47d7 bc
```

```text
15 74403329 78563412 80 1100 62D80183 0000 0000 00000000 0765 FE --- AlarmData 0x11
15 74403329 78563412 80 1200 62D80183 0000 0000 00000000 FFC4 2A --- AlarmUpdate 0x12
15 74403329 78563412 80 1E00 62D80183 0000 0000 00000000 086A 0E --- GetSelfCheckState 0x1E
^^------------------------------------------------------------------ MainCmd 0x15 REQ_ARW_DAT_ALL
   ^^^^^^^^--------------------------------------------------------- WR Serial ID
            ^^^^^^^^------------------------------------------------ DTU Serial ID
                     ^^--------------------------------------------- MultiFrameID 0x80
                        ^^------------------------------------------ SubCmd bzw. DataType: 0x11 = AlarmData, 0x12 AlarmUpdate
                          ^^---------------------------------------- rev Protocol Revision ?
                             ^^^^^^^^------------------------------- UNIX timestamp 62BE1CE0 -> 2022-07-01 00:00:00
                                      ^^^^-------------------------- Gap always 0x0000
                                           ^^^^--------------------- 0x0000, nur bei AlarmData: WarnSerNub (Warning Serial Number)  
                                                ^^^^^^^^------------ Password always 0x0000
                                                         ^^^^------- CRC16 / CRC-Modbus über die UserData, excl. Frame ID!
                                                              ^^---- CRC8
```

`0x80` ist die MultiFrameID für SingleFrame Nachrichten !

Dann kommt das SubCmd `0x11` bzw. in `UsartNrf3_Send_PackPollMultiDataCommand()` wird das als DataType `0x11` und `0x00` (rev = Protokoll Revision/Version) bezeichnet (zusammen zwei Byte) und weiter übergeben bzw. gleichzeitig als `CurRecSendPackageDataType` gesetzt.
```c
    temp_dat[9] = 0x80;//Multi-frame identification
    temp_dat[10] = DataType;//User data: data type
    CurRecSendPackageDataType = DataType;//The currently packaged data type
    temp_dat[11] = 0;//rev
```

Danach folgt der `Timestamp`,
```c
    temp_dat[12] = (u8)(time >> 24);
    temp_dat[13] = (u8)(time >> 16);
    temp_dat[14] = (u8)(time >> 8);
    temp_dat[15] = (u8)(time);
```

das `Gap` (zwei Byte, steht im Excel)
```c
    temp_dat[16] = Gap;//User data: data upload server interval
    temp_dat[17] = Gap >> 8;
```

und im Falle von `AlarmData` eine Unterscheidung:
```c
    if(DataType == AlarmData)
    {
        //        temp_dat[18] = (u8)((CurRealAlarmNum + 1) / 0xff);
        //        temp_dat[19] = (u8)((CurRealAlarmNum + 1) % 0xff);
        temp_dat[18] = (u8)((WarnSerNub[PortNO]) / 0xff);
        temp_dat[19] = (u8)((WarnSerNub[PortNO]) % 0xff);
    }
    else
    {
        memset((u8 *) & (temp_dat[18]), 0, 2);  // User data: the latest alarm serial number received on the same day
    }
```

Also zwei Bytes `0x00 00` um die letzte Alarm Serial Nummer zu abzufragen, bzw. die aktuelle Alarm Serial Number falls man schon welche kennt.
Dann noch das Password also `0x00000000` (vier Bytes alle 0).
```c
    memcpy((u8 *)(&temp_dat[20]), Password, 4); //User data: anti-theft password
```

Dann noch schnell die CRC-16 über die Daten nach der MultiFrameID drüber berechnet
```c
    for(i = 10; i < 24; i++)
    {
        if((i - 10) % 2 == 1)
        {
            TempCrc = (u16)(temp_dat[i - 1] << 8) | (temp_dat[i]);
            DatCrc =  CalcCRC16t(TempCrc, DatCrc);
        }
    }

    temp_dat[24] = (u8)(DatCrc >> 8);
    temp_dat[25] = (u8)(DatCrc);
```

und dann die CRC8 über alles.
```c
    temp_dat[26] = Get_crc_xor((u8 *)temp_dat, 26);
```

Danach wird dann anhand des `CurRecSendPackageDataType` die entsprechende Antwort in `UsartNrf3_Process_DevInform()` bzw. `UsartNrf3_Process_DevInform_Alarm()` oder `UsartNrf3_Process_DevInform_InformUpdate()` geparst.


Routine `UsartNrf3_Process_DevInform_Alarm()` wird verwendet um die o.a. Alarm Payload zu dekodieren.
Es werden immer in 12 byte zusammengefaßt, wobei die ersten beiden die Alarm Version number darstellen:

Fehlermeldungen in [HM-600 HM-800 Bedienungsanleitung](https://www.alpha-solar.info/media/Dokumente/Wechselrichter/Hoymiles%20HM/Deutsch/Bedienungsanleitungen/HM-600%20%20HM-800%20Bedienungsanleitung.pdf)

Alarmcode 129 deckt sich u.A. auch mit der Fehlertabelle in der 
Bedienungsanleitung vom HM-600. "Softwarefehlercode 129". Zufall?
Dann könnte der WR ja prinziepiell auch die anderen Alarmcodes senden. 
Dafür bräuchte es aber eine Art Session zwischen der DTU und dem WR. 
Weil ich habe noch keine unbekannten Pakete rein purzeln sehen, wenn ich 
z.B. das Netz abtrenne. Das müsste dann laut Anleitung 0x93/147 oder 
0x94/148 sein

So wie ich es verstehe, ergibt sich z.B. bei mir folgender zerlegter Block (Hand bearbeitet):

```text
W1   W2   W3   W4   W5   W6
B1 2  3 4  5 6  7 8 9 10 11 12
0001                             Hex    Dez
8001 0006 1698 1698 0000 0000 ; 1698 > 5784 /60 = 96 /60=1:36:xx ;          0x1698 = 02:36:24
8002 0007 4F16 4F16 FFFF FFDF ; 4F16 > 20246/60 = 337/60=5:37:xx ;          0x4F16 = 06:37:26
8002 0008 5CC9 5CC9 FFFF F261 ; 5CC9 > 23753/60 = 395/60=6:35:xx ; F2=242 ; 0x5CC9 = 07:35:53
8002 0009 5D0E 5D0E FFFF FFA7 ; 5D0E > 23822/60 = 397/60=6:37:xx ;          0x5D0E = 07:37:02
8002 000A 641D 641D FFFF F8F1 ; 641D > 25629/60 = 427/60=7:07:xx ; F8=248 ; 0x641D = 08:07:09
8002 000B 64DE 64DE FFFF FF3F ; 64DE > 25822/60 = 430/60=7:10:xx ;          0x64DE = 08:10:22
8002 000C 657D 657D FFFF FF61 ; 657D > 25981/60 = 433/60=7:13:xx ;          0x657D = 08:13:01
8002 000D 6679 6679 FFFF FF18 ; 6679 > 26233/60 = 437/60=7:17:xx ;          0x6679 = 08:17:13
8002 000E 754A 754A FFFF F12F ; 754A > 30026/60 = 500/60=8:00:xx ; F1=241 ; 0x754A = 09:20:26
34E7
```

a) Nur was sollen mir die Worte W1 bis W6 sagen ?
Ich habe gegen 12:41 Uhr mit der Aufzeichnung begonnen.
Der WR arbeitet aber schon sehr viel früher.
Also "Uptime" in der Zeile 8001 mit 1:36:xx kann nicht sein.

Es ist die Uhrzeit zu der das Event / der Alarm aufgetreten ist.
Hier sind alle Zeiten am selben Tag mit AM angegeben.

W1 = WCode
     Bit 14 und Bit 15 ergeben den RunCode[0] und RunCode[1]
     Bit 12 und Bit 13 ergeben AM und PM für AlarmStartTime und AlarmEndTime
W2 = WNum/WarnSerNub
W3 = AlarmStartTime
W4 = AlarmEndTime
W5 = AlarmData1
W6 = AlarmData2

b) Welches Wort/Byte (W1 bis W6/B1 bis B12) soll Bitte der Alarmcode 
sein?

AlarmCode ist das LowByte von W1

6.1 Fehlerbehebungsliste

<details><summary>Table Fehlerbehebungsliste</summary>
<p>

| Alarm Code | Alarmbezeichnung       | Vorschlag |
| ---------- | ---------------------- | -------------------------------------------------------------------------------- |
| 121        | Übertemperaturschutz.  | 1. Überprüfen Sie am Standort der Mikroumwechselrichterinstallation die Belüftung und Umgebungstemperatur. |
|            |                        | 2. Bei schlechter Belüftung oder Überschreitung der Temperaturgrenzwerte, verbessern Sie die Belüftung und Wärmeableitung. |
|            |                        | 3. Wenn sowohl die Belüftung als auch die Umgebungstemperatur den Vorgaben entsprechen, kontaktieren Sie bitte Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 125        | Parameterfehler der Netzkonfiguration | 1. Überprüfen Sie, ob die Netzkonfigurationsparameter korrekt sind und aktualisieren Sie sie erneut. |
|            |                        | 2. Wenn weiterhin ein Fehler vorliegt, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 126        | Softwarefehlercode 126 | 1. Wenn der Alarm ohne besonderen Anlass auftritt, der Mikrowechselrichter jedoch normal arbeitet, wird kein besonderer Eingriff benötigt. |
|            |                        | 2. Wenn der Alarm häufig auftritt und nicht behoben werden kann, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 127        | Firmwarefehler         | 1. Überprüfen Sie, ob die Firmware korrekt ist und aktualisieren Sie diese erneut. |
|            |                        | 2. Überprüfen Sie die Kommunikation zwischen DTU und dem Überwachungssystem von Hoymiles sowie die Kommunikation zwischen DTU und Mikrowechselrichter. |
|            |                        | 3. Wenn weiterhin ein Fehler vorliegt, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 128        | Softwarefehlercode 128 | 1. Wenn der Alarm ohne besonderen Anlass auftritt, der Mikrowechselrichter jedoch normal arbeitet, wird kein besonderer Eingriff benötigt. |
|            |                        | 2. Wenn der Alarm häufig auftritt und nicht behoben werden kann, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 129        | Softwarefehlercode 129 | 1. Wenn der Alarm ohne besonderen Anlass auftritt, der Mikrowechselrichter jedoch normal arbeitet, wird kein besonderer Eingriff benötigt. |
|            |                        | 2. Wenn der Alarm häufig auftritt und nicht behoben werden kann, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 130        | Offline                | 1. Bitte stellen Sie sicher, dass der Mikroumwechselrichter normal arbeitet. |
|            |                        | 2. Überprüfen Sie den Kommunikationszustand zwischen der DTU und demMonitoringsystem von Hoymiles, sowie die Kommunikation zwischen DTU und Mikrowechselrichter. Wenn die Kommunikation schlecht ist, versuchen Sie Verbesserungen anhand der weiter oben genannten Punkte zu erreichen. |
|            |                        | 3. Wenn der Alarm häufig auftritt und nicht behoben werden kann, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 141        | Netzüberspannung       | 1. Wenn der Alarm ohne besonderen Anlass auftritt, kann die Netzspannung vorübergehend zu hoch sein. Der Mikroumwechselrichter verbindet sich automatisch wieder mit dem Netz, sobald sich die Netzspannung normalisiert hat. |
|            |                        | 2. Wenn der Alarm häufig auftritt, überprüfen Sie, ob die Netzspannung am Anschlusspunkt innerhalb der erlaubten Grenzen liegt. Wenn nicht, kontaktieren Sie den örtlichen Netzbetreiber, oder adaptieren Sie mit Zustimmung des örtlichen Netzbetreibers die Grenzwerte über das Monitoringsystem von Hoymiles. |
| 142        | 10 Minuten-Mittelwert  |  1. Wenn der Alarm ohne besonderen Anlass auftritt, kann die Netzspannung vorübergehend zu hoch sein. Der Mikroumwechselrichter verbindet sich automatisch wieder mit dem Netz, sobald sich die Netzspannung normalisiert hat. |
|            | Netzüberspannung       | 2. Wenn der Alarm häufig auftritt, überprüfen Sie, ob die Netzspannung am Anschlusspunkt innerhalb der erlaubten Grenzen liegt. Wenn nicht, kontaktieren Sie den örtlichen Netzbetreiber, oder adaptieren Sie mit Zustimmung des örtlichen Netzbetreibers die Grenzwerte über das Monitoringsystem von Hoymiles. |
| 143        | Netzunterspannung      | 1. Wenn der Alarm ohne besonderen Anlass auftritt, kann die Netzspannung vorübergehend zu niedrig sein. Der Mikroumwechselrichter verbindet sich automatisch wieder mit dem Netz, sobald sich die Netzspannung normalisiert hat. |
|            |                        | 2. Wenn der Alarm häufig auftritt, überprüfen Sie, ob die Netzspannung am Anschlusspunkt innerhalb der erlaubten Grenzen liegt. Wenn nicht, kontaktieren Sie den örtlichen Netzbetreiber, oder adaptieren Sie mit Zustimmung des örtlichen Netzbetreibers die Grenzwerte über das Monitoringsystem von Hoymiles. |
|            |                        | 3. Wenn der Fehler weiterhin auftritt, überprüfen Sie den Sicherungsautomat oder die AC-Verdrahtung. |
| 144        | Netzüberfrequenz       | 1. Wenn der Alarm ohne besonderen Anlass auftritt, kann die Netzfrequenz vorübergehend zu hoch sein. Der Mikroumwechselrichter verbindet sich automatisch wieder mit dem Netz, sobald sich die Netzfrequenz normalisiert hat. |
|            |                        | 2. Wenn der Alarm häufig auftritt, überprüfen Sie, ob die Netzfrequenz am Anschlusspunkt innerhalb der erlaubten Grenzen liegt. Wenn nicht, kontaktieren Sie den örtlichen Netzbetreiber, oder adaptieren Sie mit Zustimmung des örtlichen Netzbetreibers die Grenzwerte über das Monitoringsystem von Hoymiles. |
| 145        | Netzunterfrequenz      | 1. Wenn der Alarm ohne besonderen Anlass auftritt, kann die Netzfrequenz vorübergehend zu niedrig sein. Der Mikroumwechselrichter verbindet sich automatisch wieder mit dem Netz, sobald sich die Netzfrequenz normalisiert hat. |
|            |                        | 2. Wenn der Alarm häufig auftritt, überprüfen Sie, ob die Netzfrequenz am Anschlusspunkt innerhalb der erlaubten Grenzen liegt. Wenn nicht, kontaktieren Sie den örtlichen Netzbetreiber, oder adaptieren Sie mit Zustimmung des örtlichen Netzbetreibers die Grenzwerte über das Monitoringsystem von Hoymiles. |
| 146        | Schnelle Wechselrate der Netzfrequenz | 1. Wenn der Alarm ohne besonderen Anlass auftritt, kann die sich Netzfrequenz vorübergehendzu häufig/schnell ändern. Der Mikroumwechselrichter verbindet sich automatisch wieder mit dem Netz, sobald sich die Netzfrequenz normalisiert hat. |
|            |                        | 2. Wenn der Alarm häufig auftritt, überprüfen Sie, ob die Netzfrequenz am Anschlusspunkt innerhalb der erlaubten Grenzen liegt. Wenn nicht, kontaktieren Sie den örtlichen Netzbetreiber, oder adaptieren Sie mit Zustimmung des örtlichen Netzbetreibers die Grenzwerte (Netzfrequenzwechselrate) über das Monitoringsystem von Hoymiles. |
| 147        | Stromnetzausfall       | Bitte überprüfen Sie, ob ein Netzstromausfall vorliegt. |
| 148        | Netzabtrennung         | Bitte überprüfen Sie, ob der Sicherungsautomat und die AC-Verdrahtung in Ordnung sind. |
| 149        | Inselbetrieb festgestellt | 1. Wenn der Alarm ohne besonderen Anlass auftritt, kann dies an untypischen Netzverhältnissen liegen. Der Mikroumwechselrichter verbindet sich automatisch wieder mit dem Netz, sobald sich der Netzzustand normalisiert hat. |
|            |                        | 2. Wenn der Alarm häufig an allen Mikrowechselrichter Ihrer Anlage auftritt, kontaktieren Sie den örtlichen Netzbetreiber, um zu überprüfen, ob ein Inselbetrieb vorliegt. |
|            |                        | 3. Wenn der Alarm weiterhin besteht, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 205        | Überspannung am DC-Eingangsport 1 | 1. Bitte stellen Sie sicher, dass die Leerlaufspannung des PV-Moduls geringer oder gleich der maximal erlaubten Eingangsspannung ist. |
|            |                        | 2. Wenn die Leerlaufspannung des PV-Moduls innerhalb des normalen Bereichs liegt, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 206        | Überspannung am DC-Eingangsport 2 | 1. Bitte stellen Sie sicher, dass die Leerlaufspannung des PV-Moduls geringer oder gleich der maximal erlaubten Eingangsspannung ist. |
|            |                        | 2. Wenn die Leerlaufspannung des PV-Moduls innerhalb des normalen Bereichs liegt, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 207        | Unterspannung am DC-Eingangsport 1 | 1. Bitte stellen Sie sicher, dass die Leerlaufspannung des PV-Moduls höher oder gleich der minimalen Eingangsspannung ist. |
|            |                        | 2. Wenn die Leerlaufspannung des PV-Moduls innerhalb des normalen Bereichs liegt, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 208        | Unterspannung am DC-Eingangsport 2 | 1. Bitte stellen Sie sicher, dass die Leerlaufspannung des PV-Moduls höher oder gleich der minimalen Eingangsspannung ist. |
|            |                        | 2. Wenn die Leerlaufspannung des PV-Moduls innerhalb des normalen Bereichs liegt, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 209        | Fehler beim DC-Eingang 1 | 1. Bitte prüfen Sie, ob das PV-Modul an den Wechselrichter angeschlossen ist. Wenn das PV-Modul angeschlossen ist, überprüfen Sie bitte die DC-Kabelverbindungen zwischen Anschluss und PV-Modul. |
| 210        | Fehler beim DC-Eingang 2 | 1. Bitte prüfen Sie, ob das PV-Modul an den Wechselrichter angeschlossen ist. Wenn das PV-Modul angeschlossen ist, überprüfen Sie bitte die DC-Kabelverbindungen zwischen Anschluss und PV-Modul. |
| 301        | Hardwarefehlercode 301 | 1. Wenn der Alarm ausversehen auftritt, der Mikrowechselrichter jedoch normal arbeitet, wird kein besonderer Eingriff benötigt. |
|            |                        | 2. Wenn der Alarm häufig auftritt und nicht behoben werden kann, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 302        | Hardwarefehlercode 302 | 1. Wenn der Alarm ohne besonderen Anlass auftritt, der Mikrowechselrichter jedoch normal arbeitet, wird kein besonderer Eingriff benötigt. |
|            |                        | 2. Wenn der Alarm häufig auftritt und nicht behoben werden kann, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 303        | Hardwarefehlercode 303 | 1. Wenn der Alarm ohne besonderen Anlass auftritt, der Mikrowechselrichter jedoch normal arbeitet, wird kein besonderer Eingriff benötigt. |
|            |                        | 2. Wenn der Alarm häufig auftritt und nicht behoben werden kann, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 304        | Hardwarefehlercode 304 | 1. Wenn der Alarm ohne besonderen Anlass auftritt, der Mikrowechselrichter jedoch normal arbeitet, wird kein besonderer Eingriff benötigt. |
|            |                        | 2. Wenn der Alarm häufig auftritt und nicht behoben werden kann, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 305        | Hardwarefehlercode 305 | 1. Wenn der Alarm ohne besonderen Anlass auftritt, der Mikrowechselrichter jedoch normal arbeitet, wird kein besonderer Eingriff benötigt. |
|            |                        | 2. Wenn der Alarm häufig auftritt und nicht behoben werden kann, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 306        | Hardwarefehlercode 306 | 1. Wenn der Alarm ohne besonderen Anlass auftritt, der Mikrowechselrichter jedoch normal arbeitet, wird kein besonderer Eingriff benötigt. |
|            |                        | 2. Wenn der Alarm häufig auftritt und nicht behoben werden kann, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 307        | Hardwarefehlercode 307 | 1. Wenn der Alarm ohne besonderen Anlass auftritt, der Mikrowechselrichter jedoch normal arbeitet, wird kein besonderer Eingriff benötigt. |
|            |                        | 2. Wenn der Alarm häufig auftritt und nicht behoben werden kann, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
| 308        | Hardwarefehlercode 308 | 1. Wenn der Alarm ohne besonderen Anlass auftritt, der Mikrowechselrichter jedoch normal arbeitet, wird kein besonderer Eingriff benötigt. |
|            |                        | 2. Wenn der Alarm häufig auftritt und nicht behoben werden kann, kontaktieren Sie Ihren Händler oder die technische Unterstützung von Hoymiles. |
</p>
</details>

I have found alarm_codes 121..314 in the HM-1600 documentation you mentioned on the forum:
Chapter 6. Troubleshooting, 6.1 Troubleshooting List

However I could not find the alarm_codes 5041..5200, these are probably elaborate guesses based on first hand experience / results ?
Or is 0x50XY another prefix like the 0x8Y we have seen with the paket numbering maybe for some "channels" / MPPT ports ?

Found it under MI-600, MI-700 and MI-800 manual

6.1 Troubleshooting List (SN: 1042xxxxxxxx)
  Error Codes: 121 - 308

6.2 Troubleshooting List (SN: 1040xxxxxxxx, 1041xxxxxxxx)
  Error Codes: 130 (Offline), 5041 - 9000 *sic*

So the error codes are Device Dependent, but there seem to be little / no differences in the overlapping codes.

The codes above 1000 can be found in the MI-Series user manuals. Just google a bit. There are lots of different models out there. Compare all user manuals and you will find, all seem to have the same codes. Depending on their hardware layout of course, but the codes don't seem to overlap a single time. If you merge all that information in a single table you likely end up with a similar result. Is this list complete? I don't think so. Especially because I could not find any hint on codes 1 and 2. They where just guessed, based on real observation.

Gerade das hier gefunden zur Analyse von WR/DTU Fehlern https://www.hoymiles.com/wp-content/uploads/2021/07/Failure-process-for-common-fault.pdf


```c
            // MI Error Codes
            5041: 'Error code-04 Port 1', // 0x13B1
            5042: 'Error code-04 Port 2', // 0x13B2
            5043: 'Error code-04 Port 3', // 0x13B3
            5044: 'Error code-04 Port 4', // 0x13B4
            5051: 'PV Input 1 Overvoltage/Undervoltage', // 0x13BB
            5052: 'PV Input 2 Overvoltage/Undervoltage', // 0x13BC
            5053: 'PV Input 3 Overvoltage/Undervoltage', // 0x13BD
            5054: 'PV Input 4 Overvoltage/Undervoltage', // 0x13BE
            5060: 'Abnormal bias', // 0x13C4
            5070: 'Over temperature protection', // 0x13CE
            5080: 'Grid Overvoltage/Undervoltage', // 0x13D8
            5090: 'Grid Overfrequency/Underfrequency', // 0x13E2
            5100: 'Island detected', // 0x13EC
            5120: 'EEPROM reading and writing error', // 0x1400
            5150: '10 min value grid overvoltage', // 0x141E
            5200: 'Firmware error', // 0x1450
            8310: 'Shut down', // 0x2076
            9000: 'Microinverter is suspected of being stolen' // 0x2328
```

I especially like 9000: 'Microinverter is suspected of being stolen' :rofl:

```text
00 01 
80 01 00 06 30 62 30 62 00 00 00 00 // 0x80 = AM,AM, 0x3062 = 04:26:26
00 d4 00 07 30 6a 00 00 00 00 00 00 // 0x00 = AM,AM, 0x306A = 04:26:34, 0xD4 = 212 Port 4 no input
b0 02 00 48 4c f7 4c f7 00 00 00 05 // 0xB0 = PM,PM, 0x4CF7 = 06:28:23 + 12:00:00 = 18:28:23
b0 02 00 49 55 da 55 da ff ff ff fb // 0xB0 = PM,PM, 0x55DA = 07:06:18 + 12:00:00 = 19:06:18
b0 02 00 4a 55 ed 55 ed 00 00 00 05 // 0xB0 = PM,PM, 0x55ED = 07:06:37 + 12:00:00 = 19:06:37
b0 02 00 4b 56 72 56 72 ff ff ff fb // 0xB0 = PM,PM, 0x5672 = 07:08:50 + 12:00:00 = 19:08:50
b0 02 00 4c 56 72 56 72 00 00 00 06 // 0xB0 = PM,PM, 0x5672 = 07:08:50 + 12:00:00 = 19:08:50
b0 02 00 4d 56 79 56 79 ff ff ff fb // 0xB0 = PM,PM, 0x5679 = 07:08:57 + 12:00:00 = 19:08:57
b0 02 00 4e 56 82 56 82 00 00 00 05 // 0xB0 = PM,PM, 0x5682 = 07:09:06 + 12:00:00 = 19:09:06
b0 02 00 4f 56 e7 56 e7 ff ff ff fb // 0xB0 = PM,PM, 0x56E7 = 07:10:47 + 12:00:00 = 19:10:47
b0 02 00 50 56 f3 56 f3 00 00 00 05 // 0xB0 = PM,PM, 0x56F3 = 07:10:59 + 12:00:00 = 19:10:59
b0 02 00 51 57 1d 57 1d ff ff ff fb // 0xB0 = PM,PM, 0x571D = 07:11:41 + 12:00:00 = 19:11:41
b0 02 00 52 57 23 57 23 00 00 00 05 // 0xB0 = PM,PM, 0x5723 = 07:11:47 + 12:00:00 = 19:11:47
b0 02 00 53 57 4f 57 4f ff ff ff fb // 0xB0 = PM,PM, 0x574F = 07:12:31 + 12:00:00 = 19:12:31
b0 02 00 54 57 51 57 51 00 00 00 05 // 0xB0 = PM,PM, 0x5751 = 07:12:33 + 12:00:00 = 19:12:33
05 ab
```

80 0B00 623B5E4B 0000 000B 00000000 2F87 2B6A BD BD6A 1


```text
00 01 
80 01 00 01 64 42 64 42 00 00 00 00 
00 d1 00 04 64 4a 00 00 00 00 00 00 // 0xD1 = 209 Fehler beim DC-Eingang 1
00 d2 00 05 64 4a 00 00 00 00 00 00 // 0xD2 = 210 Fehler beim DC-Eingang 2
00 cf 00 06 65 76 00 00 00 00 00 dc // 0xCF = 207 Unterspannung am DC-Eingangsport 1
80 02 00 09 6a b3 6a b3 ff ff ff f6 
80 02 00 0a 6a b8 6a b8 ff ff ff fb 
80 02 00 0b 6b cf 6b cf ff ff fe e9 
40 8f 00 0c 64 4a 6c 19 00 03 07 a3 // 0x8F = 143 Netzunterspannung
40 93 00 0d 64 4a 6c 19 00 00 00 00 // 0x93 = 147 Stromnetzausfall
80 02 00 0e 6c ac 6c ac ff ff ff 23 
80 02 00 0f 6c b1 6c b1 ff ff ff fb 
80 02 00 10 6c b8 6c b8 ff ff ff f9 
80 02 00 11 6c be 6c be ff ff ff fa 
80 02 00 12 6c c3 6c c3 ff ff ff fb 
80 02 00 13 6c ca 6c ca ff ff ff f9 
2f 89
```

```text
00 01 <-- Alarm Version number
80 01 00 01 62 26 62 26 00 00 00 00 // 0x6226 = 07:58:46; 0x01 =
00 d1 00 04 62 2e 00 00 00 00 00 00 // 0x622E = 07:58:54; 0xD1 = 209 Fehler beim DC-Eingang 1
00 d2 00 05 62 2e 00 00 00 00 00 00 // 0x622E = 07:58:54; 0xD2 = 210 Fehler beim DC-Eingang 2
00 cf 00 06 63 5a 00 00 00 00 00 dc // 0x635A = 08:03:54; 0xCF = 207 Unterspannung am DC-Eingangsport 1
40 8f 00 0c 62 2e 69 fd 00 03 07 a3 // 0x622E = 07:58:54; 0x8F = 143 Netzunterspannung
40 93 00 0d 62 2e 69 fd 00 00 00 00 // 0x622E = 07:58:54; 0x93 = 147 Stromnetzausfall
80 02 00 22 6c a4 6c a4 ff ff ff fa // 0x6CA4 = 08:43:32; 0x02 = 
80 02 00 23 6c ab 6c ab ff ff ff f9
80 02 00 24 6c ec 6c ec ff ff ff bf
80 02 00 25 6c f1 6c f1 ff ff ff fb
80 02 00 26 6c fb 6c fb ff ff ff f6
80 02 00 27 6d 18 6d 18 ff ff ff e3
80 02 00 28 6d 22 6d 22 ff ff ff f6
80 02 00 29 6d 27 6d 27 ff ff ff fb
80 02 00 2a 6d 32 6d 32 ff ff ff f5
53 03 <-- CRC-16 / CRC-Modbux
|...| |...| |...| |...| |...| |...|
+2 +3 +4 +5 +6 +7 +8 +9 +10.. +12..
<WCode>     |     |     |     |
      <WNum>|     |     |     |
      <WarnSerNub>|     |     |
            <AlarmStartTime>  |
                  <AlarmEndTime> 
                        <AlarmData1> 
                              <AlarmData2>
```

AlarmId:
```c
            Alarm_Id[0]), (u8 *)MIMajor[PortNO].Property.Pre_Id, 2);
            Alarm_Id[2]), (u8 *)MIMajor[PortNO].Property.Id, 4);
```

WCode:
```c
            WCode = (u16)pProBuffer[i * 12 + 2] << 8 | pProBuffer[i * 12 + 3];
```

WNum:
```c
            WNum), &(pProBuffer[i * 12 + 4]), 2);
```

WarnSerNub:
```c
            WarnSerNub[PortNO] = (u16)pProBuffer[i * 12 + 4] << 8 | (u16)pProBuffer[i * 12 + 5];
```

WTime1=AlarmStartTime:
```c
            //Alarm start time
            AlarmTime = (u32)((u16)pProBuffer[i * 12 + 6] << 8) | ((u16)pProBuffer[i * 12 + 7]) + DateToSec(calendar); // AM
            AlarmTime = 12 * 60 * 60 + (u32)(((u16)pProBuffer[i * 12 + 6] << 8) | ((u16)pProBuffer[i * 12 + 7])) + DateToSec(calendar); // PM
```

WTime2=AlarmEndTime:
```c
            //Alarm end time
            AlarmTime = (u32)((u16)pProBuffer[i * 12 + 8] << 8) | ((u16)pProBuffer[i * 12 + 9]) + DateToSec(calendar); // AM
            AlarmTime = 12 * 60 * 60 + (u32)(((u16)pProBuffer[i * 12 + 8] << 8) | ((u16)pProBuffer[i * 12 + 9])) + DateToSec(calendar); // PM
```

AlarmData1:
```c
            Data1[0]), &(pProBuffer[i * 12 + 10]), 2);
```

AlarmData2:
```c
            Data2[0]), &(pProBuffer[i * 12 + 12]), 2);
```

Das was Jan-Jonas als `a_count` identifiziert hat ist in Wirklichkeit `WarnSerNub` bzw. das High byte davon ist auch `WNum`.

Das was in Deiner Ausgabe mit `0x4d02` als `19714` sec identifiziert wurde sind die Sekunden seit 0:00 bzw. 12:00 Uhr für den `AlarmStartTime/Wtime1` bzw. `AlarmEndeTime/WTime2`

```text
80 01 00 01 4d 02 4d 02 00 00 00 00: 
 uptime=5:28:34 a_count=1 opcode=128 a_code=1 a_text=Inverter start
 BBHHHHH: (128, 1, 1, 19714, 19714, 0, 0)
```

Die untere Ausgabe mit `19714` das ist also `5:28:34 h` eine normale Uhrzeit, `AM` da die u.a. `AlarmStart` und `AlarmEnde` AM/PM Bits `13 & 12` aus dem `WCode` = 0 sind.
Der WR kennt kein Datum, die DTU addiert hierzu das Datum dazu.
Dazu muss man jeweils das aktuelle Datum addieren, dann hat man einen echten Timestamp
Lediglich den Datumswechsel scheint der WR anhand der von der DTU gesendeten Timestamps zu machen.

```c
(WCode >> 14) & 0x03 : (0x8001 >>14) & 0x03 : (0x02) & 0x03 = 0x02 // bestimmt den sog. RunCode siehe unten
(WCode >> 13) & 0x01 : (0x8001 >>13) & 0x01 : (0x04) & 0x01 = 0x00 // 0x00 = AM, 0x01 = PM AlarmStart
(WCode >> 12) & 0x01 : (0x8001 >>12) & 0x01 : (0x08) & 0x01 = 0x00 // 0x00 = AM, 0x01 = PM AlarmEnde
```

Es wird offenbar immer das aktuelle Datum des Tages in Sekunden dazu gezählt 
und anhand des Bit 13 / 12 im `WCode` entschieden ob `AlarmStartTime` / `AlarmEndTime` vormittags oder nachmittags liegt/lag.

Aus Bit 14 & 15 des WCode wird noch ein sog. `Run_Status[0]` und `[1]` extrahiert.
Was auch immer das aussagt?
```c
WCode >> 14) & 0x03)) == 0)
  Run_Status[0] = 0x00;
  Run_Status[1] = 0x08;
WCode >> 14) & 0x03) == 1)
  Run_Status[0] = 0x00;
  Run_Status[1] = 0x03;
```

Was der `Run_Status` genau aussagt weiß man aktuell noch nicht oder?

Ach ja und `AlarmData1/Data1` und `AlarmData2/Data2` sind beide `0x0000`

WCode ist also `0x8001` und WNum = `0x80`

Für WCode `0x8001` sind die Bits also
```text
0x        8            0             0            1
15 14 13 12  11 10 09 08   07 06 05 04  03 02 01 00
 8  4  2  1   8  4  2  1    8  4  2  1   8  4  2  1    
 1  0  0  0   0  0  0  0    0  0  0  0   0  0  0  1
```

```text
00 D1 00 04 4D 0A 00 00 00 00 00 00: 
 uptime=5:28:42 a_count=4 opcode=0 a_code=209 a_text=Port 1 no input
 BBHHHHH: (0, 209, 4, 19722, 0, 0, 0)
```

Hier ist WCode `0x00D1`, also ist `((WCode >> 14) & 0x03)) == 0)` und somit `Run_Status[0] = 0x00;` und `Run_Status[1] = 0x08;`.
Die Uhrzeit stimmt, da auch Bit 12&13 0 sind, ist die `AlarmStartTime/Wtime1` AM.
Und die `WarnSerNub = 0x0004` und WNum = `0x00`

```text
40 8f 00 0c 4d 0a 54 d9 00 03 07 a3: 
 uptime=5:28:42 a_count=12 opcode=64 a_code=143 a_text=Grid undervoltage
 BBHHHHH: (64, 143, 12, 19722, 21721, 3, 1955)
```

Hier ist WCode `0x408f`, also ist `((WCode >> 14) & 0x03)) == 1)` und somit `Run_Status[0] = 0x00;` und `Run_Status[1] = 0x03;`.
Die Uhrzeit stimmt, da auch Bit 12&13 wieder 0 sind ist auch die `AlarmStartTime/Wtime1 0x4d0a` = 5:28:42h `AlarmEndTime/Wtime2 0x54d9` =6:02:01h beide AM.
Hier sind `AlarmData1/Data1 = 0x0003` und `AlarmData2/Data2 = 0x07a3`
Und die `WarnSerNub = 0x000c` und `WNum = 0x00`

```c
//CurAlarmState -- alarm state type
typedef enum
{
    InitState = 0,
    //There is a new alarm record
    HasNewAlarmRecord = 1,
    //There is a new wave recording alarm
    HasNewWaveRecord = 2,
    //No new alarm record
    HasNONewAlarmRecord = 3,
    //No new wave recording alarm
    HasNONewWaveRecord = 4,
    // Suspend the alarm
    AlarmInforUpdate_Server = 10,
    //APP state switch
    AlarmInforUpdate_App = 11,
} AlarmStateType;
extern volatile AlarmStateType CurAlarmState;
```


```c
typedef union
{
    struct
    {
        //dong 20200520
        u16 WCode;
        u8 Alarm_Id[6] ;
        u8 WNum[2];
        u8 WTime1[4];
        u8 WTime2[4];
        u8 Data1[2];
        u8 Data2[2];
    } Data;
    u8 DataMsg[22];
} AlarmDataType;
```


#### InternalData | 0x14

<details><summary>traces</summary>
<p>

```
22:06:44.659 > Fetch inverter: 112172615582
22:06:44.659 > 
22:06:44.659 >  >>> sendCommand: InternalData | 0x014 | 20
22:06:44.664 > 
22:06:44.664 > sendEsbPacket
22:06:44.664 > TX 15 72 61 55 82 78 56 34 11 80 14 00 62 E8 32 54 00 00 00 00 00 00 00 00 07 D4 71 
22:06:44.713 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 01 00 01 9B 8A 09 F7 08 09 FF FB 00 04 00 00 04 B5 CA 
22:06:44.750 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 82 01 4B 03 61 03 61 66 0A 31 
22:06:45.712 > RX Period End
22:06:45.713 > Success
```
</p>
</details>

```
TX 15 72615582 78563411 80 1400 62E83254 0000 00000000 0000 07D4 71    InternalData 0x14
RX 95 72615582 72615582 01 0001 9B8A 09F7 0809 FFFB 0004 0000 04B5 CA  UsartNrf3_Process_DevInform_InternalData()
                           ^^^^--------------------------------------- ???
                                ^^^^---------------------------------- 
                                     ^^^^----------------------------- 
                                          ^^^^------------------------ 
                                               ^^^^------------------- 
                                                    ^^^^-------------- 
                                                         ^^^^--------- 
RX 95 72615582 72615582 82 014B 0361 0361 660A 31                     
                           ^^^^--------------------------------------- ???
                                ^^^^---------------------------------- 
                                     ^^^^----------------------------- 
```

#### GetLossRate | 0x15

<details><summary>traces</summary>
<p>

```
22:00:39.560 > Fetch inverter: 112172615582
22:00:39.560 > 
22:00:39.560 >  >>> sendCommand: GetLossRate | 0x15 | 21
22:00:39.566 > 
22:00:39.566 > sendEsbPacket
22:00:39.566 > TX 15 72 61 55 82 78 56 34 11 80 15 00 62 E8 30 E7 00 00 00 00 00 00 00 00 3B 54 7D 
22:00:39.624 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 81 9B 26 09 30 8F C8 D7 
22:00:40.612 > RX Period End
22:00:40.613 > Success
```
</p>
</details>

Die Information in GetLossRate 0x15 sind m.E. sehr sinnvoll, da hier die RX/TX Statistik des Wechselrichters zu finden ist.
```
TX 15 72615582 78563411 80 1500 62E830E7 0000 00000000 0000 3B54 7D    GetLossRate 0x15
RX 95 72615582 72615582 81 9B26 0930 8FC8 D7                           UsartNrf3_Process_DevInform_GetLossRate()
                           ^^^^--------------------------------------- MI_CF_Num_Start/End Micro-inverse receive count
                                ^^^^---------------------------------- MI_RF_Num_Start/End Micro-inverse send count
```
Man muß die Werte auf DTU Seite initialisieren, falls diese (noch) 0 sind. 
Danach kann man diese Start Werte von den aktuellen Werte (End) abziehen und erhält die aktuelle Differenz.
Vielleicht sind diese Zähler bei einigen am Überlaufen ?


#### GetSelfCheckState | 0x1E

<details><summary>traces</summary>
<p>

```
21:57:39.511 > Fetch inverter: 112172615582
21:57:39.512 > 
21:57:39.512 >  >>> sendCommand: GetSelfCheckState | 0x1E | 30
21:57:39.517 > 
21:57:39.517 > sendEsbPacket
21:57:40.568 > TX 15 72 61 55 82 78 56 34 11 80 1E 00 62 E8 30 33 00 00 00 00 00 00 00 00 F5 F1 C9 
21:57:40.631 > Interrupt received |  > RX OK: 95 72 61 55 82 72 61 55 82 81 00 01 00 00 00 00 00 00 CB 50 8E 
21:57:41.614 > RX Period End
21:57:41.614 > Success
```
</p>
</details>

Die GetSelfCheckState 0x1E Anfrage wird in UsartNrf3_Process_Self_Check_State mit der Hilfsfunktion UsartNrf3_Process_GetDatatoProBuffer in einen pProBuffer kopiert. Erst danach werden die Werte ausgelesen.

```
TX 15 72615582 78563411 80 1E00 62E83033 0000 00000000 0000 F5F1 C9    GetSelfCheckState 0x1E
RX 95 72615582 72615582 81 0001 0000 0000 0000 CB50 8E                 UsartNrf3_Process_Self_Check_State()
                           ^^^^--------------------------------------- ver Data version
                                ^^^^---------------------------------- st Test status (2<=st<=6 Collecting / Collection completed)
                                     ^^^^----------------------------- gpf Grid-connected rule file code
                                          ^^^^------------------------ gpf_ver Grid-connected rule file version
                                               //st 4 to 6 There is no subsequent data
...                                            // 2<=st<=3 
                                               //First-level overvoltage self-test test results
                                               ^^^^------------------- code  
                                               ^^^^------------------- dflt_val
                                               ^^^^------------------- dflt_tim
                                               ^^^^------------------- rslt_val
                                               ^^^^------------------- rslt_tim
                                               //First-level undervoltage self-test test results
                                               ^^^^------------------- code  
                                               ^^^^------------------- dflt_val
                                               ^^^^------------------- dflt_tim
                                               ^^^^------------------- rslt_val
                                               ^^^^------------------- rslt_tim
                                               //Secondary overvoltage self-test test results
                                               ^^^^------------------- code  
                                               ^^^^------------------- dflt_val
                                               ^^^^------------------- dflt_tim
                                               ^^^^------------------- rslt_val
                                               ^^^^------------------- rslt_tim
                                               //Secondary undervoltage self-test test results
                                               ^^^^------------------- code  
                                               ^^^^------------------- dflt_val
                                               ^^^^------------------- dflt_tim
                                               ^^^^------------------- rslt_val
                                               ^^^^------------------- rslt_tim
                                               //First-level over-frequency self-test test results
                                               ^^^^------------------- code  
                                               ^^^^------------------- dflt_val
                                               ^^^^------------------- dflt_tim
                                               ^^^^------------------- rslt_val
                                               ^^^^------------------- rslt_tim
                                               //First-level underfrequency self-test test results
                                               ^^^^------------------- code  
                                               ^^^^------------------- dflt_val
                                               ^^^^------------------- dflt_tim
                                               ^^^^------------------- rslt_val
                                               ^^^^------------------- rslt_tim
                                               //Secondary over-frequency self-test test results
                                               ^^^^------------------- code  
                                               ^^^^------------------- dflt_val
                                               ^^^^------------------- dflt_tim
                                               ^^^^------------------- rslt_val
                                               ^^^^------------------- rslt_tim
                                               //Secondary underfrequency self-test test results
                                               ^^^^------------------- code  
                                               ^^^^------------------- dflt_val
                                               ^^^^------------------- dflt_tim
                                               ^^^^------------------- rslt_val
                                               ^^^^------------------- rslt_tim
```


#### InitDataState | 0xFF

DevInform 0x15 mit 0xFF als SubCmd ?
TX 15 72615582 78563412 FF <CRC8>

<details><summary>traces</summary>
<p>

```
23:13:06.763 > Fetch inverter: 112172615582
23:13:06.763 > sendCommand: DevInform
23:13:06.766 >  >>> Command DevInform <<<
23:13:06.768 > 
23:13:06.768 > sendEsbPacket
23:13:06.771 > TX 15 72 61 55 82 78 56 34 12 FF 26 
23:13:08.795 > RX Period End
23:13:08.795 > All missing
23:13:08.795 > Nothing received, resend whole request
23:13:08.800 > TX 15 72 61 55 82 78 56 34 12 FF 26 
23:13:10.826 > RX Period End
23:13:10.826 > All missing
23:13:10.826 > Nothing received, resend whole request
23:13:10.831 > TX 15 72 61 55 82 78 56 34 12 FF 26 
23:13:10.866 > Interrupt received |  > RX OK: D1 72 61 55 82 72 61 55 82 81 50 
23:13:10.872 > FATAL: (lib/Hoymiles/src/inverters/InverterAbstract.cpp, 51) fragment too short
23:13:12.857 > RX Period End
23:13:12.857 > All missing
23:13:12.857 > Nothing received, resend whole request
23:13:12.862 > TX 15 72 61 55 82 78 56 34 12 FF 26 
23:13:14.888 > RX Period End
23:13:14.888 > All missing
23:13:14.888 > Nothing received, resend count exeeded
```
</p>
</details>

```
TX 15 72615582 78563412 FF 26   InitDataState 0xFF
RX D1 72615582 72615582 81 50 
                        ^^----- ???
```


------------------------------------------------------------------------------------------


### Welche Device Control DEVCONTROL_ALL (0x51) Sub Kommandos gibt es

<details><summary>source code</summary>
<p>

```c
typedef enum
{
    Type_TurnOn = 0, // 0x00
    Type_TurnOff = 1, // 0x01
    Type_Restart = 2, // 0x02
    Type_Lock = 3, // 0x03
    Type_Unlock = 4, // 0x04
    Type_ActivePowerContr = 11, // 0x0b
    Type_ReactivePowerContr = 12, // 0x0c
    Type_PFSet = 13, // 0x0d
    Type_CleanState_LockAndAlarm = 20, // 0x14
    //dong 06-15
    Type_SelfInspection = 40, // 0x28 // self-inspection of grid-connected protection files
    Type_Init = 0xff, //0xff
} DevControlType;
```
</p>
</details>

SubCmd =
* [x] Type_TurnOn (0x00) Boot
* [x] Type_TurnOff (0x01) Shutdown
* [x] Type_Restart (0x02)
* [ ] Type_Lock (0x03)
* [ ] Type_Unlock (0x04)
* [x] Type_ActivePowerContr (0x0B) Active Power Limit
* [ ] Type_ReactivePowerContr (0x0C) Reactive Power Limit
* [ ] Type_PFSet (0x0D) Power Faktor Limit
* [ ] Type_CleanState_LockAndAlarm (0x14) Lock Alarm löschen
* [ ] Type_SelfInspection (0x28) Selbsttest
* [ ] Type_Init (0xFF)


### Wie sieht ein Device Control Kommando aus ?

```text
7E 51 81101507 81101507 81 00 00 B001 61 7F Type_TurnOn 0x00
7E 51 81101507 81101507 81 01 00 2000 F1 7F Type_TurnOff 0x01
7E 51 81101507 81101507 81 02 00 D000 02 7F Type_Restart 0x02
^^------------------------------------------ SOF Start of Frame 0x7E
   ^^--------------------------------------- MainCmd 0x51 DEVCONTROL_ALL
      ^^^^^^^^------------------------------ WR Serial ID
               ^^^^^^^^--------------------- DTU Serial ID wird vom NRF24 überschrieben, da initial vom Treiber gesetzt
                        ^^------------------ Single Frame ID
                           ^^--------------- SubCmd siehe oben
                           ^^^^^------------ Control Mode ? immer zwei Byte im Gen3 Protokoll
                                 ^^^^------- CRC16 / CRC-Modbus über die Daten, nach und excl. Frame ID!
                                      ^^---- CRC8
                                         ^^- EOF End of Frame 0x7F
```

### Wie kann man das Passwort setzen / zurücksetzen

Mit SubCmd `0x03` Type_Lock und `0x04` Type_Unlock kann man ein Passwort (vierstellige Pin) setzen.
```c
AdminPasswd[4] = {10, 16, 50, 82}; // = 0x0A 0x10 0x32 0x52 oder 0x0A103252
```

Nach dem Vergleich mit dem Master / AdminPassword wird das neue Passwort einfach auf 0x00000000 gesetzt und das alte Passwort mit 0xFFFFFFFF überschrieben.

```c
            if(memcmp((u8 *)AdminPasswd, (u8 *)Dtu3Detail.Property.LockOldPassword, 4) == 0)
            {
                memset((u8 *)Dtu3Detail.Property.LockNewPassword, 0, 4);
                memset((u8 *)Dtu3Detail.Property.LockOldPassword, 0xff, 4);
                memcpy((u8 *)MIMajor[PortNO].Property.Pass.PassWordSet.PWO, (u8 *)Dtu3Detail.Property.LockOldPassword, 4);
                memcpy((u8 *)MIMajor[PortNO].Property.Pass.PassWordSet.PWN, (u8 *)Dtu3Detail.Property.LockNewPassword, 4);
                memcpy((u8 *)MIMajor[PortNO].Property.Pass.PassWordSet.ATTime, (u8 *)Dtu3Detail.Property.Lock_Time, 2);
            }
```

### Wie funktioniert das Active Power Limit (0x0B) Sub Kommando 

Leistungsreduzierung HM300 · Issue #35 · tbnobody/OpenDTU
https://github.com/tbnobody/OpenDTU/issues/35


Active Power Limit (0x0B)
```text
21:06:33.342 > TX 51 72 61 55 82 78 56 34 12 81 0B 00 00 96 01 00 DC E0 BC 
                  51 74 40 33 29 78 56 34 12 81 0b 00 00 96 01 00 dc e0 56  => 0x96 = dezimal 150, d.h. das sind 15.0 Watt
21:06:33.570 > Interrupt received
21:06:33.570 > 
21:06:33.570 > >> RX  OK: D1 72 61 55 82 72 61 55 82 81 00 00 0B 00 14 07 48 
```

```text
<0x51> <WR> <DTU> <0x81> <0x0b 0x00> <0x00 0x96> <0x01 0x00> <CRC16/modbus> <crc8>
<Cmd> <target> <source> <subcmd> <limit> <?desc?-fix 0x01 0x00> <crc16/modbus> <crc8>
```

Das mit dem `0x0B00` hatte ich irgendwie anders interpretiert, da er den Wert ja mit `(u16)(SubCmd << 8)` in `UsartNrf_Send_DevControlUpdate()` übergibt und als `u16 ControlMode` in `UsartNrf3_Send_PackDevControl()` übernimmt.
Also wird aus dem `SubCmd=0x0b` -> `Control Mode=0x0b00`.
Und das wird dann wiederum als `temp_dat[10] = 0x0b` und `temp_dat[11] = 0x00` an den NRF24 per USART übergeben.

`P_Limit1` is the absolute value of the power limit, **the unit is W, with 1 decimal place**


`Dtu3Detail.Property.DRM_Limit_Switch` oder `Dtu3Detail.Property.SunSpec_Switch` dann
`.Desc[0] = 0x00 .Desc[1] 0x01`

`Dtu3Detail.Property.Zero_Export_Switch` oder `Dtu3Detail.Property.Phase_Balance_Switch` dann `.Desc[0] = 0x00 .Desc[1] 0x00`

Vielleicht wäre es übersichtlicher, wenn du `Desc[0]` und `[1]` in der Reihenfolge vertauschst, das liest sich besser, so landet es ja am Ende im Befehl, erst [0] dann [1]

### Wie funktioniert das Reactive Power Limit Setzen (0x0D) Kommando

```text
81 0C 00 00 64 00 0a
^^------------------- SingleFrameID
   ^^---------------- SubCmd bzw. DevControlType: 0x0C = Type_ReactivePowerContr
   ^^ ^^------------- Control Mode
         ^^ ^^------- PowerPFDev.SetValut 0x0064 = 4.0 W
               ^^ ^^- PowerPFDev.Desc das müsste m.W. immer (?) mit 0x00 01 angegeben sein
```

Sollte also `51 74403329 78563412 81 0D00 0000 0000 0601 14` oder sowas sein.... 
Schreibt halt m.W. einen PowerFactor, aber Du hast glaube ne DTU mit der Du das ggf. korrigieren kannst oder ?

### Wie funktioniert das Power Faktor Setzen (0x0D) Kommando

```text
81 0D 00 00 64 00 0a
^^------------------- SingleFrameID
   ^^---------------- SubCmd bzw. DevControlType: 0x0D = Type_PFSet
   ^^ ^^------------- Control Mode
         ^^ ^^------- PowerPFDev.SetValut 0x0064 = 4.0 W
               ^^ ^^- PowerPFDev.Desc das müsste m.W. immer (?) mit 0x00 01 angegeben sein
```

Sollte also `51 74403329 78563412 81 0D00 0000 0000 0601 14` oder sowas sein.... 
Schreibt halt m.W. einen PowerFactor, aber Du hast glaube ne DTU mit der Du das ggf. korrigieren kannst oder ?

------------------------------------------------------------------------------------------

### Welche Parameter Setzen PARASET_ALL (0x52) Kommandos gibt es 

`UsartNrf3_Send_PackSetPara()`

Sowas wie EleEnergySet `0x01` und AntitheftParaSet `0x04`

* EleEnergySet (0x01)
* AntitheftParaSet (0x04) Passwort setzen

### Welche File Multi-Package Kommandos gibt es 
### Wie wird das DOWN_PRO (0x0E) / DOWN_DAT (0x0A) verwendet

* Type_Init (`0xFF`)
Das SubCmd = Type_Init (`0xFF`) scheint nur bei MainCmd = DOWN_PRO (`0x0E`) oder DOWN_DAT (`0x0A`) verwendet zu werden.

O&M > **Grid Profile Management**

File Name | Alias | Device Ver.
--- | --- | ---
AT_TOR_Erzeuger_default |  | Gen3
DE_VDE4105_2011 |  | Gen3
DE_VDE4105_2018 |  | Gen3
AT-OVE-E-8001 |  | Gen2
Germany_VDE4105 |  | Gen2
LN_50Hz |  | Gen2

- [File Name: **AT_TOR_Erzeuger_default**](#file-name-at_tor_erzeuger_default)
- [File Name: **DE_VDE4105_2011**](#file-name-de_vde4105_2011)
- [File Name: **DE_VDE4105_2018**](#file-name-de_vde4105_2018)
- [File Name: **AT-OVE-E-8001**](#file-name-at-ove-e-8001)
- [File Name: **Germany_VDE4105**](#file-name-germany_vde4105)
- [File Name: **LN_50Hz**](#file-name-ln_50hz)

#### File Name: **AT_TOR_Erzeuger_default**

SN | Name | Value | Unit | Range
--- | --- | --- | --- | ---
1 | **AT_TOR_Erzeuger_default** (?) |
2 | **H/LVRT** (?) |
3 | Nominal Voltage (NV) | 230 | V | ~
4 | Low Voltage 1 (LV1) | `184` | V | 170~184
5 | LV1 Maximum Trip Time (MTT) | 1.5 | s | ~
6 | High Voltage 1 (HV1) | `255.3` | V | 253~270
7 | HV1 Maximum Trip Time (MTT) | 0.1 | s | ~
8 | Low Voltage 2 (LV2) | 57.5 | V | ~
9 | LV2 Maximum Trip Time (MTT) | 0.5 | s | ~
10 | High Voltage 2 (HV2) | `264.5` | V | 264.5~275
11 | HV2 Maximum Trip Time (MTT) | 0.08 | s | ~
12 | 10 mins Average High Voltage (AHV) | `255.3` | V | 245~255.3
13 | **H/LFRT** (?) |
14 | Nominal Frequency | 50 | Hz | ~
15 | Low Frequency 1 (LF1) | `47.5` | Hz | 47.5~49
16 | LF1 Maximum Trip Time (MTT) | 0.1 | s | ~
17 | High Frequency 1 (HF1) | `51.5` | Hz | 50.5~51.5
18 | HF1 Maximum Trip Time (MTT) | 0.1 | s | ~
19 | **Islanding Detection** (?) |
20 | ID Function Activated | `1` |  | 0~1
21 | **Reconnection (RT)** (?) |
22 | Reconnect Time (RT) | `60` | s | 10~300
23 | Reconnect High Voltage (RHV) | `250.7` | V | 240~250.7
24 | Reconnect Low Voltage (RLV) | `195.5` | V | 195.5~210
25 | Reconnect High Frequency (RHF) | `50.1` | s | 50.1~50.9
26 | Reconnect Low Frequency (RLF) | `47.5` | s | 47.5~49.9
27 | **Ramp Rates (RR)** |
28 | Normal Ramp up Rate (RUR_NM) | `20` | Rated%/s | 10~100
29 | Soft Start Ramp up Rate (RUR_SS) | `0.16` | Rated%/s | 0.1~10
30 | **Frequency Watt (FW)** (?) |
31 | FW Function Activated | `1` |  | 0~1
32 | Start of Frequency Watt Droop (Fstart) | `50.2` | Hz | 50.2~52
33 | FW Droop Slope (Kpower_Freq) | `40` | Pn%/Hz | 16.7~100
34 | Recovery Ramp Rate (RRR) | `0.16` | Pn%/s | 0.1~50
35 | **Volt Watt (VW)** (?) |
36 | VW Function Activated | `1` |  | 0~1
37 | Start of Voltage Watt Droop (Vstart) | 253 | V | ~
38 | End of Voltage Watt Droop (Vend) | 257.6 | V | ~
39 | VW Droop Slope (Kpower_Volt) | 21.74 | Pn%/Hz | ~
40 | **Volt Var (VV)** (?) |
41 | VV Function Activated | `0` |  | 0~1
42 | Voltage Set Point V1 | 211.6 | V | ~
43 | Reactive Set Point Q1 | `30` | %Pn | 0~50
44 | Voltage Set Point V2 | 220.8 | V | ~
45 | Voltage Set Point V3 | 241.5 | V | ~
46 | Voltage Set Point V4 | 248.4 | V | ~
47 | Reactive Set Point Q4 | `30` | %Pn | 0~50
48 | **Specified Power Factor (SPF)** (?) |
49 | SPF Function Activated | `0` |  | 0~1
50 | Power Factor (PF) | `v` `0.95` |  | 0.9~1
51 | **Watt Power Factor (WPF)** (?) |
52 | WPF Function Activated | `0` |  | 0~1
53 | Start of Power of WPF (Pstart) | 50 | %Pn | ~
54 | Power Factor ar Rated Power (RFRP) | `0.95` |  | 0.8~1
55 | **Active Power Control (APC)** (?) |
56 | APC Function Activated | `1` |  | 0~1
57 | Power Ramp Rate (PRR) | `100` | Pn%/s | 0.33~100
58 | **Reactive Power Control (RPC)** (?) |
59 | RPC Function Activated | `0` |  | 0~1
60 | Reactive Power (VAR) | `v` `0` | %Sn | 0~50

Save and generate new profile

#### File Name: **DE_VDE4105_2011**

SN | Name | Value | Unit | Range
--- | --- | --- | --- | ---
1 | **DE_VDE4105_2011** (?) |
2 | **H/LVRT** (?) |
3 | Nominal Voltage (NV) | 230 | V | ~
4 | Low Voltage 1 (LV1) | `184` | V | 170~184
5 | LV1 Maximum Trip Time (MTT) | 0.1 | s | ~
6 | High Voltage 1 (HV1) | `264.5` | V | 264.5~270
7 | HV1 Maximum Trip Time (MTT) | 0.1 | s | ~
8 | 10 mins Average High Voltage (AHV) | `253` | V | 253~260
9 | **H/LFRT** (?) |
10 | Nominal Frequency | 50 | Hz | ~
11 | Low Frequency 1 (LF1) | `47.5` | Hz | 47~49.5
12 | LF1 Maximum Trip Time (MTT) | 0.1 | s | ~
13 | High Frequency 1 (HF1) | `51.5` | Hz | 50.5~53.5
14 | HF1 Maximum Trip Time (MTT) | 0.1 | s | ~
15 | **Islanding Detection** (?) |
16 | ID Function Activated | `1` |  | 0~1
17 | **Reconnection (RT)** (?) |
18 | Reconnect Time (RT) | `65` | s | 10~300
19 | Reconnect High Voltage (RHV) | `264.5` | V | 253~264.5
20 | Reconnect Low Voltage (RLV) | `184` | V | 182~210
21 | Reconnect High Frequency (RHF) | `51.5` | V | 50.5~52
22 | Reconnect Low Frequency (RLF) | `47.5` | V | 47~49.5
23 | Short Interruption Reconnect Time (SRT) | 8 | s | ~
24 | Short Interruption Time (SIT) | 3 | s | ~
25 | **Ramp Rates (RR)** |
26 | Normal Ramp up Rate (RUR_NM) | `20` | Rated%/s | 10~100
27 | Soft Start Ramp up Rate (RUR_SS) | `10` | Rated%/s | 0.1~20
28 | **Active Power Control (APC)** (?) |
29 | APC Function Activated | `1` |  | 0~1

Save and generate new profile

#### File Name: **DE_VDE4105_2018**

SN | Name | Value | Unit | Range
--- | --- | --- | --- | ---
1 | **DE_VDE4105_2018** (?) |
2 | **H/LVRT** (?) |
3 | Nominal Voltage (NV) | 230 | V | ~
4 | Low Voltage 1 (LV1) | `184` | V | 160~195.5
5 | LV1 Maximum Trip Time (MTT) | 3 | s | 3~3
6 | High Voltage 1 (HV1) | `287.5` | V | 270~287.5
7 | HV1 Maximum Trip Time (MTT) | 0.1 | s | 0.1~0.1
8 | Low Voltage 2 (LV2) | `103.5` | V | 100~150
9 | LV2 Maximum Trip Time (MTT) | 0.3 | s | 0.3~0.3
10 | 10 mins Average High Voltage (AHV) | `253` | V | 250~270
11 | **H/LFRT** (?) |
12 | Nominal Frequency | 50 | Hz | ~
13 | Low Frequency 1 (LF1) | `47.5` | Hz | 47.5~49.9
14 | LF1 Maximum Trip Time (MTT) | 0.1 | s | 0.1~0.1
15 | High Frequency 1 (HF1) | `51.5` | Hz | 50.1~51.5
16 | HF1 Maximum Trip Time (MTT) | 0.1 | s | 0.1~0.1
17 | **Islanding Detection** (?) |
18 | ID Function Activated | `1` |  | 0~1
19 | **Reconnection (RT)** (?) |
20 | Reconnect Time (RT) | `60` | s | 10~300
21 | Reconnect High Voltage (RHV) | `253` | V | 240~253
22 | Reconnect Low Voltage (RLV) | `195.5` | V | 195.5~210
23 | Reconnect High Frequency (RHF) | `50.1` | s | 50.1~50.9
24 | Reconnect Low Frequency (RLF) | `47.5` | s | 47.5~49.9
25 | **Ramp Rates (RR)** |
26 | Normal Ramp up Rate (RUR_NM) | `20` | Rated%/s | 5~100
27 | Soft Start Ramp up Rate (RUR_SS) | `0.16` | Rated%/s | 0.1~10
28 | **Frequency Watt (FW)** (?) |
29 | FW Function Activated | `1` |  | 0~1
30 | Start of Frequency Watt Droop (Fstart) | `50.2` | Hz | 50.2~52
31 | FW Droop Slope (Kpower_Freq) | `40` | Pn%/Hz | 16.7~100
32 | Recovery Ramp Rate (RRR) | `0.16` | Pn%/s | 0.1~50
33 | Recovery High Frequency (RVHF) | `50.2` | Hz | 50.1~52
34 | Recovery Low Frequency (RVLF) | `49.8` | Hz | 49~49.9
35 | **Active Power Control (APC)** (?) |
36 | APC Function Activated | `1` |  | 0~1
37 | Power Ramp Rate (PRR) | `100` | Pn%/s | 0.33~100
38 | **Volt Var (VV)** (?) |
39 | VV Function Activated | `0` |  | 0~1
40 | Voltage Set Point V1 | 213.9 | V | ~
41 | Reactive Set Point Q1 | `30` | %Pn | 0~100
42 | Voltage Set Point V2 | 223.1 | V | ~
43 | Voltage Set Point V3 | 236.9 | V | ~
44 | Voltage Set Point V4 | 246.1 | V | ~
41 | Reactive Set Point Q4 | `30` | %Pn | 0~100
46 | **Specified Power Factor (SPF)** (?) |
47 | SPF Function Activated | `0` |  | 0~1
48 | Power Factor (PF) | `v` `0.95` |  | 0.9~1
49 | **Watt Power Factor (WPF)** (?) |
50 | WPF Function Activated | `0` |  | 0~1
51 | Start of Power of WPF (Pstart) | 50 | %Pn | ~
52 | Power Factor ar Rated Power (RFRP) | `0.95` |  | 0.8~1
53 | **Reactive Power Control (RPC)** (?) |
54 | RPC Function Activated | `0` |  | 0~1
55 | Reactive Power (VAR) | `v` `0` | %Sn | 0~50

Save and generate new profile

#### File Name: **AT-OVE-E-8001**

SN | Name | Value | Unit | Range
--- | --- | --- | --- | ---
1 | **Voltage limits and trip time** |
2 | Over voltage limit | 264.5 | V | ~
3 | Under voltage limit | 184 | V | ~
4 | Average over voltage | `253.11` | V | 253~264.5
5 | **Frequency limits and trip time** |
6 | Over frequency limit | 51.5 | Hz | ~
7 | Under frequency limit | 47.5 | Hz | ~
8 | **Reconnect time** |
9 | Short term reconnect time | `8` | s | 5~10
10 | Long term reconnect time | `65` | s | 60~300

Save and generate new profile

#### File Name: **Germany_VDE4105**

SN | Name | Value | Unit | Range
--- | --- | --- | --- | ---
1 | **Voltage limits and trip time** |
2 | Over voltage limit | 264.5 | V | ~
3 | Under voltage limit | 184 | V | ~
4 | Average over voltage | `253` | V | 253~260
5 | **Frequency limits and trip time** |
6 | Over frequency limit | 51.5 | Hz | ~
7 | Under frequency limit | 47.5 | Hz | ~
8 | **Reconnect time** |
9 | Short term reconnect time | `8` | s | 5~10
10 | Long term reconnect time | `65` | s | 60~300

Save and generate new profile

#### File Name: **LN_50Hz**

SN | Name | Value | Unit | Range
--- | --- | --- | --- | ---
1 | **Voltage limits and trip time** |
2 | Over voltage limit | 280 | V | ~
3 | Over voltage limit trip time | 0.1 | s | ~
4 | Over voltage limit (slow) | `255` | V | 240~270
5 | Over voltage limit trip time (slow) | `0.5` | s | 0.1~20
6 | Under voltage limit | 110 | V | ~
7 | Under voltage limit trip time | 0.1 | s | ~
8 | Under voltage limit (slow) | `170` | V | 170~220
9 | Under voltage limit trip time (slow) | `0.5` | s | 0.1~20
10 | **Frequency limits and trip time** |
11 | Over frequency limit | 54 | Hz | ~
12 | Over frequency limit trip time | `0.1` | s | 0.05~1
13 | Over frequency limit (slow) | `53` | Hz | 50.2~54
14 | Over frequency limit trip time (slow) | `0.5` | s | 0.1~20
15 | Under frequency limit | 46 | Hz | ~
16 | Under frequency limit trip time | `0.1` | s | 0.05~1
17 | Under frequency limit (slow) | `47` | Hz | 46~49.5
18 | Under frequency limit trip time (slow) | `0.5` | s | 0.1~20
19 | **Reconnect time** |
20 | Long term reconnect time | `180` | s | 20~800

Save and generate new profile

### Was bedeutet die Antwort ANSWER_EXCEPTION_MULTI_ONE 0xF1 bzw. ANSWER_EXCEPTION_ONE_MULTI 0xFF

Das ist ein Fehler bzw. eine Fehlermeldung.

```c
#define ANSWER_EXCEPTION_MULTI_ONE 0xF1
#define ANSWER_EXCEPTION_ONE_MULTI 0XFF
```

Fehler ist `0xF1` oder `0xFF` je nachdem ob SingleFrame / MultiFrame Anfrage

------------------------------------------------------------------------------------------


## Funkverbindung

### Wird Auto-ACK vom Wechselrichter beim nRF24L01+ unterstützt

Tatsache ist, es ist sehr unwahrscheinlich, dass der WR antworten wird, 
wenn er nicht einmal ein ACK sendet.

------------------------------------------------------------------------------------------


## Reverse Engineering

### Wo und wie kann das Protokoll mitgeschnitten werden

* Mit einem Scanner (HackRF oder nRF24L01+) auf der/n Funkfrequenz/en


* Mit einem Logic Analyzer zwischen MCU und nRF24L01+

  eine RX und eine TX Leitung zwischen den beiden Chips (UART). Der 
  Mikrocontroller hat laut Datenblatt ([1], s.o.) genau eine serielle 
  Schnittstelle, bei dem verbauten 32-pin-Gehäuse sollten die hier sein:
  - P0.4 (Pin  7): RXD
  - P0.3 (Pin 10): TXD

### Was ist ein Scanner und welche gibt es

Welche Scanner eingesetzt wurden: ich nutzte die von den Libs RF24 und nrf_hal.

