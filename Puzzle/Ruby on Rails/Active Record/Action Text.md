


# Action Text in Rails

Action Text bringt einen Rich-Text-Editor (Trix) in Rails. Damit kannst du formatierten Text speichern, z. B.:

- Fett/Kursiv
- Listen
- Links
- Bilder & Attachments

Rails speichert den Inhalt automatisch über Active Storage.
Es geht nach WYSIWYG

##### Was heist WYSIWYG
<details>
<summary>Answer</summary>
What you see is what you get
</details>


---

# Installation

## 1. Action Text installieren

```
bin/rails action_text:install
```

Dadurch passiert automatisch:

- Installation von `trix` und `@rails/actiontext`
- Erstellung der nötigen Migrationen
- Erstellung von CSS-Dateien
- Einrichtung von Active Storage Tabellen

---

## 2. Migration ausführen

```
bin/rails db:migrate
```

---

# Model vorbereiten

Beispiel: `Message`

```
class Message < ApplicationRecord  has_rich_text :contentend
```

Damit bekommt das Model ein Rich-Text-Feld namens `content`.

---

# Formular verwenden

In deinem Form:

```
= form_with model: @message do |f|  = f.label :content  = f.rich_text_area :content  = f.submit
```

Da du HAML verwendest, passt das direkt für dein Projekt.

---

# Controller

Strong Params erlauben:

```
def message_params  params.require(:message).permit(:content)end
```

---

# Ausgabe im View

```
= @message.content
```

Rails rendert den HTML-Inhalt automatisch sicher.





