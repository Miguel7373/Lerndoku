
## Was ist Cypress

Cypress ist ein modernes End-to-End (E2E) Test-Framework für Webanwendungen. Es wurde entwickelt, um Entwicklern und QA-Teams dabei zu helfen, automatisierte Tests für ihre Anwendungen zu schreiben und auszuführen. Cypress ist besonders für seine einfache Einrichtung, schnelle Ausführung von Tests und die Möglichkeit, Tests in Echtzeit zu debuggen, bekannt.

## Wichtige Cypress-Funktionen

- `cy.visit(url)`: Besucht die angegebene URL.
- `cy.get(selector)`: Wählt ein Element auf der Seite basierend auf einem CSS-Selektor aus.
- `cy.contains(text)`: Findet ein Element, das den angegebenen Text enthält.
- `cy.click()`: Führt einen Klick auf das ausgewählte Element aus.
- `cy.type(text)`: Gibt den angegebenen Text in ein Eingabefeld ein.
- `cy.should('condition')`: Fügt eine Assertion hinzu, um zu überprüfen, ob eine Bedingung erfüllt ist.
- Usw der Rest ist hier zu finden https://docs.cypress.io/api/table-of-contents


## Isolation 
macht das nach jedem Test localstorage sessionstorage und Cookies gelöscht werden was dazu führt das jeder Test von den anderen unabhängig ist 

wenn man das deaktiviert hat, kann man auch cy.session verwenden was im Grunde auch nur einen neue Session macht und somit das gekennzeichnete Element von den anderen unabhängig macht

das Ganze hat viele Vorteile im Grunde ist es super da man dann immer von einem Anfangspunkt aus testen kann und sich im beforeEach nicht Gedanken machen muss wie man zurück auf den Anfang kommt aber es kann natürlich auch zu längeren und komplexeren testen führen da man nicht beim letzten File weitermachen kann. Es ist zur zeit best practice






### Sicheres und Unsicheres Chaining von Commands in Cypress
#### Einführung

Cypress führt Commands asynchron aus, wartet aber automatisch auf deren Abschluss. 

#### Unsicheres Chaining 
Unsicheres Chaining entsteht, wenn Commands ohne klare Synchronisation oder Abhängigkeiten verkettet werden, was zu unvorhersehbaren Ergebnissen führt.
#### Unsicheres Chaining vermeiden
Alias mit as:
Aliasnamen helfen, Elemente wiederzuverwenden und den Code lesbarer zu machen.
```` d
cy.get('.input').as('inputField')
cy.get('@inputField').type('Test')
````
Verwendung von then:
Mit .then() lassen sich Commands explizit synchronisieren.
````d
cy.get('.button').click().then(() => {
  cy.get('.message').should('be.visible')
})
````

Assertions einbauen:
Sicherstellen, dass der gewünschte Zustand vorliegt, bevor der nächste Schritt ausgeführt wird.
```` d
cy.get('.message').should('exist').and('be.visible')
````
Custom Commands:
Komplexe Abläufe in eigenen Commands zusammenfassen.
```` d
    Cypress.Commands.add('submitForm', () => {
      cy.get('.input').type('Test')
      cy.get('.button').click()
      cy.get('.message').should('be.visible')
    })
    cy.submitForm()
````
Fazit

Unsicheres Chaining führt zu instabilen Tests. Mit Aliasen, then, Assertions und Custom Commands können Sie stabile und wartbare Tests sicherstellen.


## Testing specific test file headless 

npm run cypress:run -- --headless --spec cypress/e2e/tab.cy.ts





