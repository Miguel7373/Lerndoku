
Ich würde sagen, dass sie auf einer kleinen Skala ganz nützlich sein können. Aber sie fördern natürlich auch wieder die Komplexität und verlieren somit an Einfachheit beim Debuggen, was ärgerlich ist. 

Sie können aber auch extrem praktisch sein. Die Tests sind dann folgendermassen aufgebaut. Du beginnst deine Tests mit einem.

````ruby
RSpec.shared_examples 'a model that touches the associated person' do

````


Das führt dazu, dass Rails realisiert, dass das nun shared examples sind, und du kannst sie dann mehrmals aufrufen.

````ruby
describe Education do  
  fixtures :educations  
  
  let(:record) { educations(:bsc) }  
  
  it_behaves_like 'a model with date range validations'  
  it_behaves_like 'a model that touches the associated person'  
end
````

Indem du sie in einem describe mit einem `it_behaves_like` aufrufst und dann den Namen deines shared examples Test nennst.



Ebenfalls cool ist, dass du ihnen variablen mitgeben kannst
````ruby
let(:record) { educations(:bsc) }  
````


Diese kannst du dann auch in dem Test verwenden, unter dem Namen, den du ihnen hier gibst, wie hier `record`.
````ruby
# RSpec.shared_examples 'a model that touches the associated person' do  
 # context 'on update' do  
 #   it 'updates updated_at on the associated person' do  
 #     person_updated_at = record.person.updated_at  
      record.save!  
 #     expect(record.person.reload.updated_at).to be > person_updated_at  
 #   end  
 # endend
````
