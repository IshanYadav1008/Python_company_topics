* Chalo, samajhte hain ki @dataclass fields ke basis par 
  __init__() automatically kaise banata hai.

1. Sabse pehle fields samjho:
-----------------------------
from dataclasses import dataclass

@dataclass
class Student:
    name: str
    age: int

Is code mein:
-------------
- name: str ek field hai.
- age: int ek field hai.

* Ye fields batati hain ki Student object mein kaun-kaun '
  sa data hoga.

==============================================================================

2. @dataclass kya karta hai ?

* Jab Python @dataclass dekhta hai, toh woh fields ko read karke 
  automatically ek __init__() method generate karta hai.

Conceptually, woh kuch aisa hota hai:
-------------------------------------
def __init__(self, name: str, age: int):
    self.name = name
    self.age  = age

* Tumhe ye method manually likhne ki zaroorat nahi hai.

==============================================================================

3. Ab object create karke dekho:

=> s1 = Student("Rahul", 20)

. Ye call, generated __init__() ko arguments deta hai:

Student("Rahul", 20)
        |       |
        v       v
       name    age
        |       |
        v       v
 self.name = "Rahul"
 self.age  =   20

--> Ab object ke andar ye values store hain:

=> print(s1.name)print(s1.age)

Output:
-------
Rahul
20

==============================================================================

4. Agar ek aur field add kar dein toh ?

from dataclasses import dataclass

@dataclass
class Student:
    name: str
    age: int
    city: str

------------------------------------------------------------------------------

* Ab Python automatically aisa __init__() generate karega:

def __init__(self, name: str, age: int, city: str):
    self.name = name
    self.age = age
    self.city = city

------------------------------------------------------------------------------

* Ab object banate waqt teen arguments dene honge:

=> s1 = Student("Rahul", 20, "Bhopal")

Output:
-------
print(s1.city)
# Bhopal

==============================================================================

5. Ek line mein yaad rakho:
---------------------------

* @dataclass class ke fields ko dekhkar automatically __init__() 
  generate karta hai, jo arguments ko object ke attributes mein 
  assign karta hai.

* Aur haan, name: str aur age: int type hints hain. Ye expected 
  types batate hain, lekin apne aap galat type ki value dene se 
  nahi rokte.