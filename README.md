# IPSymconDataFlowGenerator

Modul für IP-Symcon ab Version 4. Dieses Modul dient keiner Steuerung eines Geräts. Es dient nur dazu eine Grundstruktur an Files für ein PHP Modul zu erstellen.

## Dokumentation

**Inhaltsverzeichnis**

1. [Funktionsumfang](#1-funktionsumfang)  
2. [Voraussetzungen](#2-voraussetzungen)  
3. [Installation](#3-installation)  
4. [Funktionsreferenz](#4-funktionsreferenz)
5. [Konfiguration](#5-konfiguartion)  
6. [Anhang](#6-anhang)  

## 1. Funktionsumfang

Mit dem Modul lassen sich GUIDs für ein PHP Modul von IP-Symcon generieren. Desweiteren wird aus generierten oder bereits vorhandenen GUIDs ein Grundgerüst erstellt auf dessen Grundlage dann ein individuelles PHP Modul gebaut werden kann. 

### GUID und Vorlagen generieren:  

 - GUID generieren
 - Erstellt Vorlagen für module.json und module.php für Datenfluss
  

## 2. Voraussetzungen

 - IPS 4.1

## 3. Installation

### a. Laden des Moduls


Die IP-Symcon (min Ver. 4.x) Konsole öffnen. Im Objektbaum unter Kerninstanzen die Instanz __*Modules*__ durch einen doppelten Mausklick öffnen.

![Modules](docs/Modules.png?raw=true "Modules")

In der _Modules_ Instanz rechts oben auf den Button __*Hinzufügen*__ drücken.

![Modules](docs/Hinzufuegen.png?raw=true "Hinzufügen")
 
In dem sich öffnenden Fenster folgende URL hinzufügen:

	
    `https://github.com/Wolbolar/IPSymconDataFlowGenerator`  
    
und mit _OK_ bestätigen.    
    
### b. Einrichtung in IPS

In IP-Symcon nun _Instanz hinzufügen_ (_CTRL+1_) auswählen unter der Kategorie, unter der man die Instanz hinzufügen will, und _PHP Modul Dataflow Generator_ auswählen.
Im Konfigurationsformular sind die Parameter zu ergänzen. 


## 4. Funktionsreferenz

### GUID:

In IP-Symcon werden Daten zwischen einzelnen Instanzen über den [Datenfluss in IP-Symcon](https://www.symcon.de/service/dokumentation/entwicklerbereich/sdk-tools/sdk-php/datenfluss/) weitergegeben. 
Hierbei hat jede Instanz in IP-Symcon eine eindeutige GUID (Globally Unique Identifier), anhand dessen die Instanz eindeutig erkannt werden kann. Für ein PHP Modul braucht jede Instanz eine eindeutige GUID.
Innerhalb der module.json wird angegeben wie die GUID der anderen mit der Instanz kommunizierenden Instanzen lauten, damit IP-Symcon weis wohin die Daten zu senden sind.
Existierende Instanzen wie TCP, UDP, Mulicast Socket usw. haben feststehende GUID über die diese angesprochen werden. Sollte man z.B. einen eigene IO Instanz definieren wird auch hierfür eine GUID benötigt.
Der Datenaustausch zwischen IO <-> Splitter <-> Gerät erfolgt über die Funktionen [ForwardData](https://www.symcon.de/service/dokumentation/entwicklerbereich/sdk-tools/sdk-php/module/forwarddata/) und [ReceiveData](https://www.symcon.de/service/dokumentation/entwicklerbereich/sdk-tools/sdk-php/module/receivedata/) in beiden
Funktionen ist jewiels die passende GUID einzutragen damit die funktion an die passende Instanz versendet.

Das Modul ist einfach eine kleine Hilfestellung um neue GUID zu generieren bzw. nicht versehentlich eine GUID an die falsche Stelle zu kopieren. Daher können die Vorlagen die generiert werden so übernommen werden und die GUID sind schon an der passenden Stelle eingetragen.


## 5. Konfiguration:

Pro PHP Modul das erstellt werden soll und für das Vorlagen generiert werden sollen ist eine Kategorie anzulegen unter der dann das Modul Skripte als Vorlagen ablegt.

### DataFlowGenerator:

| Eigenschaft | Typ     | Standardwert | Funktion                                  |
| :---------: | :-----: | :----------: | :---------------------------------------: |
| CategoryID  | integer |              | Objekt ID der Katergorie für Vorlagen     |
| author      | string  |              | Verfasser des Moduls                      |
| modulename  | string  |              | Modulname                                 |
| url         | string  |              | URL                                       |
| version     | string  |              | Version des PHP Moduls                    |
| build       | string  |              | Build                                     |
| vendor      | string  |              | Hersteller                                |
| prefix      | string  |              | Prefix zum Aufrufen von Methoden          |
| aliases     | string  |              | Anzeige Name im Auswahlmenü               |






## 6. Anhang

###  a. Funktionen:

#### PHP Modul Dataflow Generator:

```php
DataFlowGenerator_GenerateGUID(integer $InstanceID)
```

Generiert mehrere GUID für ein PHP Modul. Die GUID wird in einem Array von der Funktion zurückgeben. Gleichzeitig werden die GUID in den Webfront geschrieben.

```php
DataFlowGenerator_CreateScripts(integer $InstanceID, array $instances, array $files, $volume)
```

Legt unter der im Modul eingestellten Kategorie Bespiel Skripte an. Diese können als Vorlage für ein PHP Modul genutzt werden.


###  b. GUIDs und Datenaustausch:

#### PHP Modul Dataflow Generator:

GUID: `{CB4BD64D-7088-42F0-919F-644C00CF0EBE}` 




