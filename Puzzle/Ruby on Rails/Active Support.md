
## 1. Was ist Active Support?

Active Support ist die Werkzeugkiste von Ruby on Rails. Es ist eine Sammlung von Erweiterungen für die Standard-Ruby-Klassen (wie `Object`, `String`, `Array`, `Hash`, etc.). Das Ziel? Den Code lesbarer, intuitiver und kürzer zu machen. Es nimmt uns als Entwicklern die immer wiederkehrenden, nervigen Alltagsaufgaben ab (Boilerplate-Code).

---

## 2. Wie wird es geladen? (Das Standardverhalten)

In einer normalen Ruby on Rails-Anwendung musst du dich um nichts kümmern: **Rails lädt standardmäßig das komplette Active Support Paket.**

Es gibt jedoch eine Ausnahme: Wenn du in deiner Konfiguration `config.active_support.bare = true` setzt, lädt Rails nur das absolute Minimum, das das Framework selbst zum Funktionieren braucht. Das macht man manchmal bei Performance-kritischen oder extrem schlanken APIs.

---

## 3. Nur spezifische Teile laden (Cherry-Picking)

Wenn du `bare = true` nutzt oder Active Support in einem reinen Ruby-Projekt (ohne den Rest von Rails) verwenden willst, kannst du gezielt nur die Funktionen laden ("Cherry-Picking"), die du wirklich brauchst. Das hält den Speicherbedarf klein.

**Beispiele:**

- Das absolute Minimum laden: `require "active_support"`
    
- Nur die Methode `blank?` für Objekte laden: `require "active_support/core_ext/object/blank"`
    
- Alle String-Erweiterungen auf einmal laden: `require "active_support/core_ext/string"`
    
- Alles laden (wenn man außerhalb von Rails ist): `require "active_support/all"`
    

---

## 4. Die wichtigsten Methoden im Alltag

Hier sind die absoluten "Gamechanger", die man ständig braucht.

### 4.1. Die Basics für alle Objekte (`Object`)

- **`blank?`**: Ist `true` für alles, was logisch "leer" ist: `nil`, `false`, `""` (auch Strings nur mit Leerzeichen!), `[]` und `{}`.
    
- **`present?`**: Das genaue Gegenteil von `blank?` (`!blank?`).
    
- **`presence`**: Gibt das Objekt zurück, wenn es `present?` ist, ansonsten `nil`. Genial für kurze Fallbacks:
    
    Ruby
    
    ```
    name = user.name.presence || "Unbekannt"
    ```
    

### 4.2. Die Falle beim Kopieren: `dup` vs. `deep_dup`

Das ist enorm wichtig, um fiese Bugs zu vermeiden, wenn man mit verschachtelten Daten (z.B. Arrays von Strings) arbeitet.

- **`dup` (Ruby Standard):** Erstellt nur eine _flache Kopie_. Wenn du ein Array kopierst und ein Element darin änderst, ändert es sich auch im Original!
    
    Ruby
    
    ```
    array = ["hallo"]
    kopie = array.dup
    kopie.first.gsub!("hallo", "tschüss")
    
    array # => ["tschüss"]  <-- Original wurde überschrieben!
    ```
    
- **`deep_dup` (Active Support):** Erstellt eine _tiefe Kopie_. Alles wird komplett geklont.
    
    Ruby
    
    ```
    array = ["hallo"]
    kopie = array.deep_dup
    kopie.first.gsub!("hallo", "tschüss")
    
    array # => ["hallo"]  <-- Original bleibt unangetastet!
    ```
    

## Active Support Functions 

### duplicable?

ohne duplicable?

Ruby

```ruby
begin
  obj.dup
rescue TypeError
  # Nicht duplizierbar
end
```

##### mit duplicable?

Ruby

```ruby
obj.duplicable?
```

Prüft, ob ein Objekt sicher mit `dup` kopiert werden kann (z.B. Klassen oder Methoden sind es oft nicht).

### deep_dup

ohne deep_dup

