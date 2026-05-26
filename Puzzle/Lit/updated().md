Die Methode `updated()` wird automatisch ausgeführt, **nachdem** sich etwas an den Daten (Properties) geändert hat und die Komponente neu gerendert wurde.

### Beispiel:
````Typescript
updated() {  
  this.applyHostAttributes();  
}
````
