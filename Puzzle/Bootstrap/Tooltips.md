#### Was ist ein Tool-tip
Bootstrap Tool-tips sind kleine text die angezeigt werden wenn du mit deiner Maus über das Attribut hoverst.
Sie werden dir aber nicht automatisch von Bootstrap 5.0.0 zur verfügung gestellt du muss sie eigenhändig hinzufüge

#### Hinzufügen
Add bootstrap Tooltips in ````application.js````
````js
import * as bootstrap from "bootstrap";

  
    const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]');  
    const tooltipList = [...tooltipTriggerList].map(tooltipTriggerEl => new bootstrap.Tooltip(tooltipTriggerEl));  
````

Nach dem hinzufügen kann nun der Bootstrap Tool-tip verwendet werden.
zuerst muss definiert werden das ein tool-tip auf dem attribute existieren soll.
Dann muss noch eine titel definiert werden, das ist dann der text der im tool-tip angezeigt wird.
````rb
bs_toggle: 'tooltip', bs_title: I18n.t('errors.messages.authorization_error')
````