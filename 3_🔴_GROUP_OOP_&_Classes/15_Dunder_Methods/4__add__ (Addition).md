1. __add__ hota kya hai ?

* __add__ Python ka Dunder Method hai, jo define karta hai ki + operator 
  use karne par hamare objects ke saath kya hona chahiye.

Normal Python mein: 
-------------------
a = 10
b = 20
print(a + b)

Output: 30   // Python ko numbers add karna pehle se aata hai.

* Lekin agar hum apni class ke objects ko add karna chahein, toh 
  humein addition ka rule define karna pad sakta hai.

==================================================================================

2. Example se samjho:
---------------------
class Box:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return self.value + other.value

b1 = Box(10)
b2 = Box(20)
print(b1 + b2)

Output: 30

==================================================================================

3. Ye kaise kaam kar raha hai?

Jab tum likhte ho:
------------------
=> print(b1 + b2)

- Python + operator ke liye __add__() method ko use karta hai.

Conceptually:
-------------
=> print(b1.__add__(b2))

Ab method ke andar:
-------------------
def __add__(self, other):    
return self.value + other.value

- self → b1 object, jisme value = 10
- other → b2 object, jisme value = 20

Toh calculation hoti hai:
-------------------------
=> return 10 + 20

- Result 30 return hota hai, aur print() use display karta hai.

==================================================================================

4. Poora flow:

b1 + b2
   |
b1.__add__(b2)
   |
self.value + other.value
10 + 20
   |
Result: 30

==================================================================================

5. Ek line mein yaad rakho:

Dunder Method	          Operator	          Kaam
-------------------------------------------------------------------------------
__len__	                  len(obj)	          Length nikalna
__eq__	                  obj1 == obj2	      Equality check karna
__add__	                  obj1 + obj2	      Addition ka behavior define karna
-------------------------------------------------------------------------------

Ab tum batao
------------
Agar b1 ki value 5 hai aur b2 ki value 7 hai, aur __add__ dono values ko add karta hai, toh print(b1 + b2) ka output kya hoga?

ANS) Bilkul sahi! 5 + 7 = 12.