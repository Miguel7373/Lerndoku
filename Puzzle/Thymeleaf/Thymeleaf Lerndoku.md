
**Thymeleaf** ist ein Serverseitiges Java-Template-Engine-Framework
simple expressions:
- Variable Expressions: `${...}`
- Selection Variable Expressions: `*{...}`
- Message Expressions: `#{...}`
- Link URL Expressions: `@{...}`
- Fragment Expressions: `~{...}`


**Model**
```
model.addAttribute("searchInput", searchInput);
```

Hierbei wird das `searchInput`-Objekt mit dem Schlüssel `"searchInput"` dem `Model` hinzugefügt. Das `Model` ist eine Schnittstelle zwischen dem Controller und der View.


**Fragments**
```
<div class="subject-box" th:fragment="downloadBox(examFile)">
```

Ein Fragment  ist eine html Vorlage die später in anderen Teilen der Vorlage oder in anderen Vorlagen wiederverwendet werden kann.

























