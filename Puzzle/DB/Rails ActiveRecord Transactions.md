
## 1. Normale Transaction

Rails startet und committet die SQL-Befehle vollautomatisch im Hintergrund.

Ruby

```ruby
Role.transaction do
  Role.create!(name: "/sys")
  Role.create!(name: "/ux")
end
```

SQL

```sql
BEGIN;
INSERT INTO roles (name) VALUES ('/sys');
INSERT INTO roles (name) VALUES ('/ux');
COMMIT;
```

Alle oder gar nichts wird gespeichert

## 2. Standard-Exception = Automatischer Rollback

Wenn eine Exception den Transaktionsblock verlässt, rollt Rails die gesamte Transaktion zurück. Rails fängt die Exception jedoch nicht ab. sie steigt im Ruby-Callstack weiter nach oben (_bubbling up_).

Ruby

```ruby
Role.transaction do
  Role.create!(name: "/sys")
  raise "Boom"
  Role.create!(name: "/ux")
end
```

- Rollback: Sys wird nicht gespeichert


## 3. Der Spezialfall: `ActiveRecord::Rollback`

Manchmal möchte man die Datenbank zurückrollen, aber den Programmfluss im Ruby-Code nicht durch eine abstürzende App unterbrechen. Genau dafür existiert `ActiveRecord::Rollback`.

Ruby

```ruby
Role.transaction do
  Role.create!(name: "/sys")
  raise ActiveRecord::Rollback
  Role.create!(name: "/ux")
end
puts "Hier läuft der Code ganz normal weiter!"
```

Rollback ohne error. Der rest des codes läuft weiter

### Unterschied im Verhalten:

| **Fehlerklasse**                | **Rollback ausgelöst?** | **Exception nach aussen sichtbar?** |
| ------------------------------- | ----------------------- | ----------------------------------- |
| `StandardError` / Eigene Fehler | **Ja**                  | **Ja**                              |
| `ActiveRecord::Rollback`        | **Ja**                  | **Nein**                            |

## 4. Verschachtelung & Savepoints (`requires_new`)

Standardmässig sind Transaktionen in Rails nicht echt verschachtelt. Wenn du einen `transaction`-Block in einen anderen packst, verschmelzen sie zu einer einzigen grossen Transaktion. Möchtest du Teil-Transaktionen, brauchst du `requires_new: true`.

Ruby

```ruby
Role.transaction do
  Role.create!(name: "/sys")

  # Nutzt SQL-Savepoints dank 'requires_new: true'
  Role.transaction(requires_new: true) do
    Role.create!(name: "/ux")
    raise ActiveRecord::Rollback
  end
  
  Role.create!(name: "admin")
end
```

**Datenbank-Mental-Model (SQL):**

SQL

```sql
BEGIN;
INSERT INTO roles (name) VALUES ('/sys');

SAVEPOINT active_record_1;
INSERT INTO roles (name) VALUES ('/ux');
ROLLBACK TO SAVEPOINT active_record_1;

INSERT INTO roles (name) VALUES ('admin');
COMMIT;
```
/ux ist das einzige was das rollback betrift.

## 5. Rollback-Kontext-Regel

`ActiveRecord::Rollback` hat ausschliesslich eine Bedeutung, wenn es innerhalb eines aktiven Transaktions-Blocks geworfen wird.

Ruby

```ruby
# Buns
raise ActiveRecord::Rollback 
```

## 6. Das Return-Value-Pattern (Oft übersehen)

Der Rückgabewert eines Transaktions-Blocks ist immer der Wert der letzten ausgeführten Zeile innerhalb des Blocks.

Ruby

```ruby
result = Role.transaction do
  Role.create!(name: "/sys")
  :yupi
end

puts result
# => :erfolgreich
```

`Return-Value ≠ Commit-Status`. Der Block gibt den Wert auch dann zurück, wenn darin logische Fehler passieren, solange keine Exception geworfen wird.

Transactions fixt deine logic nicht wenn sie nicht geht
## 7.`save` vs. `save!`

