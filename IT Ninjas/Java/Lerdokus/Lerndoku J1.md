````markdown
# Java-Variablen

- **Variablen** in Java dienen dazu, Werte zu speichern.
- Eine Variable muss **deklariert** und optional **initialisiert** werden.
- Die Deklaration erfolgt mit dem **Typ** und dem **Variablennamen**.

- Die **Initialisierung** erfolgt durch das Zuweisen eines Werts während der Deklaration.


- Variablennamen sollten mit einem **Kleinbuchstaben** beginnen und können Buchstaben, Zahlen, `$` und `_` enthalten.

# Datentypen in Java

- Java verwendet **starke Typisierung**, wodurch Variablen einen Datentyp haben müssen.
- Es gibt zwei Arten von Datentypen: **primitive Datentypen** und **Referenztypen**.

## Primitive Datentypen

Die wichtigsten primitiven Datentypen in Java sind:

- `byte`
- `short`
- `int`
- `long`
- `float`
- `double`
- `boolean`
- `char`

Die Wahl des richtigen Datentyps hängt von der Art der Daten ab.

## Kontrollstrukturen in Java

- **Kontrollstrukturen** steuern den Programmfluss in Java und umfassen bedingte Anweisungen, Schleifen und die Switch-Anweisung.

## Mathematik & Logik in Java

- Java bietet eine Vielzahl von **arithmetischen Operatoren**, **Vergleichsoperatoren**, **Boolsche Operatoren** und den **Ternary Operator** zur Durchführung von Berechnungen und Bedingungsprüfungen.

## Referenztypen in Java

- **Referenztypen** speichern nicht direkt Werte, sondern Verweise auf den Speicherort der Daten.
- Es gibt zwei Hauptarten: **Objektdatentypen** und **Arrays**.

## Scanner-Klasse

Die Scanner-Klasse in Java ermöglicht die Erfassung von Benutzereingaben von der Konsole. Die grundlegende Verwendung sieht wie folgt aus:

# Arrays in Java

- Arrays speichern zusammengehörige Variablen desselben Datentyps.
- Die Deklaration eines Arrays umfasst Datentyp, eckige Klammern und Namen.
- Die Initialisierung erfolgt mit der Größenangabe oder direkter Wertezuweisung.
- Die Länge eines Arrays wird mit `.length` überprüft, und die Indizes beginnen bei 0.
- Elemente werden über den Index zugegriffen und geändert.
- Arrays können mithilfe von Schleifen durchlaufen werden.
- Zweidimensionale Arrays (2D) eignen sich für tabellarische Daten.

# Statische und Nicht-Statische Elemente

- Statische Elemente existieren einmal pro Klasse, nicht an Objekte gebunden.
- Nicht-statische Elemente sind objektspezifisch.
- Statische Methoden können über den Klassennamen aufgerufen werden und sind in Utility-Klassen nützlich.
- Utility-Klassen sollten `final` und einen privaten Konstruktor haben.

Die Verwendung von `static` sollte je nach Anwendungsfall und Funktionalität entschieden werden. Static ist gut für gemeinsame Funktionen und Konstanten, während nicht-statische Elemente für objektspezifische Daten und Verhalten verwendet werden.
````
