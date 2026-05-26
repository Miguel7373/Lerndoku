main 
neew Game OB
Game.character1.add(player 1)
"" p2""
(Shop für p1) - > In inventar...
"" p2""

Game.FightingKlass.doFight






- Package: Spielfiguren
  - Abstrakte Klasse: Spielfigur
    - Instanzvariablen: Name, Lebenspunkte, Tragkraft,
    - Methoden:
      - get und sett alles
  - Klasse: Mensch (erweitert Spielfigur)
  - Klasse: Zwerg (erweitert Spielfigur)
  - Klasse: Elf (erweitert Spielfigur)
    - Instanzvariable: Zauberwert
    - getKampfwert() (spezialisiert)
  - Klasse: Ork (erweitert Spielfigur)
    - Spezialisierungen: Kampfrausch
  - Klasse: Goblin (erweitert Spielfigur)
  - Klasse: Troll (erweitert Spielfigur)
    - Spezialisierungen: Kampfwert mit Keule
  - Klasse: Rüstung(erweitert Items)
    - Instanzvariablen:  Schutzwert
- Package: Waffen
  - Abstrakte Klasse: Waffe
    - Instanzvariablen: Angriffswert, Verteidigungswert
    - Methoden:
      - getKampfwert()
  - Klasse: Nahkampfwaffe (erweitert Waffe)
  - Klasse: Schwert (erweitert Nahkampfwaffe)
  - Klasse: Keule (erweitert Nahkampfwaffe)
  - Klasse: Fernkampfwaffe (erweitert Waffe)
  - Klasse: Bogen (erweitert Fernkampfwaffe)
  - Klasse: Wurfmesser (erweitert Fernkampfwaffe)
- Package: Gegenstände
  - Abstrakte Klasse: Gegenstand
    - Instanzvariablen: Bezeichnung, Gewicht
  - Klasse: Trank (erweitert Gegenstand)
    - Instanzvariable: Lebenspunkte, Stärkewert
  - Klasse: Zauberring (erweitert Gegenstand)
    - Instanzvariable: Kraftring, Schutzring
- Package: Kampf
  - Klasse: KampfManager
    - Methoden:
      - starteKampf()
      - zähleRunden()
      - verrechneSchaden()
      - ermittleGewinner()
  - Klasse: Initiative
    - Instanzvariable: Initiative-Wert
    - Beeinflussung durch Rüstung und schwere Rüstung
Package GameMech

Menu Klass
Prints
Shop









```
- Package: Spielfiguren
  - Abstrakte Klasse: Spielfigur
    - Instanzvariablen: Name, Lebenspunkte, Tragkraft, Waffe, Gegenstände, Rüstung, Initiative-Wert
    - Methoden:
      - getKampfwert()
      - benutzeGegenstand()
      - trageRüstung()
  - Klasse: Mensch (erweitert Spielfigur)
  - Klasse: Zwerg (erweitert Spielfigur)
  - Klasse: Elf (erweitert Spielfigur)
    - Instanzvariable: Zauberwert
    - getKampfwert() (spezialisiert)
  - Klasse: Ork (erweitert Spielfigur)
    - Spezialisierungen: Kampfrausch
  - Klasse: Goblin (erweitert Spielfigur)
  - Klasse: Troll (erweitert Spielfigur)
    - Spezialisierungen: Verdoppelter Kampfwert mit Keule
									
- Package: Gegenstände
  - Abstrakte Klasse: Gegenstand
    - Instanzvariablen: Bezeichnung, Gewicht
	- Package: Waffen
		- Abstrakte Klasse: Waffe
	    - Instanzvariablen: Angriffswert, Verteidigungswert,
	    - Methoden:
	      - getKampfwert()
	  - Klasse: Nahkampfwaffe (erweitert Waffe)
		  - Klasse: Schwert (erweitert Nahkampfwaffe)
		  - Klasse: Keule (erweitert Nahkampfwaffe)
	  - Klasse: Fernkampfwaffe (erweitert Waffe)
		  - Klasse: Bogen (erweitert Fernkampfwaffe)
		  - Klasse: Wurfmesser (erweitert Fernkampfwaffe)
	- Packet Trank 
		- Klasse: Trank (erweitert Gegenstand)
		    - Instanzvariable: Lebenspunkte, Stärkewert
	- Packet Zauberring
		- Klasse: Zauberring (erweitert Gegenstand)
		    - Instanzvariable: Kraftring, Schutzring
	- Packet Rüstung
		- Klasse: Rüstung
		  - Instanzvariablen: Schutzwert
									
- Package: Kampf
  - Klasse: KampfManager
    - Methoden:
      - starteKampf(Spielfigur spielfigur1, Spielfigur spielfigur2)
      - zähleRunden()
      - verrechneSchaden()
      - ermittleGewinner()
									
- Package: Fighter
	- Klasse Fighter
		- NurfBuffHuman
		- nurfBuffOrc
		- ...
									
```
      - Instanzvariable: Initiative-Wert
      - Beeinflussung durch Rüstung und schwere Rüstung







![[role play.canvas]]