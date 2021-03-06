<!--

author:   Sebastian Zug & André Dietrich
email:    zug@ovgu.de   & andre.dietrich@ovgu.de
version:  0.0.1
language: de
narrator: Deutsch Female

@logo: <a href="https://www.hrk.de/weltoffene-hochschulen"><img style="width: 10%; position:absolute; right:20px; top: 30px" src="https://www.hrk.de/fileadmin/redaktion/hrk/news/_migrated/images/Logo-Fuer-PM-Startseite.jpg"></a>


link:     https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.min.css

import: https://raw.githubusercontent.com/LiaTemplates/Rextester/master/README.md
import: https://raw.githubusercontent.com/LiaTemplates/WebDev/master/README.md
import: https://raw.githubusercontent.com/LiaTemplates/NetSwarm-Simulator/master/README.md
-->


# Arduino Einführung

@logo

**Eingebette Systeme**

Prof. Dr. Sebastian Zug,
Technische Universität Bergakademie Freiberg

------------------------------

![Welcome](images/WorkingDesk.jpg "Experiments")<!-- width="80%" -->

<h2>Herzlich Willkommen!</h2>

> Die interaktive Ansicht dieses Kurses ist unter folgendem [Link](https://liascript.github.io/course/?https://raw.githubusercontent.com/liaScript/ArduinoEinstieg/master/Course_00.md#1) verfügbar.

https://github.com/liaScript/ArduinoEinstieg/blob/master/Course_00.md


## 1. Einführung

@logo

![Welcome](images/PassatMitInnenleben.png "Motivation")<!-- width="40%" -->

**Was heißt das eigentlich "Eingebettetes System"?**

                              {{1-2}}
*******************************************************************************
> ... ein elektronischer Rechner ..., der in einen technischen Kontext
> eingebunden ist. Dabei übernimmt der (Kleinst-)Rechner entweder
> Überwachungs-, Steuerungs- oder Regelfunktionen ... weitestgehend unsichtbar
> für den Benutzer .. \[nach Wikipedia "Eingebettete Systeme"\].
*******************************************************************************

**Wie programmiere ich einen Mikrocontroller?**

                              {{2-3}}
*******************************************************************************
> Compiler wird eine Software genannt, die einen in einer Programmiersprache
> geschrieben Quellcode so übersetzt, dass sie von Maschinen verstanden
> werden können.
*******************************************************************************

**Was ist das Arduino Projekt?**

                                 {{3}}
*******************************************************************************
> Arduino ist eine aus Soft- und Hardware bestehende
> Physical-Computing-Plattform. Beide Komponenten sind im Sinne von Open
> Source quelloffen. Die Hardware besteht aus einem einfachen E/A-Board mit
> einem Mikrocontroller und analogen und digitalen Ein- und Ausgängen.

  https://www.arduino.cc/

  ![Arduino Hardwarefamilie](images/ArduinoGallery.jpg "ArduinoFamilie")<!-- width="70%" -->
  [^3]

[^3] aus entsprechendem Artikel "Spiegel Online" http://www.spiegel.de/netzwelt/gadgets/arduino-erklaert-das-kann-der-microcontroller-a-1105328.html

*******************************************************************************

## 2. Arduino Programmierung

@logo

Arduino nutzt eine C/C++ Semantik für die Programmierung, die folgende
Grundelemente bedient

+ Alle Anweisungen enden mit einem `;`
+ Variabeln sind typbehaftet (`int`, `char`, `float`, etc.)
+ wichtige Schlüsselwörter sind `for`, `if`, `while`, etc.
+ Kommentare werden durch `//` eingeleitet

![Cheat-Sheet](images/Arduino-Cheat-Sheet_v0.1.png "Cheat-Sheet")<!-- width="80%" -->

Unter 2.4 folgen einige Beispiele für den Gebrauch der Schleifen und Verzweigungen.

### 2.1 Aufbau eines Arduino-Programmes

@logo

Jedes Arduinoprogramm umfasst 2 grundlegende Funktionen `setup()` und `loop()`.

```c
const int ledPin = 13;

// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin ledPin as an output.
  pinMode(ledPin, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(ledPin, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                  // wait for a second
  digitalWrite(ledPin, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                  // wait for a second
}
```

### 2.2 Arduino IDE

@logo

![Bildtext](images/ArduinoIDE_Screenshot.jpg "Arduino IDE")<!-- width="80%" -->

Wichtige Grundeinstellungen:

+ Richtigen Port für den Programmiervorgang auswählen (Tools -> Port)
+ Richtigen Controller auswählen (Tools -> Board)
+ Richtige Baudrate für die Serielle Schnittstellen

### 2.3 Hello World

@logo

*Und jetzt sind Sie dran!*

Laden Sie das Beispielprogramm "Blink" in Ihren Editor:

Datei -> Beispiele -> Basics -> Blink

Kompilieren und flashen Sie das Programm! Wichtige Tastaturbefehle sind dabei

| Tastenkombination | Bedeutung                |
| ----------------- | ------------------------ |
| Strg-R            | Kompilieren (Ve**R**ify) |
| Strg-U            | Flashend (**U**pload)    |
| Strg-T            | Code korrekt einrücken   |
| Strg-Shift-M      | Seriellen Monitor öffnen |
| Strg-L            | Cursor auf Zeile setzen  |

### 2.4 C++ Basiskonstrukte und die Serielle Schnittstelle

@logo

                              {{0-1}}
*******************************************************************************

Was fehlt? Ich möchte irgendwie in den Rechner schauen können :-)

