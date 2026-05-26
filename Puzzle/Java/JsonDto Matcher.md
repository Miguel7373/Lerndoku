Normalerweise hat man in einem Projekt viele redundante Codezeilen, um die Controller-Response mit den Attributen des DTOs abzugleichen — also zu prüfen, ob die erwarteten Werte mit der tatsächlichen Antwort übereinstimmen.  
Das lässt sich aber auch generisch lösen.

Du kannst eine Funktion schreiben, die das Ergebnis (`result`) entgegennimmt und automatisch den Vergleich durchführt:
``` java
 public static ResultMatcher matchesDto(Object expectedDto, String jsonPrefix) {  
    return result -> {  
        JsonNode expectedNode = objectMapper.valueToTree(expectedDto);  
        matchJson(expectedNode, jsonPrefix, result);  
    };  
}
```

Hier wird das `result` abgefangen (vom Typ `MvcResult`) und anschließend weitergegeben, um den Abgleich mit dem erwarteten DTO vorzunehmen.


Dann kannst du das Ganze nach den verschiedenen Typen sortieren. Was du musst, da du sonst durch den [[Custom ObjectMapper]] noch nicht die JSON-Value zu dem dazu gegebenen DTO messen kannst.

``` java
private static void matchJson(JsonNode expected, String pathPrefix, MvcResult result) throws Exception {  
    if (expected == null || expected.isNull())  
        return;  
    switch (expected.getNodeType()) {  
        case OBJECT -> {  
            Iterator<String> fieldNames = expected.fieldNames();  
            while (fieldNames.hasNext()) {  
                String field = fieldNames.next();  
                matchJson(expected.get(field), pathPrefix + "." + field, result);  
            }  
        }  
        case ARRAY -> {  
            for (int i = 0; i < expected.size(); i++) {  
                matchJson(expected.get(i), pathPrefix + "[" + i + "]", result);  
            }  
        }  
        case BOOLEAN -> jsonPath(pathPrefix).value(expected.booleanValue()).match(result);  
        case NUMBER -> jsonPath(pathPrefix).value(expected.longValue()).match(result);  
        case NULL -> jsonPath(pathPrefix).doesNotExist().match(result);  
        default -> jsonPath(pathPrefix).value(expected.asText()).match(result);  
    }  
}
``` 

Wie man beim Objekt sehen kann, ist hier noch eine Rekursion eingebaut. Denn wenn man ein Objekt in den DTO getestet hat, ist der JSONPath natürlich nicht einfach gleich. Er ist weiter eingebettet und man kann somit dieselbe noch einmal aufrufen, damit man alle Objekte abfängt und richtig testet. 

Somit können so alle Attribute, die ein DTO hat (inklusive Subklassenattribute), getestet werden.