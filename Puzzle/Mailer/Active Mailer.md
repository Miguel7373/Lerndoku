Active Mailer ist eine Mailer-Engine von Ruby. Du kannst mit ihr genau bestimmen, wie du Mails senden willst.

Du kannst im `application_mailer` angeben, von wem aus diese Mails gehen sollen. Das ist die Mail, die dann als Absender dastehen wird.

```ruby
default from: 'skills@puzzle.ch'
```



In deinem spezifisch erstellten Mail-File kannst du dann die restlichen wichtigen Infos angeben. An wen das Mail gehen soll und auch das Subject, also alle weiteren Spezifikationen bis auf den Text des E-Mails.
````ruby
def update_user_reminder_email(person)
	mail(to: person.email, subject: 'Erneuere dein Skills Profil!')
end
````
Das ist dann auch die Methode, die du aufrufst, um die Mail zu versenden.



Den Inhalt der Mail kannst du über [[Template|Templates]] bestimmen.

Wenn du dein Mail über Mail-Relay oder auch in eine Sandbox versenden willst, brauchst du jetzt noch eine [[Config]].












## Running Formatter  
  
```bash  
# Check code formatting: npm run format:all  
# Format the code: npm run format  
```







src/assets/  
dist/  
.angular/  
# The following files are already getting formatted by eslint  
**/*.html  
**/*.ts