Die Serielle Schnittstelle (häufig auch als UART) bezeichnet ermöglicht das
Versenden und den Empfang von Textnachrichten. Damit können Sie zum Beispiel
Messwerte ausgeben oder das Erreichen bestimmter Programmpositionen anzeigen.

Die folgenden Beispiele vermitteln grundlegende Programmierkonstrukte in C++.
Anhand des NetSwarm Simulator können diese ausgeführt werden.  Achtung, bis auf
die Serielle Schnittstelle können keine  weiteren Funktionalitäten genutzt
werden!

```c
void setup() {
  Serial.begin(9600);
  Serial.println("Hello World");
}

void loop() {
}
```
@NetSwarm.single_loop

Arduino kennt zwei Varianten der Ausgabe mit `print` - das einfache `print` und `println`. Welchen Unterschied vermuten Sie?
*******************************************************************************

                              {{1-2}}
*******************************************************************************

**Schleifen**

Was müssen wir tuen, um die Zahlen von 1 bis 10 auf dem Terminal anzuzeigen?

```c
void setup() {
  Serial.begin(9600);
  int counter = 0;
  for (int i = 0; i < 10; i++){
    Serial.println(counter);  
    counter = counter + 1;
  }
}

void loop() {
}
```
@NetSwarm.single_loop

Welche "Einsparmöglichkeiten" sehen Sie als erfahrener Programmierer in dem Beispiel? Wie kann der Code, mit der gleichen Ausgabe kürzer gestaltet werden?
*******************************************************************************

                              {{2-3}}
*******************************************************************************

**Verzweigungen**

Verzweigungen folgen dem Muster

```c
if (Bedingung) {
  // Anweisungen
}
else{               
  // Anweisungen       
}                      
```

wobei der `else` Abschnitt optional ist.

```c
void setup() {
  Serial.begin(9600);
  float value = 5.234;
  Serial.print(value);
  if (value > 10){
    Serial.println(" - Der Wert ist größer als 10!");
  }else{
    Serial.println(" - Der Wert ist kleiner als 10!");
  }
}

void loop() {
}
```
@NetSwarm.single_loop

*******************************************************************************


                              {{3-4}}
*******************************************************************************

Bedingungen werden dabei wie folgt formuliert:

```c
void setup() {
  Serial.begin(9600);
  int a = 2;
  if (a == 2) {Serial.println("a ist gleich zwei!");}
  if (a <= 5) {Serial.println("a ist kleiner oder gleich fünf!");}
  if (a != 3) {Serial.println("a ist ungleich drei!");}
  char b = 'g';
  if (b == 'z') {Serial.println("In b ist ein z gespeichert!");}
  else {Serial.println("In b ist kein z gespeichert!");}
}

void loop() {
}
```
@NetSwarm.single_loop

