# DRY CRUD in Ruby on Rails

## 1. Einleitung

In fast jeder Ruby-on-Rails-Anwendung gibt es Models, die **klassische CRUD-Funktionalität** benötigen:

* **Create** (Erstellen)
* **Read** (Anzeigen)
* **Update** (Bearbeiten)
* **Delete** (Löschen)

Rails bietet dafür zwar Mittel wie *Scaffolding*, doch in der Praxis führt das schnell zu:

* viel **dupliziertem Code**
* schwer wartbaren Views
* aufgeblähten Controllern

**DRY CRUD** setzt genau hier an.

**Ziel:**
Eine saubere, erweiterbare und verständliche CRUD-Basis schaffen – ohne Magie, ohne Blackbox.

---

## 2. Was ist DRY CRUD?

**dry_crud** ist ein **Rails Generator**, kein klassisches Runtime-Gem.

Das bedeutet:

* Der generierte Code liegt **vollständig in deiner App**
* Du kannst **alles lesen, anpassen und erweitern**
* Keine versteckte Logik
* Keine Abhängigkeit zur Laufzeit

**Kernidee:**

> Konzentriere wiederkehrende CRUD-Logik (Controller, Views, Helpers) in klaren, erweiterbaren Basisklassen.

---

### DRY CRUD

 Volle Kontrolle
 Einheitliche CRUD-Struktur
 Leicht erweiterbar
 Verständlicher Code

---

## 4. Installation

### Variante 1: Neues Projekt

```bash
rails new APP_NAME -m https://raw.github.com/codez/dry_crud/master/template.rb
```

### Variante 2: Bestehendes Projekt

```bash
gem install dry_crud
```

```ruby
# Gemfile
gem 'dry_crud'
```

```bash
rails generate dry_crud [--templates haml] [--tests rspec]
```

Optionen:

* `--templates haml`  HAML statt ERB
* `--tests rspec` RSpec statt Test::Unit

Nach dem Generieren kann das Gem wieder entfernt werden.

---

## 5. Grundintegration in die App

Für ein CRUD-Model brauchst du nur **drei Dinge**:

### 1 Controller von `CrudController` erben

```ruby
class PeopleController < CrudController
  self.permitted_attrs = [:firstname, :lastname, :birthday, :gender, :city_id]
end
```

### 2 `to_s` im Model definieren

```ruby
class Person < ApplicationRecord
  def to_s
    [lastname, firstname].compact.join(' ')
  end
end
```

### (Optional) Scopes definieren

```ruby
scope :list, -> { order('lastname, firstname') }
```

Fertig: Liste, Sortierung, Suche, Show-, Edit- & New-Views sind sofort da.

---

## 6. Architektur-Überblick

### Zentrale Controller

* `ListController`  Nur Lesen
* `CrudController`  Vollständiges CRUD

### Module

* `Sortable`  Sortierung
* `Searchable`  Suche
* `Nestable`  Nested Resources
* `Rememberable`  Zurück zur Liste
* `RenderCallbacks`  before_render Hooks

Alles modular & austauschbar.

---

## 7. Views & Overriding-Prinzip

DRY CRUD arbeitet mit **Fallback-Views**:

* Existiert eine View in `app/views/people/`  diese wird genutzt
* Sonst  Fallback auf `app/views/crud/`

### Beispiel: Liste anpassen

```erb
<%= crud_table :lastname, :firstname, :city, :gender %>
```

Nur diese Attribute erscheinen in der Tabelle.

---

## 8. Formulare mit `crud_form` & `standard_form`

```erb
<%= standard_form(@person, :firstname, :lastname, :age, :city) %>
```

Automatisch:

* Labels
* Input-Typen
* Fehlermeldungen
* Save-Button

### Custom Fields

```erb
<%= f.labeled(:female) do %>
  <%= f.radio_button :female, true %> female
  <%= f.radio_button :female, false %> male
<% end %>
```

---

## 9. Associations

### belongs_to

```erb
<%= f.belongs_to_field :city %>
```

### has_many

```erb
<%= f.has_many_field :visited_cities %>
```

Nutzt automatisch `options_list` Scope im Model.

---

## 10. Sortierung & Suche

### Default Sortierung

```ruby
self.default_sort = 'lastname, firstname'
```

### Suchfelder

```ruby
self.search_columns = [:firstname, :lastname]
```

Automatische Suchbox im Index.

---

## 11. Formatierung von Attributen

```ruby
def format_person_female(person)
  person.female ? 'female' : 'male'
end
```

Oder global:

```ruby
def format_female(value)
  value ? 'female' : 'male'
end
```

---

## 12. Nested Resources

DRY CRUD unterstützt verschachtelte Controller/Resources automatisch:

```ruby
namespace :admin do
  resources :departments do
    resources :people
  end
end
```

```ruby
  self.nesting = :admin, Department
```



## 13. Internationalisierung (I18n)

Hierarchisches Lookup:
```ruby
people.index.title: "Die Personen"
```
Fallback:

Controller

Parent-Controller

Global

Kein Überschreiben ganzer Views nötig.