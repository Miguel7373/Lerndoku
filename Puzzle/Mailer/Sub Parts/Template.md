[[Active Mailer|<- Zurück]]

Dein Template muss in zwei Formen vorhanden sein. Einmal in einem HTML-File und einmal in einem Text-File, damit auch die E-Mail-Clients, die kein HTML rendern können. Deshalb hat es der Rails Mailer folgendermassen aufgebaut:

##### Allgemeine Templates
Hier werden alle Einstellungen und Anteile, die du in allen deinen Mail-Templates brauchst, angewendet. Diese Files findest du im `layout`-Ordner bei den Views.
###### HTML
Hier werden meist deine Meta-Tags und auch deine CSS-Klassen
```haml
!!!
%html
  %head
    %meta{:content => "text/html; charset=utf-8", "http-equiv" => "Content-Type"}/
    :css
      body{
	      padding: 10px
      }
```

Allerdings kannst du hier auch deinen Header oder Footer einbinden, denn alles, was du hier hinschreibst, wird auf allen spezifischen Mail-Templates auch angezeigt.

Bei Bildern musst du immer die Webseiten-URL angeben, wo man es genau findet. Das Bild sollte also irgendwo online findbar sein. Auch wenn es nur auf deiner Seite angezeigt wird, kannst du mit «Bild öffnen mit Link» den richtigen Pfad bekommen.
```haml
%img.logo{src: "https://skills.puzzle.ch/assets/logo.svg", alt: "Skills Logo"}
```

Auch hier musst du aber noch von dem spezifischen Template den Content reingeben.
```haml
= yield
```
###### Text
Hier wird meist nur ein 
```text
= yield
```
Reingeschrieben, da du bei Text nicht viel anderes Relevantes beiführen musst.

Natürlich kannst du hier über oder unter auch eine Art Header oder Footer des Mails schreiben, damit du es in allen Mails hast.
##### Spezifische Templates
Das Hier ist das Template das dann mit dem `yield` dazu geladen wird.
Welche spezifischen Templates genommen werden, kommt auf die Methode in deiner Mailer-Klasse an. Denn die sollten dir ebenfalls unter dem Ordner `mailer` bei den Views generiert worden sein.
###### HTML
Hier sollte der Body von deinem Mail sein, also ein mit einfachen HTML-Tags gestalteter Body des Mails, erstellt werden.

```haml
%h2 Dein Skills-Profil wartet auf Sie

%p
	Hallo,
```


Du kannst auch URLs generisch hinzufügen, denn anders als die nicht unterstützten Methoden mit `example_path` kannst du `example_url` aufrufen, was dir die ganze URL des angegebenen Komponenten gibt.
```haml
%a.button{href: people_url} Profil jetzt aktualisieren
```
###### Text
Hier kommt einfach dein Text, den du senden wolltest.

[[Active Mailer|<- Zurück]]