Fun Mise on Place
Makes the rat move across screen
```bash
alias mice='for ((i=1; i<=$COLUMNS; i++)); do printf "\r%*s" $i ".=.>"; sleep 0.01; done; tput cr; tput el; mise'
```

**`tput cr`** → setzt den Cursor an den Anfang der Zeile.
**`tput el`** → löscht die aktuelle Zeile vom Cursor bis zum Ende.


Hier wird in `U` die Remote-URL gespeichert, dann auch noch der Basename. 
Dann bin ich aus dem Directory verschoben und dann habe ich alles entfernt und neu geklont.

```ruby
reclone() {
u=$(git remote get-url origin) || return
d=$(basename "$(git rev-parse --show-toplevel)") || return
cd .. && rm -rf "$d" && git clone "$u"
}
```





### Grep

RegEx Notation

- `^` Markiert den Zeilenanfang
- `$` Markiert das Zeilenended
- `.` Markiert ein beliebiges Zeichen
- `( )` Markiert eine Zeichengruppierung
- `{ n }` Quantifiziert einen vorhergehenden Ausdruck n-mal
- `?` Quantifizierung für “höchstens einmal”
- `*` Quantifizierung für “null oder mehrmals”
- `+` Quantifizierung für “ein oder mehrmals”


-E flag gibt grep die erweiterten funktionen frei

```bash
grep -E '(Linux|TEST)'
```

```bash
grep -Eo '^[a-z]*'
```

```bash
grep -E '(zz)+'
```


### Sed 

Sed without any attribute just give back the input

```bash
$ echo "who stole my cookies?" | sed ''
who stole my cookies?
```



```bash
$ sed '' sample.txt
puzzle
puzzle itc
PUZZLE TEST
hello puzzle member
Linux is great
tux
unix
Preferita is my favourite pizza
asdfasdf
öäü///
```



But when you enter 'p' it prints the intput once if you dont use the '-n' flag that surpresses the deafult output you will now see everything double


With a number infront of the p you can manipulate how much you print

```bash
$ sed -n '3p' sample.txt
PUZZLE TEST

$ sed -n '1,4p' sample.txt
puzzle
puzzle itc
PUZZLE TEST
hello puzzle member

$ sed -n '2,+4p' sample.txt
puzzle itc
PUZZLE TEST
hello puzzle member
Linux is great
tux

$ sed -n '1~2p' sample.txt
puzzle
PUZZLE TEST
Linux is great
unix
asdfasdf
```




## journalctl
This tool controles most of you loggs

Flags :
	-b seit dem letzten boot
	 -p prioritäten dann kannst du err oder so dahinter schriben um alle erros zu begommen
	- u um einen service anzugeben nachdem du suchen willst
	- f um ab jetzt alles anzuzeigen
	- r um die neusten loggs zuerst zu zeigen






### DU

Zeight specherplatz von allen files immer mit -h verwenden um die grössen zu sehen




## Network

#### Arping
Versuch wert wenn der ping nicht geht

#### telnet
mit telnet und dann die url und der port kannst du sehen ob der port offen ist

#### ss

Der befehl 
```bash
ss -tulpn
```
Kann man sehen wer auf welchen port hört gerade


## nmap

Nmap ist ein Port und Vulnerability Scanner. Er liefert Informationen, wie z.B. ob ein Server erreichbar ist, welche Ports offen sind und Auskunft über verwendete Softwareversionen.

```bash
nmap odoo.puzzle.ch
```

Vulnerability scan:
```bash
nmap -Pn --script vuln 192.168.1.100
```


| IPv4           | IPv6                 |
| -------------- | -------------------- |
| Dezimal        | Hexadezimal          |
| 32 Bit Numbers | 128 Bit alphabetisch |
| IPsec optional | IPsec standart       |
|                |                      |
Heisst das die adressen eifach nicht so knapp werden und grudsätzlich immer sicher sind
Dafür kann man sich die adressen nicht merken oder halt nur schwer