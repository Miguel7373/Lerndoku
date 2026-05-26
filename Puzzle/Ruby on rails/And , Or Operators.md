

### Ruby hat zwei Arten von logischen Operatoren Einmal ausgeschriebenen `and`, `or` und dann noch die normalen Logischen Operatoren `||`, `&&`


#### Vergleich zu Java Operatoren
Die ausgeschriebenen Operatoren sind NICHT! Mit den `|` `&` Operatoren von anderen Programmierarten zu verglichen. Da die Operatoren mit nur einem Zeichen nur Bitweise überprüfen.

| Operatoren | Beschreibung                                                                                                                            |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `&`        | Beim bitweisen Und wird eine „1“ produziert, sofern beide Operanden ebenfalls „1“ sind. Trifft dies nicht zu, wird eine „0“ ausgegeben. |
| `\|`       | Das bitweise Oder produziert dann eine „1“, wenn auch einer der beiden Operanden a und b „1“ ist.                                       |


#### Nun zu den In Ruby vorhanden Operatoren

###### Die Normalen logischen Operatoren



| Operatoren | Beschreibung                                                                                     |
| ---------- | ------------------------------------------------------------------------------------------------ |
| `&&`       | Logisches **Und**: Gibt `true` zurück, wenn **beide** Operanden wahr sind. Andernfalls `false`.  |
| `\|\|`     | Logisches **Oder**: Gibt `true` zurück, wenn **mindestens einer** der beiden Operanden wahr ist. |
###### Die Ausgeschrieben Operatoren

| Operatoren | Beschreibung                                                                                                                        |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `and`      | Funktioniert wie `&&`, hat jedoch eine **niedrigere Priorität** bei der Auswertung. Wird häufig zur Kontrolle von Abläufen genutzt. |
| `or`       | Funktioniert wie `\|`, aber ebenfalls mit **niedrigerer Priorität**. Praktisch z. B. bei Zuweisungen oder in Kontrollstrukturen.\|  |


Or und And sind nicht oft verwend bar da sie durch die niedrige prio Fehler hervorholen kann.