Ruby

```ruby
# flaches dup, verschachtelte Elemente werden referenziert
duplicate = array.dup 
```

##### mit deep_dup

Ruby

```ruby
duplicate = array.deep_dup
```

Macht eine echte, tiefe Kopie, inkl. aller verschachtelten Arrays/Hashes.

### try / try!

ohne try

Ruby

```ruby
@number.next unless @number.nil?
```

##### mit try

Ruby

```ruby
@number.try(:next)
```

Entfernt den nutzlosen nil-Aufruf. `try!` wirft weiterhin einen Fehler, wenn die Methode auf dem Objekt gar nicht existiert.


### acts_like?

ohne acts_like?

Ruby

```ruby
if obj.is_a?(Time) || obj.is_a?(DateTime)
```

##### mit acts_like?

Ruby

```ruby
if obj.acts_like?(:time)
```

Prüft über Duck-Typing, ob sich ein Objekt wie ein bestimmter Datentyp verhält.

### to_param

ohne to_param

Ruby

```ruby
"#{user.id}-#{user.name.parameterize}"
```

##### mit to_param

Ruby

```ruby
user.to_param
```

Gibt eine String-Repräsentation für URLs oder Query-Strings zurück (z.B. für Routing).

### to_query

ohne to_query

Ruby

```ruby
"user=#{CGI.escape(user.to_param.to_s)}"
```

##### mit to_query

Ruby

```ruby
user.to_query("user")
```

Konstruiert einen sicheren, escaped Query-String.

### with_options

ohne with_options

Ruby

```ruby
has_many :contracts, dependent: :destroy
has_many :companies, dependent: :destroy
```

##### mit with_options

Ruby

```ruby
with_options dependent: :destroy do |assoc|
  assoc.has_many :contracts
  assoc.has_many :companies
end
```

Fasst wiederkehrende Optionen in einem Block zusammen.

### instance_values / instance_variable_names

ohne instance_values

Ruby

```ruby
hash = {}
instance_variables.each { |ivar| hash[ivar.to_s.sub('@', '')] = instance_variable_get(ivar) }
```

##### mit instance_values

Ruby

```ruby
object.instance_values
object.instance_variable_names
```

Gibt Hashes (ohne @) oder Arrays (mit @) der Instanzvariablen zurück.

### silence_warnings / suppress

ohne suppress

Ruby

```ruby
begin
  # Code
rescue ActiveRecord::StaleObjectError
  # ignorieren
end
```

##### mit suppress

Ruby

```ruby
suppress(ActiveRecord::StaleObjectError) do
  # Code
end
```

Unterdrückt Warnungen oder bestimmte Error-Klassen gezielt.

### in?

ohne in?

Ruby

```ruby
[1, 2, 3].include?(@number)
```

##### mit in?

Ruby

```ruby
@number.in?([1, 2, 3])
```

Dreht die Logik um, damit sie sich natürlicher liest.

## 2. Extensions to Module

### alias_attribute

ohne alias_attribute

Ruby

```ruby
def login; email; end
def login=(v); self.email = v; end
def login?; email?; end
```

##### mit alias_attribute

Ruby

```ruby
alias_attribute :login, :email
```

Legt Getter, Setter und Prädikat auf einmal als Alias an.

### attr_internal

ohne attr_internal

Ruby

```ruby
attr_accessor :_my_library_internal_state
```

##### mit attr_internal

Ruby

```ruby
attr_internal :state
```

Versteckt die Instanzvariable hinter einem Namensschema (z.B. `@_state`), um Namenskollisionen zu vermeiden.

### module_parent / module_parent_name / module_parents

ohne module_parent

Ruby

```ruby
# String-Splitting von Module.name
```

##### mit module_parent

Ruby

```ruby
M::N.module_parent # => M
```

Gibt das übergeordnete Modul oder dessen Namen zurück.

### anonymous?

ohne anonymous?

Ruby

```ruby
mod.name.nil?
```

##### mit anonymous?

