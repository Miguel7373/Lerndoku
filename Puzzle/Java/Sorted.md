### .sorted()
- Sortiert die Elemente eines Streams in natürlicher Reihenfolge (z.B. alphabetisch bei Strings, aufsteigend bei Zahlen).

### Benutzerdefinierter Comparator:
 - Ermöglicht es, eine eigene Sortierlogik anzugeben (z.B. absteigend, nach Länge von Strings).

- Beispiele:
  `zahlen.stream().sorted(Comparator.reverseOrder())`
  `namen.stream().sorted(Comparator.comparingInt(String::length))