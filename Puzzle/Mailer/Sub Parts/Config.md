```ruby
config.action_mailer.smtp_settings = {
address: ENV['MAIL_SERVER_ADDRESS'],
port: 25,
user_name: ENV['MAIL_SERVER_USERNAME'],
password: ENV['MAIL_SERVER_PASSWORD'],
enable_starttls_auto: true,
delivery_method: :smtp,
authentication: :plain
}
```

In der Config definierst du einen Mailserver, also ob du es in eine Sandbox senden willst oder einen Mailing-Server hast, der das Mail für dich sendet. In der Config kannst du auch die Verschlüsselung und anderes, was das Mail beeinflusst, definieren. 
#### Sandbox 
Eine Sandbox wäre zum Beispiel *Mail-Trab*. Diese kannst du gratis verwenden, du musst dich nur anmelden. Eine Sandbox fängt das Mail ab, das du gerade heraussenden wolltest, und du kannst dir dort das ganze Mail ansehen, mit allen Einzelteilen.

#### Mailing-Server 
Bei einem Mailing-Server brauchst du einen User, mit dem du dich dann anmelden kannst.

[[Active Mailer|<- Zurück]]