Ruby

```ruby
mod.anonymous?
```

Prüft, ob das Modul einen Namen hat oder anonym generiert wurde.

### delegate

ohne delegate

Ruby

```ruby
def street
  address.street
end
```

##### mit delegate

Ruby

```ruby
delegate :street, to: :address
```

Delegiert eine Methode direkt an ein anderes Objekt.

### redefine_method

ohne redefine_method

Ruby

```ruby
remove_method :foo if method_defined?(:foo)
define_method(:foo) { ... }
```

##### mit redefine_method

Ruby

```ruby
redefine_method(:foo) { ... }
```

Überschreibt eine Methode sicher ohne Warnungen von Ruby.

## 3. Extensions to Class

### class_attribute

ohne class_attribute

Ruby

```ruby
# Komplexe Getter/Setter Konstrukte auf Klassen- und Instanzebene
```

##### mit class_attribute

Ruby

```ruby
class_attribute :setting
```

Erstellt vererbbare Klassen-Attribute, die in Subklassen oder Instanzen sicher überschrieben werden können.

### subclasses / descendants

ohne descendants

Ruby

```ruby
# Objekt-Raum durchsuchen (sehr langsam)
```

##### mit descendants

Ruby

```ruby
Parent.subclasses  # Nur direkte Kinder
Parent.descendants # Alle Generationen
```

Liefert alle abgeleiteten Klassen.

## 4. Extensions to String

### html_safe

ohne html_safe

Ruby

```ruby
# Standard-Strings werden von Rails Views immer escaped
```

##### mit html_safe

Ruby

```ruby
"<div>".html_safe
```

Markiert einen String als sicheres HTML, damit Rails ihn im View nicht escaped.

### remove

ohne remove

Ruby

```ruby
"Hello World".gsub(/World/, "")
```

##### mit remove

Ruby

```ruby
"Hello World".remove(/World/)
```

Entfernt das angegebene Muster aus dem String.

### squish

ohne squish

Ruby

```ruby
" \n foo \t bar \n".strip.gsub(/\s+/, ' ')
```

##### mit squish

Ruby

```ruby
" \n foo \t bar \n".squish
```

Entfernt äußere Leerzeichen und komprimiert innere auf genau eines.

### truncate / truncate_bytes / truncate_words

ohne truncate

Ruby

```ruby
text.length > 15 ? "#{text[0...12]}..." : text
```

##### mit truncate

Ruby

```ruby
text.truncate(15)
text.truncate_words(4)
```

Kürzt den String nach Zeichen, Bytes oder Wörtern und hängt "..." an.

### inquiry

ohne inquiry

Ruby

```ruby
status == "active"
```

##### mit inquiry

Ruby

```ruby
status.inquiry.active?
```

Erlaubt es, String-Werte mit einer Prädikat-Methode abzufragen.

### starts_with? / ends_with?

ohne starts_with?

Ruby

```ruby
string.match?(/^foo/)
```

##### mit starts_with?

Ruby

```ruby
string.starts_with?("foo")
```

Prüft explizit auf den Anfang oder das Ende des Strings (auch auf Symbolen verfügbar).

### Access (at, from, to, first, last)

ohne from

Ruby

```ruby
string[2..-1]
```

##### mit from

Ruby

```ruby
string.from(2)
string.to(4)
string.first(3)
```

Lesbarere Methoden, um Substrings zu extrahieren.

### Inflections (pluralize, singularize, camelize, underscore, titleize, dasherize, demodulize, deconstantize, parameterize, tableize, classify, constantize, humanize, foreign_key)

ohne Inflections

Ruby

```ruby
# Manuelle String-Manipulation oder Regex
```

##### mit Inflections

Ruby

```ruby
"post".pluralize        # "posts"
"posts".singularize     # "post"
"active_record".camelize # "ActiveRecord"
"ActiveRecord".underscore # "active_record"
"john smith".titleize   # "John Smith"
"a_b".dasherize         # "a-b"
"User".foreign_key      # "user_id"
"john doe".parameterize # "john-doe"
"Module::Class".demodulize # "Class"
"Module::Class".constantize # Gibt die echte Klasse Module::Class zurück
```

