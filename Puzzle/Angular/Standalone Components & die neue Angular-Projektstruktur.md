## Entwicklung

Vor Standalone basierte noch alles auf NgModules.

Jede Komponente, Pipe oder Direktive musste in einem Modul deklariert werden.

Standalone Components, Directives und Pipes sollen NgModules langfristig ablösen.

Ziel:

- Einfachere Architektur

- Weniger unnötige Deklarationen

- Bessere Lesbarkeit

- Schnellere Lernkurve

## Was ist eine Standalone Component?

Eine Standalone Component ist eine Angular Component, die ohne Modul funktioniert.

Sie wird mit `standalone: true` deklariert und importiert ihre Abhängigkeiten selbst.

### Beispiel früher (mit Modul)
```typescript=
@NgModule({
  declarations: [TechtalkComponent],
  imports: [CommonModule, FormsModule],
})
export class TechTalk {}
```
### Beispiel heute (mit Standalone)
```typescript=
@Component({
  selector: 'techtalk',
  standalone: true,
  imports: [CommonModule, FormsModule, AndereComponent],
  template: `Techtalk {{ name }}!`,
})
export class TechtalkComponent {
  name = 'Angular';
}
```
Andere Komponenten kann man einfach importieren.

#### Standalone ist vorhanden für:

- @Component

- @Directive

- @Pipe

## Migration zu Standalone

Angular bietet offizielle Migrations-Schematics:
`ng generate @angular/core:standalone`

Diese Migration macht Folgendes:

- Fügt standalone: true zu den Komponenten hinzu.

- Verschiebt Imports in die Komponenten.

- Überflüssige Module werden entfernt.

- Standalone-Bootstrap wird verwendet.

## Lazy Loading
Dies kommt auch mit neuen und vereinfachten Lazy-Loading-Optionen. Du kannst nun direkt ganze Komponenten lazy-loaden und musst das nicht mehr mit `children` und `NgModules` lösen.

Früher hattest du somit extrem viel unnötigen Code, da jeder Pfad eine eigene Modul-Datei benötigte, die spezifiziert werden musste.

```typescript=
{
  path: 'members',
  loadChildren: () => import('./features/member/member.module').then(m => m.MemberModule)
}
```
Man brauchte früher also noch:
- Eine module.ts mit den Imports und Deklarationen der Komponente, die man mit Lazy Loading laden wollte.

- Und auch eine x-routing.module.ts, wo dann auch noch die Route definiert werden musste.

So kannst du nun ganz einfach eine ganze Komponente lazy-loaden:
```typescript=
{
  path: 'members',
  loadComponent: () =>
    import('./features/member/member-list.component').then(c => c.MemberListComponent)
}
```
## Neue empfohlene Projektstruktur

Mit Standalone Components rückt Angular von der alten Modul-zentrierten Struktur ab und empfiehlt nun eine Feature-orientierte Struktur.

```css
src/
  app/
    core/
      auth/
        auth.service.ts
      guards/
        **.guard.ts
      interceptors/
        **.interceptor.ts

    shared/
      pipes/
        **.pipe.ts
      directives/
        **.directive.ts

    features/
      member/
        overview/
          user-list.component.ts / html / css / spec.ts
        detail/
          member-detail.component.ts / html / css / spec.ts

      member.service.ts / spec.ts
      member.model.ts

  style/
    _custom_angular.scss
    _variables.scss
    styles.scss
```
### Wichtig
Hierbei ist vor allem wichtig, dass du:

- Die Ordnerstruktur nie zu tief machst.

- Die Dateien danach ordnest, in welchen Features sie verwendet werden.

- Sobald mehrere Features dasselbe verwenden, gehört es in shared.

- Ordner wie components/ oder services/ sollten vermieden werden.

- Generelle Funktionen, die benötigt werden, gehören in /core.



## Docs

https://angular.dev/style-guide
https://angular.dev/reference/migrations/route-lazy-loading
https://angular.love/angular-router-everything-you-need-to-know-about
https://angular.dev/reference/migrations/standalone