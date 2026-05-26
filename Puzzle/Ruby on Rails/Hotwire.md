
### Turbo Frame
Turbo Frame ermöglicht es nur bestimmte teile der Seite asynchron zu ersetzen oder neu zu laden.
Nützlich für modale Fenster, Inline-Bearbeitungen oder Navigation innerhalb eines bestimmten Bereichs.

**Beispiel für einen Turbo Frame:**
````haml
= turbo_frame_tag 'people-skills' do
```` 


### Turbo Stream
Unterstützt verschiedene Aktionen wie `append`, `prepend`, `replace`, `remove`, usw.
Perfekt für Live-Updates, ohne die gesamte Seite neu zu laden.

**Beispiel für einen Turbo Stream:**
````haml
%turbo-stream{ action: "append", target: "messages" }
  %template
    .message Neue Nachricht!
````