Rails-typische Umwandlungen von Strings (extrem wichtig für das Namenskonzept).

### Conversions (to_date, to_time, to_datetime)

ohne to_date

Ruby

```ruby
Date.parse("2020-01-01")
```

##### mit to_date

Ruby

```ruby
"2020-01-01".to_date
```

Bequemer Shortcut zur Typumwandlung.

## 5. Extensions to Numeric & Integer & BigDecimal

### Bytes / Time (Numeric)

ohne Bytes/Time

Ruby

```ruby
size = 5 * 1024 * 1024 # 5 MB
time = 5 * 24 * 60 * 60 # 5 Tage in Sek
```

##### mit Bytes/Time

Ruby

```ruby
size = 5.megabytes
time = 5.days
```

Macht Zahlen direkt zu verständlichen Zeit- oder Byte-Einheiten.

### to_fs (Numeric)

ohne to_fs

Ruby

```ruby
sprintf("$%.2f", 12.3)
```

##### mit to_fs

Ruby

```ruby
12.3.to_fs(:currency) # "$12.30"
```

Erlaubt schnelle Formatierungen wie Währungen, Telefonnummern etc.

### multiple_of? (Integer)

ohne multiple_of?

Ruby

```ruby
number % 3 == 0
```

##### mit multiple_of?

Ruby

```ruby
number.multiple_of?(3)
```

Leserlicher Modulo-Check.

### ordinal / ordinalize (Integer)

ohne ordinalize

Ruby

```ruby
# Komplexe Suffix-Logik
```

##### mit ordinalize

Ruby

```ruby
1.ordinalize # "1st"
```


### Years 

```ruby
years.from_now
```

Hängt die englischen Suffixe (st, nd, rd, th) an die Zahl an.

## 6. Extensions to Enumerable

### index_by / index_with

ohne index_by

Ruby

```ruby
hash = {}
users.each { |u| hash[u.id] = u }
```

##### mit index_by

Ruby

```
users.index_by(&:id)
users.index_with { |u| u.name }
```

Erstellt Hashes aus Arrays. Entweder werden die Listenelemente die Werte (`index_by`) oder die Schlüssel (`index_with`).

### many?

ohne many?

Ruby

```
collection.size > 1
```

##### mit many?

Ruby

```
collection.many?
```

Gibt true zurück, wenn mehr als ein Element existiert.

### exclude? / excluding / including

ohne exclude?

Ruby

```
!array.include?(x)
array.reject { |e| e == x }
```

##### mit exclude?

Ruby

```
array.exclude?(x)
array.excluding(x) # Gibt ein Array ohne x zurück
array.including(x) # Gibt ein Array mit x zurück
```

Kehrt die include-Logik um oder erstellt Arrays ohne/mit spezifischen Elementen.

### pluck / pick

ohne pluck

Ruby

```
users.map { |u| u[:name] }
```

##### mit pluck

Ruby

```
users.pluck(:name)
users.pick(:name)
```

Extrahiert gezielt Werte von Hashes oder Objekten aus einer Collection (ähnlich wie in ActiveRecord).

## 7. Extensions to Array

### Accessing (second, third, fourth, fifth, forty_two)

ohne second

Ruby

```
array[1]
array[41]
```

##### mit second

Ruby

```
array.second
array.forty_two
```

Gibt lesbare Aliase für Array-Indizes (forty_two ist ein Easter Egg per Rails Guide).

### to_sentence

ohne to_sentence

Ruby

```
array.join(", ") # Ohne 'and'
```

##### mit to_sentence

Ruby

```
["A", "B", "C"].to_sentence # "A, B, and C"
```

Macht aus dem Array einen grammatikalisch korrekten Satz. Looks at I18n for the language

### Array.wrap

ohne Array.wrap

Ruby

