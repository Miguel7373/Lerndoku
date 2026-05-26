#### Pluck 
Pluck holt nicht nur wie `select`, das ganze Objekt aus der Datenbank lädt, kann `pluck` sie direkt im richtigen typen in einen array laden. So kann man vermeiden das man für jeden Eintrag ein eigenes Objekt laden muss wenn man es nicht braucht. Es können auch mehrere Parameter mitgegeben werden dann wirst du ein 2d array erhalten.

````ruby
Person.pluck(:name)

Person.pluck(:name, :nationality)
````


#### Placeholders

Placeholders können super praktisch sein wenn man sie richtig einsetzt sie können dir bei dem einsetzten von variablen in deine Active Record functions helfen.
````ruby 
Person.find_by('name = (?)', Jorah Mormont)

Person.find_by('name = :text', text: 'Jorah Mormont')
````
#### Invert
Um etwas zu invertieren muss man einfach nur ein .not hinter die function schreiben die man invertieren will
````ruby
Person.where.not(name: 'Jorah Mormont')

````

.not to invert

#### find / find_by
Obwohl beide Methoden zum Suchen von Datensätzen verwendet werden, gibt es einen wesentlichen Unterschied in ihrem Verhalten:

- **`find`**: Sucht nach der **Primärschlüssel-ID**. Wenn kein Datensatz mit der angegebenen ID gefunden wird, löst es eine `ActiveRecord::RecordNotFound`-Exception (einen Fehler) aus.
    
- **`find_by`**: Sucht nach beliebigen Attributen. Wenn kein passender Datensatz gefunden wird, gibt es `nil` zurück und verursacht keinen Fehler.
```ruby
person = Person.find(1) 

person = Person.find_by(name: 'Jorah Mormont')
```
#### Order / Sort_by
Beide Methoden sortieren Daten, aber auf unterschiedlichen Ebenen:

- **`order`**: Operiert auf **Datenbankebene (SQL)**. Die Sortierung wird direkt in der SQL-Abfrage mit `ORDER BY` ausgeführt. Dies ist sehr performant, besonders bei grossen Datenmengen.
    
- **`sort_by`**: Operiert auf **Ruby-Ebene**. Zuerst werden alle Daten aus der Datenbank geladen und in einem Array gespeichert. Anschliessend sortiert Ruby dieses Array. Dies kann bei vielen Datensätzen ineffizient sein.

````ruby
Person.order(:name)
Person.all.sort_by(&:name)
````
#### Delete / Destroy
Beide Methoden entfernen Datensätze, aber mit wichtigen Unterschieden bezüglich der Datenintegrität:

- **`delete`**: Entfernt einen oder mehrere Datensätze direkt aus der Datenbank mit einer einzigen SQL `DELETE`-Anweisung. Assoziierte Objekte und `callbacks` (wie `before_destroy`) werden **ignoriert**. Dies ist schneller, aber umgeht die Anwendungslogik.
    
- **`destroy`**: Entfernt einen Datensatz, indem zuerst das Objekt geladen und dann die `destroy`-Methode aufgerufen wird. Dabei werden alle `callbacks` und abhängigen Assoziationen (z.B. `dependent: :destroy`) ausgeführt. Dies ist sicherer, aber langsamer.
```ruby
Person.delete(1)
person = Person.find(1) person.destroy
```

#### Size / Length / Count

Diese drei Methoden geben die Anzahl der Elemente in einer Sammlung zurück, haben aber unterschiedliche Verhaltensweisen:

- **`size`**: Die "intelligenteste" Methode. Wenn die Sammlung bereits geladen ist, gibt sie die Grösse des Arrays zurück (wie `length`). Wenn nicht, führt sie eine effiziente `COUNT`-Abfrage in der Datenbank aus (wie `count`).
    
- **`length`**: Lädt immer die **gesamte Sammlung** von Objekten aus der Datenbank in ein Array und gibt dann dessen Grösse zurück. Dies kann bei grossen Datenmengen sehr speicherintensiv sein.
    
- **`count`**: Führt immer eine `SELECT COUNT(*)`-Abfrage in der Datenbank aus, um die Anzahl der Zeilen zu ermitteln, ohne die Objekte selbst zu laden.
````ruby
people = Person.where(nationality: 'Westeros')
people.size 
people.length
people.count
````
#### Distinct / Uniq
Beide Methoden entfernen Duplikate, aber zu unterschiedlichen Zeitpunkten:

- **`distinct`**: Eine **Datenbankoperation (SQL)**. `DISTINCT` wird der SQL-Abfrage hinzugefügt, sodass die Datenbank von vornherein nur eindeutige Werte zurückgibt.
    
- **`uniq`**: Eine **Ruby-Methode**. Zuerst werden alle Daten (inklusive Duplikate) aus der Datenbank geladen. Anschliessend entfernt Ruby die Duplikate aus dem Ergebnis-Array.
````ruby
Person.distinct.pluck(:nationality) 
Person.pluck(:nationality).uniq
````

[[Active Record| <- Zurück]]
