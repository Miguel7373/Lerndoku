Active Record ist in verbindung mit der datebase und muss ein table dahinter haben. Active Model dahingegen muss nicht mit einer DB verbunden sein sondern beited dir funktionen die dir erlauben ein model äliches konstruckt in purem ruby zu erschaffen

#### API
includes `ActiveModel::API` can be used with `form_with`, `render` and any other [Action View helper methods](https://api.rubyonrails.org/v8.0.2/classes/ActionView/Helpers.html), just like Active Record objects.


```
ActiveModel::AttributeAssignment
```
```
attr_accessor :name, :age
```
defines the attibutes of the model like object

```
  attribute :active, :boolean, default: true
```

```
Person.attribute_names
```
```
person.attributes
```




Uterschschied ActiveModel::API: A smaller subset than ActiveModel::Model

Model is the bigger pack it brings the modul Naming in the mix witch brings the whole view layer into the mix and not just the model Stuff like API dose
ActiveModel::API
- **`AttributeAssignment`**
- **`Attributes`**
- **`Conversion`**
- **`Validations`**
- **`Serialization`**
ActiveModel::Model
- everything from API
- **`Naming`** with brings `model_name`, `route_key`, and `singular_route_key` ... into the mix and alows you to use them in forms witch can be curtual



































address: 'smtp.mailrelay.com',  
port: '25',  
domain: 'mailrelay.puzzle.ch',  
user_name: ENV['MAILRELAY_USERNAME'],  
password: ENV['MAILRELAY_PASSWORD'],  
authentication: :login


user_name: '7c63694a3f5073',  
password: '92e9d944938cb2',  
address: 'sandbox.smtp.mailtrap.io',  
host: 'sandbox.smtp.mailtrap.io',  
port: '2525',  
authentication: :login



Prod
port: '25',                                      
authentication: :login
address: 'smtp.mailrelay.com',  
user_name: ENV['MAILRELAY_USERNAME'],  
password: ENV['MAILRELAY_PASSWORD'],  
domain: 'mailrelay.puzzle.ch',  


Int
port: '2525',  
authentication: :login
address: 'sandbox.smtp.mailtrap.io',  
user_name: '7c63694a3f5073',  
password: '92e9d944938cb2',  
host: 'sandbox.smtp.mailtrap.io',  

INT
ENV['EMAIL_PORT'] = '2525'
ENV['EMAIL_AUTH'] = :login
ENV['EMAIL:ADDRESS'] = 'sandbox.smtp.mailtrap.io'
ENV['EMAIL_USER_NAME'] = '7c63694a3f5073'
ENV['EMAIL_PASSWORD] = '92e9d944938cb2'

Prod
ENV['EMAIL_PORT'] = '25'
ENV['EMAIL_AUTH'] = :login
ENV['EMAIL:ADDRESS'] = 'smtp.mailrelay.com'
ENV['EMAIL_USER_NAME'] =
ENV['EMAIL_PASSWORD] =

INT
EMAIL_PORT=2525
EMAIL_AUTH=:login
EMAIL_ADDRESS=sandbox.smtp.mailtrap.io
EMAIL_USER_NAME=7c63694a3f5073
EMAIL_PASSWORD=92e9d944938cb2
EMAIL_DOMAIN=skills.com

Prod
EMAIL_PORT=25
EMAIL_AUTH=:login
EMAIL_ADDRESS=smtp.mailrelay.com
EMAIL_USER_NAME=
EMAIL_PASSWORD=
EMAIL_DOMAIN=
