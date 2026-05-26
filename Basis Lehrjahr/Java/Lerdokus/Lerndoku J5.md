```markdown
**Zusammenfassung zu Exception Handling in Java:**

- **Schlüsselwörter:** 
  - `try`, `catch`, `finally`, `throw`, `throws`

- **Exception-Typen:**
  - `Error`: Nicht reparierbare Laufzeitfehler oder Hardware-Probleme.
  - `Exception`: Fehler oder unerwartete Ereignisse während der Ausführung.

- **Arten von Exceptions:**
  - `Unchecked Exceptions`: Laufzeitfehler, nicht vom Compiler erkannt.
  - `Checked Exceptions`: Vom Compiler erkannte Fehler zur Kompilierungszeit.

- **Beispiel für Exception Handling:**
  - Vermeidung von `NullPointerException` durch Null-Checks oder Optionals.

- **`try` / `catch` / `finally`:**
  - `try`-Block für Code mit potenziellen Exceptions.
  - `catch`-Block für die Behandlung von Exceptions.
  - `finally`-Block für Code, der immer ausgeführt wird.

- **`throw` / `throws`:**
  - `throw`: Werfen eigener Exceptions.
  - `throws`: Kennzeichnen, dass die aufrufende Komponente die Exception abhandeln muss.

- **Umwandlung von Laufzeitfehlern in Checked Exceptions:**
  - Verwendung von eigenen Exception-Klassen und `throws`.

- **Multi-Catch:**
  - Behandlung mehrerer Exceptions in einem `catch`-Block seit Java 7.

- **Try-With-Resources:**
  - Automatisches Ressourcen-Management seit Java 7.
  - Vermeidet expliziten `finally`-Block durch `AutoCloseable` und `Closeable` Interfaces.

- **Null-Safety:**
  - Vermeidung von `NullPointerException` durch Null-Checks, Annotationen (`@NotNull`, `@Nullable`) und Optionals.

Diese Punkte decken die Grundlagen des Exception Handling in Java ab.
```