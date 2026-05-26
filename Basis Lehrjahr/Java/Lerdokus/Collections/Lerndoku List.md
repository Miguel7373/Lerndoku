```markdown
# Das Interface `List` in Java

- Listen sind geordnet, da die Elemente in einer bestimmten Reihenfolge vorliegen.
- Die Indexierung der Positionen in Listen beginnt bei 0, ähnlich wie bei Arrays.
- Listen haben eine dynamische Größe und können während der Laufzeit Elemente hinzufügen oder entfernen, ohne Lücken zu erzeugen.


Das `List`-Interface bietet eine Vielzahl von Methoden, darunter:

- `size()`: Gibt die Anzahl der Elemente in der Liste zurück.
- `isEmpty()`: Gibt `true` zurück, wenn die Liste keine Elemente enthält.
- `contains(Object o)`: Überprüft, ob die Liste ein bestimmtes Element enthält.
- `get(int index)`: Gibt das Element an der angegebenen Position zurück.
- `set(int index, E element)`: Ersetzt das Element an der angegebenen Position.
- `indexOf(Object o)`: Gibt den Index des ersten Auftretens eines Elements zurück.


**Wichtiger Hinweis:** Da Listen Referenzen auf Objekte enthalten, müssen für primitive Datentypen Wrapper-Klassen wie `Integer`, `Double`, usw. verwendet werden.

Weitere Implementierungen von Listen, wie `ArrayList` oder `LinkedList`, erben von der abstrakten Klasse `AbstractList`, die grundlegende Funktionalitäten bereitstellt.

Die Verwendung von `List` erleichtert die Arbeit mit geordneten Sammlungen und bietet eine breite Palette von Methoden zur Manipulation der Daten.
```