Da Transaktionen zwingend auf Exceptions angewiesen sind, um einen Rollback einzuleiten, dürfen innerhalb des Blocks nur Methoden verwendet werden, die im Fehlerfall eine Exception werfen (z.B. `.save!`, `.create!`, `.update!`).

Ruby

```ruby
# Verhindert den Rollback bei Validierungsfehlern!
Role.transaction do
  user1.save  
  user2.save
end

# Garantiert den Rollback!
User.transaction do
  user1.save! 
  user2.save!
end
```

## 8. Das `rescue`-Anti-Pattern

Wenn du eine Exception innerhalb des Transaktionsblocks abfängst und **nicht** erneut wirfst, bekommt Rails den Fehler nicht mit und führt am Ende des Blocks fälschlicherweise ein `COMMIT` aus.

Ruby

```ruby
# FALSCH: Dateninkonsistenz vorprogrammiert
Role.transaction do
  Role.create!(name: "/sys")
  
  begin
    Role.create!(name: nil) # Wirft Validierungsfehler
  rescue ActiveRecord::RecordInvalid => e
    Rails.logger.error("Fehler abgefangen: #{e.message}")
  end
end

#  RICHTIG: Fehler abfangen, loggen und Rollback triggern
Role.transaction do
  Role.create!(name: "/sys")
  
  begin
    Role.create!(name: nil)
  rescue ActiveRecord::RecordInvalid
    raise ActiveRecord::Rollback # Expliziter, stiller Rollback!
  end
end
```

## 9. Ruby-RAM vs. Datenbank-Zustand

Ein Rollback setzt **nur** den Zustand innerhalb der Datenbank zurück. Die Instanzvariablen deines Ruby-Objekts im Arbeitsspeicher (RAM) behalten die manipulierten Werte!

Ruby

```ruby
role = Role.create!(name: "Alt")

Role.transaction do
  role.name = "Neu"
  role.save!
  raise ActiveRecord::Rollback
end
```

## 11. `return` oder `break` im Block

Was passiert, wenn du einen Transaktionsblock vorzeitig mittels `return` verlässt?

Ruby

``` ruby
def setup_account
  Role.transaction do
    Role.create!(name: "/ux")
    return "Vorzeitiger Exit" 
    Role.create!(name: "Nicht erreichbar")
  end
end
```
ux wird gesetzt der rest nicht. Aber auch kein rollback


## 12. Pessimistic Locking (`with_lock`)

Wie du richtig erkannt hast, schützen Transaktionen nicht vor Logik-Bugs oder parallelen Zugriffen (Race Conditions). Wenn zwei User zeitgleich dasselbe Bankkonto leeren wollen, hilft `with_lock`.

`with_lock` startet automatisch eine Transaktion und blockiert die Zeile in der DB für andere Prozesse (`FOR UPDATE`).

Ruby

``` ruby
account = Account.first

account.with_lock do
  # SQL: SELECT * FROM accounts WHERE id = 1 FOR UPDATE;
  new_balance = account.balance - 50
  account.update!(balance: new_balance)
end
```

## 13. Grenzen bei Multi-Database-Systemen

Transaktionen sind immer an eine **konkrete Datenbankverbindung** gekoppelt. Wenn deine App Daten über mehrere Datenbanken verteilt hat, schützt ein einfacher Block nicht beide Systeme.

## 14. Isolation Levels (Datenbank-Feineinstellungen)

Falls du hochsensible Daten validierst, kannst du Rails anweisen, das Isolationslevel der Datenbank für diese eine Transaktion hochzuschrauben:

Ruby

``` ruby
Role.transaction(isolation: :serializable) do
  # Absolut sichere, aber langsame Operation
end
```

| **Isolation Level**          | **Performance** | **Schutz gegen...**                                                                          |
| ---------------------------- | --------------- | -------------------------------------------------------------------------------------------- |
| `:read_committed` (Standard) | Sehr schnell    | Verhindert das Lesen ungespeicherter Daten (Dirty Reads).                                    |
| `:repeatable_read`           | Mittel          | Garantiert, dass Daten sich während des Lesens im Block nicht ändern.                        |
| `:serializable`              | Langsam         | Schaltet die höchste Stufe frei. Simuliert, dass alle Zugriffe strikt nacheinander ablaufen. |
