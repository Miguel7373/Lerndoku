# **Lerndokumentation: HTTP‑Interceptor in Angular – TechTalk Edition**

## 1. Was sind Interceptor in Angular?

Bevor ein Request das Backend trifft – oder eine Response zu deiner App zurückkommt – kann ein Interceptor sich dazwischenwerfen und Dinge anpassen, loggen oder komplett übernehmen.

Stell dir den Interceptor‑Flow wie einen Flughafen‑Security‑Check vor:

- Jeder Request geht durch eine Pipeline
    
- Jeder Interceptor kann reinschauen
    
- Manche lassen ihn direkt durch
    
- Andere scannen, repacken, labeln oder blocken
    

Und das Beste: Deine Services bleiben clean.

### Typische Einsatzbereiche

- **Zentrales Error‑Handling**
    
- **Erfolgsmeldungen automatisieren**
    
- **HTTP‑Logging / Monitoring**
    
- **Request‑ oder Response‑Transformationen** 
    
---

## 2. Wie funktionieren Interceptor?

Angular benutzt eine chain‑basierte Architektur: Jeder Interceptor reicht den Request mit `next(req)` weiter – oder verändert ihn davor. Das Gleiche passiert beim Rückweg der Response.

### Die Pipeline:

**Request → Interceptor 1 → Interceptor 2 → Backend → Interceptor 2 → Interceptor 1 → Response**

Jeder Interceptor:

1. **modifiziert den Request** (Header, Body, URL)
    
2. **entscheidet, ob der Request weitergereicht wird**
    
3. **fängt die Response ab** und kann sie transformieren
    
4. **handelt Errors zentral**, bevor sie die Komponente erreichen
    

Der grosse Vorteil: Jeder Interceptor hat eine definierte Rolle, und zusammen werden sie zu einem mächtigen HTTP‑Framework.

---

## 3. Aufbau eines Interceptors

Ganz minimalistisch:

```ts
export const successInterceptor: HttpInterceptorFn = (req, next) => {
  return next(req);
};
```

Aber wir wollen natürlich _mehr Power_. Also werfen wir einen Blick auf deine echten Interceptor.

---

## 4. Der **Success‑Interceptor** – Automatische Erfolgsmeldungen

Dieser Interceptor sorgt dafür, dass **jede erfolgreiche Nicht‑GET‑Operation** eine automatisch übersetzte Erfolgsmeldung anzeigt.

### Key Features

- GET‑Requests werden ignoriert (macht UX‑mässig Sinn)
    
- Erfolgreiche Responses triggern einen Toast
    
- Dynamische und intelligente Übersetzung via `ScopedTranslationService`
    
- Extrahiert anhand der URL das betroffene Objekt
    

### Code‑Snippet: Success Logic

```ts
if (event instanceof HttpResponse && event.ok) {
  const message: string = translate.instant(req.method, {
    OBJECT: translate.instant(`${getObjectKeyFromUrl(req.url)}.MODEL_NAME`)
  });
  toastService.showToasts([message], 'success');
}
```

---

## 5. Der **Error‑Interceptor** – Fehler smart und elegant handeln

Dein Error‑Interceptor sorgt dafür, dass Nutzer **strukturierte, übersetzte und gekürzte Fehlermeldungen** bekommen.

### Highlights

- Unterscheidet zwischen strukturierter Error‑Liste und generischen Fehlern
    
- Mapped Backend‑Keys zu i18n‑Translation Keys
    
- Schneidet lange Werte ab (z. B. Strings mit mehr als 15 Zeichen)
    
- Wandelt Klassennamen und Felder in SCREAMING_SNAKE_CASE für die Übersetzungen um
    

### Beispiel: Error‑Mapping

```ts
if (Array.isArray(error.error)) {
  toasts = error.error.map((err) => {
    const key = `ERROR.${err.key}`;
    const values = { ...err.values };

    if (typeof values.IS === 'string') {
      values.IS = values.IS.length > 15 ? values.IS.slice(0, 15) + '...' : values.IS;
    }

    if (typeof values.FIELD === 'string') {
      values.FIELD = translate.instant(`${toScreamingSnake(values.CLASS)}.${toScreamingSnake(values.FIELD)}`);
    }

    if (typeof values.CLASS === 'string') {
      values.CLASS = translate.instant(`${toScreamingSnake(values.CLASS)}.MODEL_NAME`);
    }

    return translate.instant(key, values);
  });
} else {
  toasts = [translate.instant('ERROR.DEFAULT')];
}
```

