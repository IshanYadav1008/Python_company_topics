1. Duck Typing kya hoti hai ?
-----------------------------

* Duck typing Python ka ek concept hai jismein hum ye nahi dekhte 
  ki object kis class ka hai. Hum dekhte hain ki woh object kya 
  kaam kar sakta hai.

Ek famous line hai:
-------------------
- “If it walks like a duck and quacks like a duck, it’s probably a 
   duck.”

* Matlab agar koi cheez duck ki tarah chalti hai aur duck ki tarah 
  awaaz nikalti hai, toh uske kaam ko dekhkar hum use duck jaisa 
  maan sakte hain.

* Python mein bhi isi tarah, agar object ke paas required method 
  hai, toh hum us method ko call kar sakte hain.

================================================================================

2. Sabse simple Python example
------------------------------

class Dog:
    def speak(self):
        print("Woof!")

class Cat:
    def speak(self):
        print("Meow!")

def make_sound(animal):
    animal.speak()

dog = Dog()
cat = Cat()

make_sound(dog)
make_sound(cat)

Output:
-------
Woof!
Meow!

Samjho kya hua:
---------------
- Dog class mein speak() method hai.
- Cat class mein bhi speak() method hai.
- make_sound() function ko farak nahi padta ki object Dog ka hai ya Cat ka.
- Function bas itna expect karta hai ki object par .speak() call ho sake.

Yahi Duck Typing hai!

--------------------------------------------------------------------------------

Concept ko visualize karo
-------------------------

make_sound(animal)
Function ko animal ka exact class type jaanne ki zaroorat nahi.

Dog                   Cat
speak() → Woof!       speak() → Meow!
 

- Dono objects ka type alag hai, lekin dono required behaviour 
  provide karte hain.

================================================================================

3. Real developer example:
--------------------------

* Maan lo tum ek application bana rahe ho jismein alag-alag tarah ki 
  files ko read karna hai.

CODE:
-----
class PDF:
    def read(self):
        print("Reading PDF file")

class WordDocument:
    def read(self):
        print("Reading Word document")

def open_file(file):
    file.read()

pdf = PDF()
word = WordDocument()

open_file(pdf)
open_file(word)

Output:
-------
Reading PDF file
Reading Word document

- open_file() ko bas itna chahiye ki object ke paas read() method ho. 
  Use ye check karne ki zaroorat nahi ki object PDF hai ya Word 
  document.

- Kal ko tum ExcelFile class bana do aur usmein bhi read() method ho, 
  toh wahi function uske saath bhi kaam kar sakta hai.

================================================================================

4. Agar method hi nahi hua toh?
-------------------------------

CODE:
-----
class Phone:
    def call(self):
        print("Calling...")

def make_sound(animal):
    animal.speak()

phone = Phone()
make_sound(phone)

- Ye code AttributeError dega, kyunki Phone object ke paas speak() method 
  nahi hai.

- Matlab Duck Typing ka ye matlab nahi hai ki har object har function ke 
  saath kaam karega. Object mein woh behaviour hona chahiye jo function 
  use karna chahta hai.

================================================================================

5. Duck Typing vs Type Checking
-------------------------------

Type checking approach	              Duck typing approach
------------------------------------------------------------------------
Object ka type check kar sakte hain	  Object ka required behaviour use 
                                      karte hain.
------------------------------------------------------------------------
Example: isinstance(animal, Dog)	  Example: animal.speak()
------------------------------------------------------------------------
Specific class par depend kar    	  Alag classes ke compatible objects 
sakta hai                             ke saath kaam kar sakta hai

* Python mein isinstance() use karna galat nahi hai. Bas jab exact type 
  important na ho aur required behaviour sufficient ho, tab duck typing 
  code ko flexible bana sakti hai.

================================================================================

6. Ab tumhara chhota test
-------------------------

Question: make_sound(animal) function ko Dog aur Cat dono objects ke saath 
          kaam karne ke liye kya zaroori hai?

Answer) Dono objects mein speak() method hona chahiye

- Bilkul sahi! Duck typing mein required behaviour important hai, exact 
  class nahi.

* Ek line mein yaad rakho : Duck typing ka matlab hai — object ka exact type 
                            dekhne ke bajaye, uske required behaviour par 
                            depend karna.