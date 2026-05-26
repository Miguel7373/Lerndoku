### Was ist `it`?

`it` ist ein **Kurzschreibweise für Blockparameter** (ab Ruby 3.4).  
Es steht automatisch für das **erste Argument**, das an einen Block übergeben wird.

Anstatt noch ein Objekt zu machen wie hier:
```
operators.values.map { |op| op.downcase.to_sym }
````
Kannst du `it` verwenden:
```
operators.values.map { it.downcase.to_sym }
```

### Achtung
Du solltes dies nur in block fällen verwenden
Ebenfalls nur wenn klar ist das was `it`  sein sollte.



