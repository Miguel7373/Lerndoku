CanCanCan verwaltet alle Berechtigungen in:
```
app/models/ability.rb
```

In diesem file canst du von allen rollen die rechte anpassen wie zum beispiel hier:
```ruby
class Ability  
  include CanCan::Ability  
  
  def initialize(user)  
    initialize_user_rights(user)  
  
    role_initializers.each do |predicate, initializer|  
      send(initializer) if user.public_send(predicate)  
    end  
  end  
  private  
  
  def role_initializers  
    { 
      is_admin?: :initialize_admin_rights,  
    }  
  end  
  
  def initialize_user_rights(user)  
    user_classes.each do |user_class|  
      can :read, user_class  
      can :manage, user_class do |record|  
        record.person.auth_user_id == user.id  
      end  
    end    can :read, Skill  
    can :read, Person  
    can :manage, Person, auth_user_id: user.id  
  end  
  
  def initialize_admin_rights  
    initialize_editor_rights  
    admin_classes.each do |admin_class|  
      can :manage, admin_class  
    end  
  end  
  def user_classes  
    [Activity, AdvancedTraining, Education, Project, PeopleSkill, Contribution]  
  end  
  
  def admin_classes  
    [Certificate, Skill, UnifiedSkill, UnifiedSkillForm]  
  end  
end
```

| Begriff    | Bedeutung            |
| ---------- | -------------------- |
| `can`      | Erlaubnis erteilen   |
| `cannot`   | Erlaubnis verbieten  |
| `:manage`  | Alle Aktionen (CRUD) |
| `:read`    | Anzeigen             |
| `:create`  | Erstellen            |
| `:update`  | Bearbeiten           |
| `:destroy` | Löschen              |

### Verwenden

Du kannst nun wenn du eine abfrage machen willst ob jemand berechtigt ist nur noch 

`can?` schreiben und dann was du genau machen willst und dann noch das model also so:
`- if can? :update, @person`

#### Mit Bedingungen arbeiten

Du kannst Berechtigungen einschränken:

`can :update, Person, user_id: user.id?`

### Zugriff automatisch blockieren

Im Controller kannst du automatisch prüfen lassen:

```ruby
class PeopleController < ApplicationController  
  load_and_authorize_resource  
end
```

Wenn der User keine Rechte hat, wird automatisch:

`CanCan::AccessDenied`

ausgelöst.