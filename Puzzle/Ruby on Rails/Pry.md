# Pry is the Goat
![[Pasted image 20260410084443.png]]


Hier ist die aktualisierte Dokumentation, in die alle deine Punkte nahtlos integriert wurden, ohne die bestehende Struktur zu verändern:

# Pry is the Goat

## Gems

#### pry

**What it is:**
Eine interaktive Konsole (REPL), die eine Alternative zu IRB ist, aber zusätzliche Funktionen bietet wie Syntax-Highlighting und bessere Navigation im Code.

##### Was heist REPL

<details>
<summary>Answer</summary>
Read–Eval–Print Loop
</details>

#### pry-byebug

**What it is:**
Eine Erweiterung für pry, mit der man einfacher durch den Code Schritt für Schritt gehen kann. Sie fügt praktische Debugging-Funktionen hinzu, zum Beispiel Breakpoints setzen und mit Befehlen wie next den Code Zeile für Zeile ausführen.

#### pry-rails

**What it is:**
Dieses Gem ersetzt die Standard `rails console` automatisch durch Pry und sorgt für eine tiefere Integration in Rails (z.B. automatischer Support für `binding.pry`).

#### pry-rescue

**What it is:**
Ein mächtiges Tool, das Pry automatisch startet, sobald eine Exception (Fehler) geworfen wird. Extrem hilfreich in Tests oder Hintergrund-Jobs.

-----

## Wie verwendet man Pry überhaupt?

Ich hoffe, das ist kein Schock für euch, aber man benutzt in der Praxis fast nie nur `pry`. Der absolute Standard in Ruby on Rails Projekten ist:

```ruby
pry
```

Du kannst diesen Befehl in fast jeden Teil seines Ruby codes oder sogar in HAML einfügen (Models, Controllers, Services, Jobs).

Sobald der Code an dieser Stelle ausgeführt wird, stoppt das Programm exakt dort und öffnet eine Debugging Konsole. Du kannst dir Variablen anschauen, Methoden testen oder Schritt für Schritt nachvollziehen, was gerade passiert.

-----

## Teil 1: Hilfreich in Controller

### Kontext & Orientierung

| Befehl | Was macht der Befehl? | Wofür beim Debuggen? |
| :--- | :--- | :--- |
| `whereami` Alias `@` Flags: `-s` | Zeigt Datei und Code mit mehr Kontext drumherum. | Um das "Große Ganze" der Methode zu sehen. |
| `ls` Flags: `-g` | Zeigt globale Variablen, Methoden und Konstanten. | Wenn man einen kompletten Überblick braucht. |
| `ls --methods` | Listet nur die verfügbaren Methoden auf. | Um gezielt nach Logik zu suchen. |
| `params` | Zeigt die Request-Parameter. | Sehr wichtig bei Formularen, URLs und IDs. |
| `request.path` | Zeigt den aktuellen Pfad. | Damit du den laufenden Request prüfen kannst. |

### Objekt Navigation

| Befehl | Was macht der Befehl? | Wofür beim Debuggen? |
| :--- | :--- | :--- |
| `cd params` | Wechselt in das `params`-Objekt. | Damit du Parameter einfacher analysieren kannst. |
| `nesting` | Zeigt den aktuellen Kontext-Stack an. | Um zu sehen, wie tief man mit `cd` navigiert ist. |
| `cd ..` | Geht eine Ebene zurück im Objektbaum. | Um aus einem Objekt wieder nach oben zu kommen. |
| `exit` | Verlässt den aktuellen Kontext. | Zurück zur normalen Pry-Ansicht. |

### Dokumentation & Quellcode

| Befehl | Was macht der Befehl? | Wofür beim Debuggen? |
| :--- | :--- | :--- |
| `show-doc Person.unemployed` | Zeigt nur die Dokumentation der Methode. | Perfekt für Rails-Internals oder Gems. |
| `show-source Person.unemployed` | Zeigt den echten Ruby-Code der Methode. | **Sehr stark:** Du springst direkt in die Business Logic. |
| `find-method unemployed` | Findet, wo die Methode definiert ist. | Wenn du nicht weisst, woher etwas kommt. |

