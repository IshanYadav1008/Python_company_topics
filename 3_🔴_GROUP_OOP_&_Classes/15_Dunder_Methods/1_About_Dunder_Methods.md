1. Dunder Methods hote kya hain ?

- Dunder Methods Python ke special methods hote hain, jinke naam 
  ke aage aur peeche double underscore (__) hota hai.

- Dunder ka matlab hai Double Underscore.

Dekho, ye kuch aise dikhte hain:
--------------------------------

__init__  : Object initialize karna
            Object ko initial values dene mein kaam aata hai.

__len__   : Length batana
            len(obj) chalane par kaam aata hai.

__eq__    : Do objects ki equality check karna
            obj1 == obj2 ke liye use hota hai.

__add__   : Addition ka behavior define karna
            obj1 + obj2 ke liye use hota hai.

* In sabhi names mein shuru aur end mein __ hai, isliye inhe 
  Dunder Methods kaha jata hai.

==============================================================================

2. Ye methods hote kyun hain?

* Ek simple example se samjho. Maan lo Python mein hum do numbers 
  add karte hain:

CODE:
-----
a = 10
b = 20
print(a + b)

Output: 30

* Python ko pehle se pata hai ki numbers ko + karne ka kya matlab 
  hai.

------------------------------------------------------------------------------

# Lekin ab hum apni khud ki class banate hain:

CODE:
-----
class Box:
    def __init__(self, value):
        self.value = value

box1 = Box(10)
box2 = Box(20)
print(box1 + box2)

- Ab sawaal hai: Python ko kaise pata chalega ki do Box objects ko + 
                 karne par kya karna hai?

- Kya unke value ko add karna hai? Ya dono boxes ko kisi aur tareeke 
  se combine karna hai?

- Python khud tumhare custom objects ke liye ye decision nahi le sakta. 
  Humein use batana padega.

- Yahin par __add__ kaam aata hai!

==============================================================================

3. Dunder Methods ka actual kaam:

* Dunder Methods se hum Python ko batate hain ki hamare objects ke 
  saath kuch common operations hone par kya behavior hona chahiye.

Tumhara object
Example: box1
      |
Python operation
Example: box1 + box2
      |
Related Dunder Method
Python __add__() ko use kar sakta hai.
      |
Tumhare define kiye hue rules ke according result

* Dhyan do: ye ek conceptual flow hai. Python ke operators ka actual 
            behavior operand types aur doosre special rules par bhi 
            depend karta hai.

==============================================================================

4. Dunder Methods ke bina aur saath mein:

* Pehle bina __add__ ke code dekho:

CODE:
-----
class Box:
    def __init__(self, value):
        self.value = value

box1 = Box(10)
box2 = Box(20)
print(box1 + box2)

* Custom Box objects ke liye yahan aam taur par TypeError aayega, kyunki 
  humne addition ka behavior define nahi kiya.

------------------------------------------------------------------------------

* Ab __add__ add karte hain:

CODE:
-----
class Box:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return self.value + other.value

box1 = Box(10)
box2 = Box(20)
print(box1 + box2)

Output:
-------
30

Ab samjho:
----------
- box1 + box2              — woh operation jo hum likhte hain.

- __add__                  — woh method jo define karta hai ki addition 
                             kaise hoga.

- self.value + other.value — humne rule banaya ki dono boxes ki values 
                             add hongi.

- return                   — result wapas deta hai.

* Yaani Dunder Method se hum apni class ke objects ka behavior customize 
  kar sakte hain.

==============================================================================

5. Kuch important Dunder Methods ek table mein:

__init__      -> Object initialize karna
__str__       -> Object ko readable text mein dikhana
__len__       -> len(obj)
__eq__        -> obj1 == obj2
__add__       -> obj1 + obj2
__getitem__   -> obj[index]

==============================================================================

6. Ek important baat yaad rakho:

Dunder Methods ko aam taur par Python khud kisi operation ke 
       dauraan call karta hai.

Jaise:
------
=> len(my_object)  // Python suitable __len__ method ko call karta hai.

Isi tarah:
----------
obj1 == obj2      // Python equality behavior ke liye __eq__ ko use kar 
                     sakta hai.

* Humein har baar aise likhne ki zaroorat nahi hoti:
=> my_object.__len__()

* Hum aam taur par Python ka normal syntax use karte hain:
=> len(my_object)

* Ek exception samjho: __init__ ko object initialization ke process mein 
                       Python automatically call karta hai, jabki __new__ 
                       object creation ke process mein involved hota hai.