Für die Ausgabe von komplexeren, vorformatierten Ausdrücken können Sie auf einen
Befehl aus der C++ Standard-Bibliothek zurückgreifen `sprintf`

Eine anschauliche Dokumentation findet sich unter: [link](https://arduinobasics.blogspot.com/2019/05/sprintf-function.html)

*******************************************************************************

## 3. Einstiegsübung

@logo

> **Aufgabe:** Schreiben Sie einen Code, der das *SOS* Morsesignal über die
> Led ausgibt!

Welche Anpassungen sind dafür an unserem Beispiel vornehmen?

```c
const int ledPin = 13;

// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin ledPin as an output.
  pinMode(ledPin, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(ledPin, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                  // wait for a second
  digitalWrite(ledPin, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                  // wait for a second
}
```

## 4. Aufgabenkomplexe

@logo

![MangoLabsSet](images/MangoLabsSet.jpg "MangoLabsSet")<!-- width="80%" -->

* Webseiten des Wiki des Herstellers mangolabs
   [https://www.mangolabs.de/wiki/](https://www.mangolabs.de/wiki/)

* Referenzübersicht Arduino

    + deutsch (unvollständig) https://www.arduino.cc/reference/de/

    + englisch https://www.arduino.cc/reference/en/


### 3a. Serielle Schnittstelle

@logo

Die Arbeit mit der seriellen Schnittstelle vom Arduino zum PC kennen Sie bereits. Aber das Ganze funktioniert auch umgekehrt.

<!--
style="height: 60px; display: block; margin-right: auto;"
-->
````
-> Demo:  Vorführung Erfassen von Zeichen
````

> **Aufgabe:** Erweitern Sie den Code, so dass wir die LED über 'A' an- und
> 'B' ausschalten können.

{{1-2}}
```c      ControlLed.ino
// Loesung
void loop() {
  if (Serial.available() > 0) {
        incomingByte = Serial.read();
        Serial.write(incomingByte);
        if (incomingByte == 'A'){
          Serial.println("An");
          digitalWrite(13, HIGH);
        }
        if (incomingByte == 'B'){
          digitalWrite(13, LOW);
          Serial.println("Aus");
        }
  }
}
```

### 3b. Taster als Erweiterung

@logo

*Langweilig ... ! Das ist doch kein echtes eingebettetes System!*

> **Aufgabe:** Der Taster schaltet die LED ein und nach 3 Sekunden geht sie von
> selbst wieder aus.

Es wird ernst! Wir müssen den Taster elektrisch mit dem Board verbinden. Anweisungen unter ...

[https://www.mangolabs.de/portfolio-item/micro-switches/](https://www.mangolabs.de/portfolio-item/micro-switches/)

![BildSchalterlogik](images/Microswitch_bb.png)<!-- width="60%" -->

{{1}}
```c               ActivateLed.ino
// Loesung
const int buttonPin = 2;     // Pin des Buttons
const int ledPin =  13;      // Pin der LED

// variables will change:
int buttonState = 0;         // Variable für die Speicherung

void setup() {
  pinMode(ledPin, OUTPUT);
  pinMode(buttonPin, INPUT);
}

void loop() {
  buttonState = digitalRead(buttonPin);
  if (buttonState == HIGH) {
    // turn LED on:
    digitalWrite(ledPin, HIGH);
  } else {
    // turn LED off:
    digitalWrite(ledPin, LOW);
  }
}
```

> **Spezialaufgabe:** Nutzen Sie das kapazitive Tastenfeld für diese Aufgabe

### 3c. Distanzsensor als Input

@logo

*Langweilig ... ! Wir wollen einen echten Sensor!*

> **Aufgabe:** Schalten Sie die LED mittels Ultraschallsensor an und aus
> (distanzabhäniger Lichtschalter)

ACHTUNG: Sie müssen für die Integration des Sensors noch die Bibliothek
`NewPing` installieren. Finden Sie dafür allein einen Weg? Recherchieren sie in
den Arduino Foren zur Frage "How to install a library for Arduino?"

{{1}}
```c               Sonar.ino
// Loesung
#include <NewPing.h>

const int triggerPin = 12;   
const int echoPin = 11;     
const int maxDistance = 400;
const int ledPin =  13;

NewPing sonar(triggerPin, echoPin, maxDistance);

void setup() {
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);
}

void loop() {
  delay(50);
  if ((sonar.ping_cm() < 10) && (sonar.ping_cm() > 0)){
     digitalWrite(ledPin, HIGH);
     Serial.println("Alarm!");
  }
  else
     digitalWrite(ledPin, LOW);
}
```

> **Spezialaufgabe:** Realisiert eine Aktivieren über eine Schallamplitude
> mittels Mikrophon.

### 3d. Es wird bunt

@logo

Integration einer Mehrfarben LED als Erweiterung der Ausgabe

![RGB](images/rgb-farbmodell.png "RGB")<!-- width="60%" -->   [^1]

[^1] https://www.informatikzentrale.de/rgb-farbmodell.html

https://www.mangolabs.de/portfolio-item/rgb-led-2/

<!--
style="height: 60px; display: block; margin-right: auto;"
-->
````
-> Demo:  Demo mit der Mehrfarben Led
````

```c     LedDifferentColors.ino
// Methoden aus dem Lösungsvorschlag der MangoLabs
const int redPin = 11;
const int greenPin = 10;
const int bluePin = 9;

void setColourRgb(unsigned int red, unsigned int green, unsigned int blue) {
  analogWrite(redPin, red);
  analogWrite(greenPin, green);
  analogWrite(bluePin, blue);
}

void setup() {
  // Start off with the LED off.
  setColourRgb(0,0,0);
}

void loop() {
  setColourRgb(255, 0, 0);
  delay(1000);
}
```

> **Aufgabe:** Wechseln Sie die Farben der LED in Abhängigkeit von der Entfernung

{{1}}
```c         ViewDistance.ino
#include <NewPing.h>

const int triggerPin = 12;   
const int echoPin = 11;     
const int maxDistance = 400;

const int redPin = 10;
const int greenPin = 9;
const int bluePin = 8;

void setColourRgb(unsigned int red, unsigned int green, unsigned int blue) {
  analogWrite(redPin, red);
  analogWrite(greenPin, green);
  analogWrite(bluePin, blue);
}

const int ledPin =  13;      // the number of the LED pin

NewPing sonar(triggerPin, echoPin, maxDistance);
// NewPing setup of pins and maximum distance.

void setup() {
  Serial.begin(9600); // Open serial monitor at 9600 baud to see ping results.
  setColourRgb(0,0,0);
}

void loop() {
  int red, green, blue;
  delay(50);                     // Wait 50ms between pings (about 20 pings/sec).
  if ((sonar.ping_cm() <= 10) && (sonar.ping_cm() > 0)){
     Serial.println("Alarm!");
     setColourRgb(255, 0, 0);
  }
  if ((sonar.ping_cm() <= 20) && (sonar.ping_cm() > 10)){
     digitalWrite(ledPin, HIGH);
     Serial.println("Nah dran!");
     setColourRgb(0, 0, 255);
  }
  if ((sonar.ping_cm() <= 30) && (sonar.ping_cm() > 20)){
     digitalWrite(ledPin, HIGH);
     Serial.println("Nah dran!");
     setColourRgb(0, 255, 0);
  }
}
```


### 3e. Servomotor als Ausgabe

@logo

*Immer noch langweilig ... ! Wir wollen einen echten Aktor!*

> **Aufgabe:** Geben Sie die Ausgaben des Distanzsensors mit dem Servomotor aus.
> Entwerfen Sie dazu eine Skale die von "super weit weg" bis "dichter gehts nicht mehr".
> reicht.
https://www.mangolabs.de/portfolio-item/micro-servo/
