## Beschreibung

Diese Klasse stellt einen **konfigurierten `ObjectMapper`** bereit, der für die Serialisierung und Deserialisierung von JSON in Java-Objekte verwendet wird.

Der `ObjectMapper` ist vorkonfiguriert mit:

- Unterstützung für Java 8 Zeit-API (`JavaTimeModule`)
    
- Datums- und Zeitangaben werden **nicht** als Timestamps geschrieben, sondern im ISO-Format.
    

Du kannst den `ObjectMapper` bei Bedarf anpassen, indem du zusätzliche Module registrierst oder Features ein- bzw. ausschaltest.

## Code-Beispiel

```java
private static final ObjectMapper objectMapper = createCustomObjectMapper();

private static ObjectMapper createCustomObjectMapper() {
    ObjectMapper mapper = new ObjectMapper();
    
    mapper.registerModule(new JavaTimeModule());
    
    // Datums- und Zeitangaben als lesbares ISO-Format, nicht als Timestamp
    mapper.disable(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS);
    
    // Beispiel: Weitere Features anpassen
    // mapper.enable(SerializationFeature.INDENT_OUTPUT); // Schön formatierte JSON-Ausgabe
    // mapper.disable(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES); // Unbekannte Properties ignorieren

    return mapper;
}
}