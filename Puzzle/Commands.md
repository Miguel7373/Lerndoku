
Mit diesen Befehlen können Sie einstellen, wie lange Ihr Computer untätig sein darf, bevor der Bildschirm schwarz wird oder in den Ruhezustand geht. Man nennt das die "Inaktivitätsverzögerung". Sie bestimmen also, wie lange der Computer warten soll, wenn Sie gerade nichts machen.

Hier sind die Befehle, die man dafür verwenden können:
- **Um die Wartezeit auf 2 Stunden einzustellen:** Dieser Befehl sagt dem System, dass es 7200 Sekunden warten soll, bevor es reagiert. 7200 Sekunden sind genau 2 Stunden.
	`gsettings set org.gnome.desktop.session idle-delay 7200`

- **Um die Wartezeit unbegrenzt einzustellen:** Mit dem Wert 0 sagen Sie dem System, dass es gar nicht automatisch auf Inaktivität reagieren soll, was die Wartezeit praktisch unendlich macht.
	`gsettings set org.gnome.desktop.session idle-delay 0`
	
- **Um zu sehen, wie die aktuelle Wartezeit eingestellt ist:** Dieser Befehl zeigt Ihnen die Zahl in Sekunden an, die gerade als Wartezeit eingestellt ist.
	`gsettings get org.gnome.desktop.session idle-delay`



```docker exec -it rails bash```
wird verwendet um in den Kontext des laufenden rails containers. dort kannst du dann in die rails console. wenn du es in dem exec machst kannst du dir sicher sein das du alle Konfigurationen so hast wie sie im code stehen.