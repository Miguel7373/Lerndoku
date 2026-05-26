
## Einführung

Bean Validation ist ein Standard in der Java-Welt, um Daten auf einfache und deklarative Weise zu validieren. In Spring Boot lässt sich dieser Mechanismus nahtlos integrieren, um sicherzustellen, dass Eingabedaten korrekt sind, bevor sie weiterverarbeitet werden.

---

## Was ist Bean Validation?

Bean Validation basiert auf dem JSR-Standard (z. B. JSR 380 – Bean Validation 2.0). Dabei werden Java-Annotationen verwendet, um Validierungsregeln direkt an Feldern oder Methoden zu definieren.

Spring Boot nutzt in der Regel **Hibernate Validator** als Implementierung.

**Beispiel:**
````java
public class Member {

@NotNull
@Size(min = 2, max = 50)
private String name;

@Email
private String email;

@Min(18)
private Integer age;

}
````

Diese Annotationen sorgen dafür, dass die Felder den angegebenen Regeln entsprechen.