---

## 6. Vorteile der Verwendung von Interceptoren

### Technische Vorteile

- **DRY‑Prinzip** maximiert → weniger doppelter Code
    
- **Services bleiben schlank**
    
- **Zentrale Kontrolle** über HTTP‑Flow
    
- **Besser testbar** (jede Logik hat einen eigenen Layer)
    

### UX‑Vorteile

- Konsistente Fehler- und Erfolgsmeldungen
    
- Einheitliches Verhalten über die ganze App
    
- Nutzer bekommen **sofort** Feedback
    

---

## 7. Fazit: Warum Interceptor ein Muss sind

Deine Interceptor‑Kombi (Success + Error) hebt die UX und Code‑Qualität massiv an. Sie sorgen für:

- Klare Architektur
    
- Weniger Chaos in Komponenten
    
- Einheitliche Kommunikation mit dem User
    

Kurz gesagt: **Interceptor machen deine App smarter – und dein Code bleibt sauber.**





# Mat Snackbar

Wenn du lediglich die Standard-SnackBar von Angular Material verwenden möchtest, kannst du sie ganz einfach über `snackbar.open()` aufrufen.

Verfügbare Attribute dabei sind:

**message** → Die Nachricht, die angezeigt werden soll  
**action** → Das Label für eine optionale SnackBar-Aktion



In vielen Fällen reicht die Standard-Variante jedoch nicht aus – etwa wenn du mehrere Nachrichten gleichzeitig darstellen möchtest oder verschiedene Farben bzw. Styles pro Nachrichtentyp benötigst. In solchen Fällen solltest du statt `open()` die Methode `openFromComponent()` verwenden, wie im folgenden Beispiel:
````typescript
@Injectable({ providedIn: 'root' })  
export class SnackbarService {  
  private readonly snackBar: MatSnackBar = inject(MatSnackBar);  
  
  showToasts(messages: string[], type: 'success' | 'error') {  
    this.snackBar.openFromComponent(SnackbarComponent, {  
      data: messages,  
      panelClass: type,  
      verticalPosition: 'bottom',  
      horizontalPosition: 'right',  
      duration: 5000  
    });  
  }  
}
````

Mit dieser Variante stehen dir deutlich mehr Konfigurationsmöglichkeiten zur Verfügung. Zudem öffnest du damit eine vollständig eigene Komponente, die du frei gestalten kannst.

## **Wichtige Optionen & Besonderheiten**

### **data**

Über `data` kannst du beliebige Werte in deine SnackBar-Komponente übergeben.  
Diese Daten können z. B. als **Writable Signal** angenommen werden:
```typescript
public messages: WritableSignal<string[]> = signal(this.initialData);
```
Das ermöglicht es dir, Inhalte dynamisch zu aktualisieren oder mehrere Meldungen gleichzeitig anzuzeigen.

### **duration**

Bestimmt, wie lange die SnackBars sichtbar bleiben. Ohne Dauer würden sie dauerhaft angezeigt werden, bis der Nutzer etwas klickt oder du sie manuell schliesst.


### **horizontalPosition & verticalPosition**

Damit kannst du exakt festlegen, wo die SnackBar erscheinen soll – z. B. oben rechts, unten links, zentriert usw.  
Gerade bei mehreren SnackBars sorgt eine klare Positionierung für Übersichtlichkeit.

### **panelClass**

Über `panelClass` kannst du eigene CSS-Klassen vergeben, um dein Styling zu erweitern.  
So kannst du z. B. unterschiedliche Farben, Icons oder Layoutvarianten für verschiedene SnackBar-Typen definieren, etwa für Success-, Error- oder Warning-Meldungen.

### direction

Festlegung der Text-Richtung (z. B. `"ltr"` für links-nach-rechts oder `"rtl"` für rechts-nach-links).

Doku
https://material.angular.dev/components/snack-bar/api



13:00

13:30