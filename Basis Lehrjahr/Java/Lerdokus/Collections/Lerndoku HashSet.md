```markdown
# HashSet in Java

Ein `HashSet` in Java, definiert im Paket `java.util`, ist eine gebräuchliche Implementierung des `Set`-Interfaces. Ein `Set` wird verwendet, um eine Menge von Elementen zu speichern, ohne Duplikate zuzulassen. Das `HashSet` speichert die Elemente in einer nicht garantierten Reihenfolge. Hier sind einige wichtige Konzepte und Methoden des `HashSet`:

## Eigenschaften und Methoden:

- **Keine Duplikate:** Ein `HashSet` speichert jedes Element nur einmal. Wenn versucht wird, ein bereits vorhandenes Element erneut hinzuzufügen, wird es nicht dupliziert.
    
- **Einzigartiger Schlüssel:** Die Eindeutigkeit der Elemente wird durch den Schlüssel gewährleistet. Wenn zwei Zuweisungen denselben Schlüssel haben, wird die erste Zuweisung überschrieben.
    

## Elemente abrufen:

Die Elemente eines `HashSet` können mit verschiedenen Methoden abgerufen werden, darunter:

- `iterator()`: Ein Iterator über die Elemente.
- `stream()`: Ein sequentieller Stream über die Elemente.
- `forEach()`: Führt eine bestimmte Aktion über alle Elemente aus.

Die Reihenfolge der Elemente ist nicht garantiert. Es gibt jedoch Implementierungen wie das `SortedSet`, die eine bestimmte Reihenfolge sicherstellen.


### Auslesen der Elemente:


Das `HashSet` bietet eine effiziente Möglichkeit, eindeutige Elemente zu speichern und ist in verschiedenen Anwendungsbereichen nützlich, wo Duplikate vermieden werden sollen.
```