-----

## Teil 2: Voralem hinfreich in Models

### Kontext

| Befehl | Was macht der Befehl? | Wofür beim Debuggen? |
| :--- | :--- | :--- |
| `whereami` | Zeigt den Scope-Code. | Damit man sieht, dass man jetzt im Model ist. |
| `self` | Zeigt aktuelles Objekt / Klasse. | Hier zeigst du, dass du jetzt im `Person`-Kontext bist. |
| `ls` | Zeigt Methoden der Klasse. | Sehr gut für die Objektanalyse. |

### Step Debugging (via pry-byebug)

| Befehl | Was macht der Befehl? | Wofür beim Debuggen? |
| :--- | :--- | :--- |
| `break` | Erlaubt es, neue Breakpoints live zu setzen. | Um an späteren Stellen im Code zu stoppen. |
| `step` | Geht in die nächste Methode *hinein*. | Wenn du tiefer in Rails / ActiveRecord eintauchen willst. |
| `next` | Springt zur nächsten Zeile. | Sauberes Durchlaufen des Codes ohne abzutauchen. |
| `finish` | Beendet die aktuelle Methode. | Wenn du aus tiefem Code wieder heraus willst. |
| `continue` | Läuft bis zum nächsten Breakpoint weiter. | Um weite Strecken im Code zu überspringen. |

### Stack Analyse

| Befehl | Was macht der Befehl? | Wofür beim Debuggen? |
| :--- | :--- | :--- |
| `backtrace` | Zeigt die Aufrufkette (Stacktrace). | Wie kam Rails hierher? |
| `up` | Springt eine Ebene höher im Stack. | Um den Caller anzuschauen (Debugger-Core). |
| `down` | Springt eine Ebene tiefer im Stack. | Zurück in die aktuelle Methode. |
| `frame 0` | Zur Hauptposition springen. | Um den Stack sauber zu navigieren. |

-----

### Zurück zum Controller (Pry 1)

> Führe `continue` aus, um das Programm fortzusetzen. Pry verlässt das Model und hält wieder im Controller an.

| Befehl | Was macht der Befehl? | Wofür beim Debuggen? |
| :--- | :--- | :--- |
| `@unemployed_people` | Zeigt das Resultat der Query. | Perfekt, um zu zeigen, was geladen wurde. |
| `cd @unemployed_people.first`| Wechselt ins erste Objekt der Collection. | **Sehr stark** für Live-Objektanalyse. |
| `exit` | Verlässt den Objekt-Kontext. | Zurück in den Root-Kontext des Controllers. |
| `exit-program` | Beendet die gesamte App/Server sofort. | Wenn man den Prozess hart abbrechen muss. |

-----

## Teil 3: Destroy Action (Pry 3)

### Fehler Demo

| Befehl | Was macht der Befehl? | Wofür beim Debuggen? |
| :--- | :--- | :--- |
| `nil.name` | Erzeugt absichtlich einen Fehler. | Zum Demonstrieren der Fehleranalyse in Pry. |
| `wtf?` | Zeigt den letzten Fehler inkl. Stacktrace. | **Sehr eindrucksvoll** in einer Demo. |

### History & Shell-Integration

| Befehl | Was macht der Befehl? | Wofür beim Debuggen? |
| :--- | :--- | :--- |
| `hist -10` | Zeigt die letzten 10 Befehle. | Zur Rekonstruktion der Debug-Session. |
| `save-history file.txt` | Speichert den Verlauf in eine Datei. | Um komplexe Befehlsfolgen zu dokumentieren. |
| `.git status` | Zeigt den Git-Status. | Ein cooler Bonus-Trick\! |
| `clear-screen` | Leert die Konsole. | Sorgt für einen sauberen Abschluss. |

## Hilfestellungen

Ihr könnt immer den befehl `help` in pry schreiben dann bekommt ihr alle befehle

# Links

[https://github.com/pry/pry](https://github.com/pry/pry)