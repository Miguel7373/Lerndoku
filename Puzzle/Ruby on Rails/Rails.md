
## Spread Operator

Der Spread-Operator `**` ist eine nützliche Funktion in Ruby on Rails, insbesondere beim Arbeiten mit Hashes. Er verbessert die Lesbarkeit von Code und erleichtert die Arbeit mit dynamischen Daten. Ausserdem hilft er dabei, Hashes effizient zu entpacken und weiterzugeben, wodurch Code kompakter und flexibler wird.

Die Daten werden von dem hash einfach in das Feld ausgebreitet daher auch der nahmen dadurch kannst du gut die Optionen von extern zusammenladen.

#### Mit Hashes
Wenn du ein hash in einer Methode wie hier
``` rb
def disabled_with_ptime_sync  
  if ptime_sync_active?  
    {  
      'data-bs-toggle': 'tooltip',  
      'data-bs-title': I18n.t('people.form.ptime_data'),  
      'data-bs-placement': 'top',  
      'data-controller': 'tooltip',  
      disabled: true  
    }  
  end  
end
```
Kannst du dann in deinen settings oder wie hier in den options für das html tag den Hash mit den zwei `**` Spreaden
``` haml
%td= form.text_field :name, {class: "mw-100 form-control", **disabled_with_ptime_sync}
```






# Capybara-Tests in Ruby on Rails

## Einleitung

Capybara ist eine Testing-Bibliothek für Ruby, die Interaktionen mit einer Webanwendung in einer echten oder simulierten Browserumgebung nachahmt. In Ruby on Rails wird Capybara häufig mit RSpec verwendet, um Integrationstests zu schreiben, die das Benutzerverhalten prüfen.


## Einfache Teststruktur

Hier ein einfaches Beispiel für einen Feature-Test mit Capybara und RSpec:

``` rb
describe 'Click Quick loading Buttons' do  
  it 'shows profile after clicking button' do  
    sign_in auth_users(:admin), scope: :auth_user  
    visit people_path  
    expect(page).to have_content(t("people.index.profile"))  
    click_button(t("people.index.profile"))  
    expect(page).to have_content(t("people.profile.personals"))  
  end
end
```

### Erklärung:

- `visit`: Ruft eine URL auf.
    
- `fill_in`: Füllt ein Formularfeld aus.
    
- `click_button`: Klickt auf einen Button.
    
- `expect(page).to have_content`: Überprüft den Seiteninhalt.
    

## Best Practices

- Nutze `before`-Blöcke, um wiederkehrende Aktionen vorzubereiten.