```
obj.is_a?(Array) ? obj : (obj.nil? ? [] : [obj])
```

##### mit Array.wrap

Ruby

```
Array.wrap(obj)
```

Erzwingt immer ein Array, egal was reinkommt.

### Grouping (in_groups_of, in_groups, split)

ohne in_groups_of

Ruby

```
# Manuelles iterieren und slicen
```

##### mit in_groups_of

Ruby

```
[1, 2, 3].in_groups_of(2) # [[1, 2], [3, nil]]
[1, 2, 3].split(2) # [[1], [3]]
```

Unterteilt Arrays in gleich große Blöcke oder splittet sie an einem bestimmten Wert.

## 8. Extensions to Hash

### Merging (reverse_merge, reverse_merge!, deep_merge)

ohne reverse_merge

Ruby

```
default_options.merge(options)
```

##### mit reverse_merge

Ruby

```
options.reverse_merge(default_options)
hash1.deep_merge(hash2) # Merged auch verschachtelte Hashes
```

Lil example
```ruby
defaults = {
  app: {
    theme: "light",
    notifications: true
  },
  version: 1
}

custom = {
  app: {
    theme: "dark"
  }
}
```

Setzt Standardwerte, überschreibt aber keine vorhandenen Schlüssel. `deep_merge` arbeitet rekursiv.

### Working with Keys (stringify_keys, symbolize_keys, deep_transform_keys)

ohne symbolize_keys

Ruby

```
hash.keys.each { |k| hash[k.to_sym] = hash.delete(k) }
```

##### mit symbolize_keys

Ruby

```
hash.symbolize_keys
hash.deep_transform_keys { |k| k.to_s.upcase }
```

Konvertiert alle Schlüssel eines Hashes, optional auch tief verschachtelt.

### Working with Values (transform_values)

ohne transform_values

Ruby

```
hash.each_with_object({}) { |(k, v), h| h[k] = v.to_s }
```

##### mit transform_values

Ruby

```
hash.transform_values(&:to_s)
```

Bearbeitet nur die Werte eines Hashes, behält die Schlüssel bei.

### Slicing / Extracting

ohne extract!

Ruby

```
val = hash[:key]; hash.delete(:key)
```

##### mit extract!

Ruby

```
hash.slice(:a, :b) # Gibt Hash NUR mit :a und :b zurück
hash.extract!(:key) # Gibt den extrahierten Teil zurück UND entfernt ihn aus dem Original
```

Filtert Hashes gezielt.

### with_indifferent_access

ohne indifferent

Ruby

```
val = hash["key"] || hash[:key]
```

##### mit indifferent

Ruby

```
hash.with_indifferent_access[:key]
```

Macht den Unterschied zwischen Symbol- und String-Schlüsseln irrelevant.

## 9. Extensions to Regexp / Range

### multiline? (Regexp)

ohne multiline?

Ruby

```
(regexp.options & Regexp::MULTILINE) != 0
```

##### mit multiline?

Ruby

```
regexp.multiline?
```

Prüft einfach auf das Multiline-Flag.

### overlap? / include? / === (Range)

ohne overlap?

Ruby

```
range1.first <= range2.last && range2.first <= range1.last
```

##### mit overlap?

Ruby

```
(1..5).overlap?(4..6) # true
```

Prüft, ob sich zwei Ranges überschneiden. ActiveSupport passt auch `===` und `include?` an, um intelligenter mit Werten umzugehen.

## 10. Extensions to Date / DateTime / Time

### Calculations

ohne ActiveSupport

Ruby

```
# Datum-Berechnungen sind in reinem Ruby teils absurd komplex
```

##### mit ActiveSupport

Ruby

```
time.beginning_of_day
time.end_of_week
time.months_ago(2)
time.advance(years: 1, weeks: 2)
time.change(hour: 12, min: 0)
```

Bietet absolute Kontrolle über Zeitpunkte. Berechnet problemlos Schaltjahre, Monatsenden und Wochenanfänge.