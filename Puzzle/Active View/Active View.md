

### [](https://codimd.puzzle.ch/VkW0LPecTH2Ei0PC2YJnyw#Was-ist-Action-View "Was-ist-Action-View")Was ist Action View

Action View ist das V in MVC. Der Action Controller und die Action View arbeiten hierbei zusammen um web request zu handhaben. Dabei ist der Action Controller dafür zuständig mit der Model layer zu kommunizieren und Daten zu holen. Die Action View ist dann dafür zuständig dem web request einen response body mit den Daten aus dem Model zu rendern.

Per default sind die Action View templates (views) in ERB geschrieben.

**Für was steht ERB?**

### [](https://codimd.puzzle.ch/VkW0LPecTH2Ei0PC2YJnyw#HAML "HAML")HAML

Steht für “HTML Abstraction Markup Language”.

**Warum HAML anstatt ERB?**

- Keine closing-tags. Einrückung ist king
- Einfacher zu debuggen, einfacher zu lesen -> HAML should be beautiful, simple, and readable like that [haiku](https://www.wikihow.com/Write-a-Haiku-Poem) from back in grade school.
- Super DRY
- Effizienter & schnell zu lernen

### [](https://codimd.puzzle.ch/VkW0LPecTH2Ei0PC2YJnyw#Partials "Partials")Partials

Partial templates sind eine möglichkeit views in kleinere wiederverwendbare chunks aufzuteilen. Dieses kann dann an beliebigen orten wieder aufgerufen werden. Es bietet auch die möglichkeit an Daten von dem main template an ein partial zu passen.

Um ein partial anzuzeigen verwendet man die `render partial:` methode.

```
= render partial: 'error_message'
```

Um Daten an ein Partial zu passen wird die `locals` option verwendet.

```
-# index.html.haml
= render partial: "beautiful_partial", locals: {person: @person}

-# _beautiful_partial.html.haml
= person.name
```

Collection rendern:

```
- @products.each do |product|
    = render partial: "product", locals: { product: product }
  
-# Bessere Lösung
= render partial: "product", collection: @products
```

**Auf was sollte man achten wenn man ein partial erstellt?**

### [](https://codimd.puzzle.ch/VkW0LPecTH2Ei0PC2YJnyw#Layouts "Layouts")Layouts

Layouts werden verwendet um ein view template rund um die “normalen” controller resultate zu displayen. Ein common usecase davon sind zum beispiel header oder footer.

### [](https://codimd.puzzle.ch/VkW0LPecTH2Ei0PC2YJnyw#Helpers "Helpers")Helpers

Rails bietet viele helpermethods zur Verwendung mit Action View. Einige beispiele:

```
# time_ago_in_words
time_ago_in_words(3.minutes.from_now)
# => 3 minutes

# truncate
truncate("Once upon a time in a world far far away", length: 17)
# => "Once upon a ti..."

# sanitize
sanitize @article.body
# with permitted tags and attributes
sanitize @comment.body, tags: %w(strong em a), attributes: %w(href)

# image_tag
image_tag("icon.png")
# => <img src="/assets/icon.png" />

# stylesheet_link_tag
stylesheet_link_tag("application")
# => <link href="/assets/application.css" rel="stylesheet" />

# tag
tag.h1 "All titles fit to print"
# => <h1>All titles fit to print</h1>
tag.div "Hello, world!"
# => <div>Hello, world!</div>

# benchmark
- benchmark 'Process data files' do
  = expensive_files_operation
```

### [](https://codimd.puzzle.ch/VkW0LPecTH2Ei0PC2YJnyw#Form-Helpers "Form-Helpers")Form Helpers

Form helpers sind noch einmal eine eigene Geschichte.

#### [](https://codimd.puzzle.ch/VkW0LPecTH2Ei0PC2YJnyw#Basic-forms "Basic-forms")Basic forms

Diese option wird verwendet um manuell forms zu erstellen, ohne ActiveRecord modells einzusetzen.

```
# Basic web search form
= form_with url: "/search", method: :get do |form|
  = form.label :query, "Search for:"
  = form.search_field :query
  = form.submit "Search"
```

Helpers die man benutzen kann:

- Checkboxes
- Readio buttons
- usw

#### [](https://codimd.puzzle.ch/VkW0LPecTH2Ei0PC2YJnyw#Forms-mit-models "Forms-mit-models")Forms mit models

Der `form_with` helper hat eine `:model` option die es erlaubt den form builder an das model objekt zu binden. Das bedeutet, dass das Formular auf dieses model ausgerichtet wird und die Felder des forms mit Werten aus diesem model gefüllt werden.

```
= form_with model: @book do |form|
  %div
    = form.label :title
    = form.text_field :title
  %div
    = form.label :author
    = form.text_field :author
  = form.submit
```

#### [](https://codimd.puzzle.ch/VkW0LPecTH2Ei0PC2YJnyw#Form-selects "Form-selects")Form selects

```
= form.select :city, ["Berlin", "Chicago", "Madrid"]

= form.select :city, [["Berlin", "BE"], ["Chicago", "CHI"], ["Madrid", "MD"]]
```

oder auch so wenn man opions groupen möchte:

```
= form.select :city,                                    
  {                                                     
    "Europe" => [ ["Berlin", "BE"], ["Madrid", "MD"] ], 
    "North America" => [ ["Chicago", "CHI"] ],          
  },                                                    
  selected: "CHI"                                       
```

Natürlich kann man auch hier wieder models anbinden.

Person erstellen:

```
@person = Person.new(city: "MD")
```

Form mit model erstellen:

```
= form_with model: @person do |form|
  = form.select :city, [["Berlin", "BE"], ["Chicago", "CHI"], ["Madrid", "MD"]]
```

-> Führt dazu das ‘Madrid’ automatisch selected wird.

#### [](https://codimd.puzzle.ch/VkW0LPecTH2Ei0PC2YJnyw#Collection-helpers "Collection-helpers")Collection helpers

```
= form.collection_select :city_id, City.order(:name), :id, :name
```

würde diesem HTML übereinstimmen

```
<select name="person[city_id]" id="person_city_id">
  <option value="1">Berlin</option>
  <option value="3">Chicago</option>
  <option value="2">Madrid</option>
</select>
```

### [](https://codimd.puzzle.ch/VkW0LPecTH2Ei0PC2YJnyw#Quellen "Quellen")Quellen:

[https://guides.rubyonrails.org/action_view_overview.html#layouts](https://guides.rubyonrails.org/action_view_overview.html#layouts)  
[https://haml.info/](https://haml.info/)  
[https://haml.info/docs/yardoc/file.REFERENCE.html](https://haml.info/docs/yardoc/file.REFERENCE.html)  
[https://uharston.medium.com/5-reasons-you-should-be-using-haml-instead-of-erb-4d93766bd6b3](https://uharston.medium.com/5-reasons-you-should-be-using-haml-instead-of-erb-4d93766bd6b3)  
[https://guides.rubyonrails.org/action_view_helpers.html](https://guides.rubyonrails.org/action_view_helpers.html)  
[https://guides.rubyonrails.org/form_helpers.html](https://guides.rubyonrails.org/form_helpers.html)  
[https://api.rubyonrails.org/v8.0.2/classes/ActionView/Helpers.html](https://api.rubyonrails.org/v8.0.2/classes/ActionView/Helpers.html)  
[https://www.wikihow.com/Write-a-Haiku-Poem](https://www.wikihow.com/Write-a-Haiku-Poem)