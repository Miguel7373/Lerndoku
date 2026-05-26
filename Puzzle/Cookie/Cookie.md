### HttpOnly Flag
Das `HttpOnly`-Flag hilft, Cookies vor dem Zugriff durch clientseitige Skripte (z.B. JavaScript) zu schützen. Wenn der Browser dieses Flag nicht unterstützt, wird es einfach ignoriert. Das bedeutet, dass der Cookie nicht zugänglicher wird, aber auch nicht den zusätzlichen Schutz erhält.

Beispiel
```java
// beim erstellen
cookieBuilder.httpOnly(true);
// beim testen
Assertions.assertTrue(cookieHeader.contains("HttpOnly;"));
```

-----------------------------------------------------------------------------------
### Secure Flag
Das `Secure`-Flag sorgt dafür, dass Cookies nur über sichere Verbindungen (HTTPS) gesendet werden. Wenn der Browser das Flag unterstützt, werden keine Cookies über unsichere HTTP-Verbindungen übertragen. Dies trägt dazu bei, die Vertraulichkeit der Cookie-Daten zu wahren.

Beispiel
```java
// beim erstellen
cookieBuilder.secure(true);
// beim testen
Assertions.assertTrue(cookieHeader.contains("Secure;"));

```

### SameSite Flag

Das `SameSite`-Flag verhindert, dass Cookies bei Cross-Site-Anfragen (z.B. von einer anderen Domain) gesendet werden. Dadurch wird das Risiko von CSRF (Cross-Site Request Forgery)-Angriffen verringert. Es gibt drei mögliche Werte:

- **Strict**: Das Cookie wird nur bei Anfragen gesendet, die von derselben Site stammen. Cross-Site-Anfragen senden das Cookie nicht mit.
- **Lax**: Das Cookie wird bei Cross-Site-GET-Anfragen gesendet (wie beim Klick auf einen Link), aber nicht bei POST- oder anderen Anfragen.
- **None**: Das Cookie wird immer gesendet, unabhängig von der Herkunft der Anfrage (sollte jedoch nur mit `Secure` verwendet werden).
  
Beispiel
```java
// Beim erstellen
cookieBuilder.sameSite("Strict"); 
// Beim Testen 
Assertions.assertTrue(cookieHeader.contains("SameSite=Strict"));
```

### Max-Age Flag

Das `Max-Age`-Flag gibt die Lebensdauer eines Cookies in Sekunden an. Nach Ablauf dieser Zeit wird das Cookie ungültig und vom Browser gelöscht. Im Gegensatz zu `Expires`, das ein festes Datum verwendet, ist `Max-Age` eine relative Zeit.

Beispiel
```java
// Beim erstellen
cookieBuilder.maxAge(3600); 
// Beim Testen 
Assertions.assertTrue(cookieHeader.contains("Max-Age=3600"));
```


Die Flag ist imposant da sie sowohl die UX als auch die Security verbessert da ein Cookie das nie ausläuft und sensitive Daten hat über lange Zeit als Angriffs Fläche dienen kann. Außerdem ist es ein gesetzt das der Cookie consent manchmal erneuert werden muss.