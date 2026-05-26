

### General
#### Was ist Active Record
Active Record ist ein [[ORM]] somit bietet es verschiedene [[Methods|Methoden]] die dann in SQL query's umgeschrieben werden und dann in deiner Datenbank ausgeführt werden. Somit ist Active Record extrem angenehm zum entwickeln auch wenn es bei extrem komplexen SQL query's immer noch sinn machen kann sie selbst zu schreiben.

#### Performance
Bei der Performance solltest du auf zwei Sachen achten 
Erstens: 
	Du solltest immer wenn möglich die Daten auf Datenbank ebene sortieren oder filtern da es die Performance deutlich steigert. Somit musst du die Richtigen [[Methods|Methoden]] wählen da sie teilweise das selbe machen nur eines in Ruby und das andere in der Datenbank.
Zweitens:
	 Du solltest schauen das du sowenige SQL statements wie möglich an die Datenbank schicken also wenn du kannst solltest du immer Alles auf so wenige Query's reduzieren wie nur möglich und somit auch 
	 [[n + 1 query's]] umgehen








