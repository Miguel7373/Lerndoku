![[Pasted image 20250820114410.png]]
Mit `@property` macht man eine Variable „reaktiv“. Das bedeutet:

- Wenn sich der Wert ändert, wird das HTML der Komponente automatisch neu gebaut.
    
- Der Wert kann auch als HTML-Attribut gesetzt werden.
    

### Einfaches Beispiel:
````typescript
@customElement("pzsh-menu-action")  
export class MenuAction extends LitElement {  
  @property({ type: String })  
  href = "#";
````

