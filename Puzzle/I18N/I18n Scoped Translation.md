
## 1. Was bedeutet „Scoped Translation“ genau

„Scoped Translation“ (zu Deutsch etwa „kontextbezogene Übersetzung“) heißt, dass Übersetzungsschlüssel nicht global mit einem langen Pfad (Namespace) benutzt werden müssen, sondern lokal in einem bestimmten Kontext (Scope) definiert und referenziert werden können.

- In einem klassischen i18n-System würdest du z. B. `MEMBER.OVERVIEW.NAME` schreiben, um auf den Namen-String im „member → overview“-Kontext zuzugreifen.
    
- Mit Scoped Translation kannst du in Dateien, die bereits im Kontext „member/overview“ liegen, einfach `NAME` schreiben – weil der Kontext (Scope) automatisch vorausgesetzt wird.
    

Das setzt voraus, dass dein System einen „Prefix“-Scope kennt, also einen Mechanismus, der sagt: „In diesem Modul / dieser Komponente gilt dieser Namensraum.“

---

## 2. Welche Vorteile bringt das

Hier sind die wichtigsten Vorteile, die sich aus Scoped Translation ergeben:

1. **Weniger Boilerplate**  
    Du musst nicht jedes Mal den vollen Pfad wie `MEMBER.OVERVIEW.NAME` schreiben, sondern nur `NAME`, wenn du bereits im Scope „MEMBER → OVERVIEW“ bist. Das spart Tipparbeit und reduziert Fehler (z. B. Tippfehler im Namespace).
    
2. **Bessere Abstraktion / Wiederverwendbarkeit**  
    Deine Komponenten oder Klassen werden weniger „i18n-spezifisch“, weil sie nicht ständig mit harten Schlüsseln (z. B. `MEMBER.OVERVIEW.NAME`) getriggert werden. Stattdessen nutzt du innerhalb des Scopes universelle Keys, was deine Codebasis sauberer macht.
    
3. **Kontextrelevanz**  
    Da ein Kontext definiert ist, weiß dein i18n-Service genau, welche Übersetzungen geladen oder verwendet werden sollen. Das reduziert das Risiko, dass ein falscher Schlüssel aus einem anderen Modul verwendet wird.

---

## 3. Beispiel für die Implementation

Du hast schon erwähnt, dass dein PR folgende Teile enthält:

1. `i18n-prefix.token.ts` — Ein Token, das den Prefix (Scope) speichert.
	Dieser Token speichert den Prefix und ist dafür verantwortlich, dass die Pipe weiss, welchen Prefix du hast.
	
2. `i18n-prefix.provider.ts` — Ein Provider, der den Scope „injiziert“.
	Hier wird die provideI18nPrefix-Funktion geschrieben. Sie ist dafür verantwortlich, dass man in der Rout den Prefix-Token setzen kann.
	
3. `scoped-translation.service.ts` — Service, der Übersetzungen innerhalb des Scope auflöst.
	Dieser Service probiert alle möglichen Translation mit dem Prefix, den er hat, also kürzt er ihn so lange, bis er eine Translation findet oder eben nicht.
	
4. `scoped-translation-pipe.ts` — Pipe, um im Template zu übersetzen.
	Das ist die Pipe, die du im HTML angeben kannst, und das, was du im HTML mitgibst, gibst du dem Translation Service mit, um die Translation durchzuführen.
	
5. Anpassung der `routes` (z. B. in `app.routes.ts`), damit bei bestimmten Routen ein Scope gesetzt wird.
	Hier definierst du den Token, der zu einem Feature gehören soll.


### Spec files

In unserem `setup.js` wird der **I18N Prefix** zentral für alle Tests bereitgestellt:
````typescript
beforeEach(() => {  
    TestBed.configureTestingModule({  
        imports: [],  
        providers: [  
            {provide: ScopedTranslationService, useValue: translationMock},  
            {provide: I18N_PREFIX, useValue: "GLOBAL.DEFAULT.PREFIX"},  
          { provide: DateAdapter,  
            useClass: LuxonDateAdapter },  
          { provide: MAT_DATE_FORMATS,  
            useValue: CUSTOM_LUXON_DATE_FORMATS },  
        ]  
    });  
});
````
**Wenn du in Specs mit Translations arbeitest**, musst du diesen Prefix nutzen oder zumindest erwarten, dass er existiert.


#### Achtung!!!

Dieses TestBed ist **vordefiniert**.  
Wenn du in einem Test ein **neues TestBed aufbaust** (z. B. durch erneutes `TestBed.configureTestingModule()`),  
musst du **alle benötigten Provider erneut angeben** – insbesondere den:
````typescript
	{provide: ScopedTranslationService, useValue: translationMock},  
    {provide: I18N_PREFIX, useValue: "GLOBAL.DEFAULT.PREFIX"},  
````



https://codimd.puzzle.ch/YTHtLjlBTEGcxHhLGnVqDg#

https://github.com/puzzle/pcts/pull/197/files#diff-264ccb65ece0321a99ebbb59baa1ed5e2d2a406a6cf7526adba547f4c0fc8ca5