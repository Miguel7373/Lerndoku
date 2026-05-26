

# Rails Inflections

Inflections sorgen dafür, dass Rails versteht, welche Files zusammengehören.  
Dadurch werden beispielsweise ein `Team`-Model und ein `Teams`-Controller direkt erkannt und korrekt zugeordnet.

## Ausnahmen bei Inflections

Es gibt jedoch Ausnahmen, bei denen Rails die Mehrzahl eines Wortes nicht automatisch erkennt oder keine Aneinanderreihungen von Großbuchstaben zulassen möchte.  
Beispiele dafür sind:

- **"API"** → Keine automatische Umwandlung in "APIs"
- **"Person" → "People"** (anstatt der regulären "Persons")

## Anpassung mit `inflections.rb`

Um solche Sonderfälle zu definieren, kannst du das `inflections.rb`-File anpassen.  
Dort kannst du spezifische Regeln festlegen, damit Rails die Dateien weiterhin automatisch verknüpfen kann, ohne Fehler zu werfen.

### Beispiel für eine `inflections.rb`-Datei:

```ruby
# config/initializers/inflections.rb

ActiveSupport::Inflector.inflections(:en) do |inflect|
  inflect.irregular 'person', 'people'
  inflect.acronym 'API'
end
```








































Inflections sorgen dafür das rails versteht welche files zusammen gehören also wird dann ein team model und ein teams controller direkt erkannt das sie zusammengehören nun gibt es aber auch ausnahmen wie (API oder people/ person) dafür haben sie ein `inflections.rb` file wo du ausnahmen in dem naming angeben kannst damit rails die files wider automatisch verlinken kann ohne dir errors zu werfen nur weil er die Mehrzahl des Wortes nicht weis oder keine Aneinanderreihungen Grossbuchstaben haben will.




# Ruby Workshop  
  
Das ist der neue Programming Workshop für das IT-Ninjas Schnupper Programm  
  
Workshop-Inhalte  
  
 - Einführung in Ruby  
 - Wordle mit Zusatzaufgaben  
  
File starten  
   - `ruby dateiname.rb`


Das ist der neue Programming Workshop für das IT-Ninjas Schnupper Programm



![Owner avatar](https://avatars.githubusercontent.com/u/58933474?s=48&v=4) **[schnuppertag-ruby-workshop](https://github.com/puzzle-bbt/schnuppertag-ruby-workshop)** Private






