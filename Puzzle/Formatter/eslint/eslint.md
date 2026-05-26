

#### @typescript-es-lint/naming-convention

Diese es-lint Regel kann dir in Typescript konstante Naming Conventions Erzwingen.

Wichtige Optionen
- selector (Wofür das Naming gilt)
	 `variable`, `function`, `class`
- format (Welche Naming Conventions)
	 `camelCase`, `PascalCase`, `UPPER_CASE`
- modifiers (Zusätzliche Einschränkungen)
	 `private`, `static`, `readonly`
- prefix/suffix (spezifische Präfixe/Suffixe)


Beispielkonfiguration
``` javascript
"@typescript-eslint/naming-convention": [
  "error",
  { "selector": "default", "format": ["camelCase"] },
  { "selector": "variable", "format": ["camelCase", "UPPER_CASE"], "modifiers": ["const"] },
  { "selector": "function", "format": ["camelCase"] },
  { "selector": "class", "format": ["PascalCase"] }
]
```

[es-lint Offizielle Doku](https://typescript-eslint.io/rules/naming-convention/)



#### id-match

Die Regel `id-match` stellt sicher, dass (z. B. Variablen- oder Funktionsnamen) einem bestimmten Naming Convention entsprechen.

Wichtige Optionen
- pattern: 
	Ein regulärer Ausdruck, der die erlaubten Namensmuster definiert
	
- properties:
	Gibt an, ob die Regel auch auf Objekteigenschaften angewendet wird
	
- onlyDeclarations: 
	Beschränkt die Regel auf deklarierte Bezeichner
    
- errorMessage: 
	Eine benutzerdefinierte Fehlermeldung, wenn die Regel verletzt wird	


## Beispielkonfiguration
``` javascript
"id-match": [
  "error",
  "^[a-z]+([A-Z][a-z]+)*$",
  { "properties": true }
]
```


[es-lint Offizielle Doku](https://eslint.org/docs/latest/rules/id-match)


#### @html-eslint/id-naming-convention

Die Regel `@html-eslint/id-naming-convention` stellt sicher, dass HTML-IDs einer bestimmten Naming Convention entsprechen.

Wichtige Optionen
- pattern: 
	Ein regulärer Ausdruck, der die erlaubten Namensmuster für IDs definiert.
	
- errorMessage: 
	Eine benutzerdefinierte Fehlermeldung, wenn die Regel verletzt wird.

``` javascript
"id-match": [
  "error",
  "^[a-z]+([A-Z][a-z]+)*$",
  { "properties": true }
]
```


[es-lint Offizielle Doku](https://html-eslint.org/docs/rules/id-naming-convention)



