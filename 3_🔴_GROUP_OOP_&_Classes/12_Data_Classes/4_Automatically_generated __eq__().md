* Chalo, ab Automatically generated __eq__() ko simple way mein samajhte 
  hain.

1. __eq__() kya karta hai ?
---------------------------
* __eq__() ka kaam do objects ke data ko compare karna hai.

* Data Class mein @dataclass automatically __eq__() generate 
  karta hai, jo dono objects ke fields ki values compare karta 
  hai.

============================================================================

2. Example dekho:
-----------------

from dataclasses import dataclass

@dataclass
class Student:
    name: str
    age: int

s1 = Student("Rahul", 20)
s2 = Student("Rahul", 20)
s3 = Student("Amit", 22)

print(s1 == s2)
print(s1 == s3)

Output:
-------
True
False

----------------------------------------------------------------------------

Aisa kyun hua ?
---------------
- s1 aur s2 alag objects hain, lekin unka name aur age same hai. 
  Isliye s1 == s2 ka result True hai.

- s1 aur s3 ka data alag hai. Isliye s1 == s3 ka result False hai.

============================================================================

3. Python internally kya compare karta hai ?

* Data Class ka generated __eq__() conceptually kuch aisa kaam karta 
  hai:

def __eq__(self, other):
    if self.__class__ is other.__class__:
        return (
            self.name == other.name
            and self.age == other.age
        )
    return NotImplemented

* Ye samajhne ke liye simplified example hai; actual generated 
  implementation thodi alag ho sakti hai.

* Matlab Python pehle check karta hai ki dono objects ki class 
  same hai, phir unke fields compare karta hai.

============================================================================

4. Ek important difference: == aur is:

print(s1 == s2)
print(s1 is s2)

Output:
-------
True
False

- == → Objects ka data compare karta hai.
- is → Check karta hai ki dono variables usi ek object ko refer 
       kar rahe hain ya nahi.

* s1 aur s2 ka data same hai, lekin dono alag objects hain.

----------------------------------------------------------------------------

# Yaad rakhne ka shortcut:

__init__()  -> Object mein data set karta hai.
__repr__()  -> Object ka informative output deta hai.
__eq__()    -> Do objects ke data ko compare karta hai.

Note: Ye automatic __eq__() behavior Data Class mein default hota hai. 
      Agar tum @dataclass(eq=False) likhoge, toh Python ise automatically 
      generate nahi karega.

============================================================================
----------------------------------------------------------------------------
============================================================================

Doubt:
------
lekin upr waale example mai __eq__() use kaha hua ? or ye __eq__() 
kahi dikha bhi nahi

----------------------------------------------------------------------------

* Bilkul sahi! Tumhare code mein __eq__() kahin bhi likha hua nahi hai. 
  @dataclass ise automatically generate karta hai, aur jab tum == use 
  karte ho, tab ye method call hota hai.

1. Tumhara original code:
-------------------------
from dataclasses import dataclass

@dataclass
class Student:
    name: str
    age: int

s1 = Student("Rahul", 20)
s2 = Student("Rahul", 20)
print(s1 == s2)

Output:
-------
True

============================================================================

2. __eq__() use kahan hua?

Yahan:
------
print(s1 == s2)

----------------------------------------------------------------------------

* Jab Python s1 == s2 dekhta hai, toh woh internally __eq__() method 
  ka use karta hai.

s1 == s2

----------------------------------------------------------------------------

* Conceptually, ise aise samajh sakte ho:

s1.__eq__(s2)

--> Aur @dataclass ne __eq__() pehle hi automatically bana diya tha.

============================================================================

3. Agar @dataclass na hota toh ?

* Tab tumhe apna __eq__() likhna pad sakta tha:

CODE:
-----
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __eq__(self, other):
        return self.name == other.name and self.age == other.age

s1 = Student("Rahul", 20)
s2 = Student("Rahul", 20)
print(s1 == s2)

Output:
-------
True

--> Is baar humne __eq__() khud likha hai.

----------------------------------------------------------------------------

Yaad rakho:
-----------
- @dataclass → __eq__() automatically generate karta hai.

- ==         → Comparison karte waqt __eq__() ko use karta hai.

- Tumhe __eq__() ko manually call karne ki zaroorat nahi hai.