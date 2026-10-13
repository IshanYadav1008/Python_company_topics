# Data Classes kya hoti hain ?

* Python mein Data Class ek aisi class hoti hai jiska main kaam data ko 
  store karna hota hai. Isme Python automatically kuch methods bana deta 
  hai, jisse humein baar-baar code likhne ki zaroorat nahi padti.

1. Normal class se samjho:
--------------------------
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __repr__(self):
        return f"Student(name={self.name!r}, age={self.age!r})"

s1 = Student("Rahul", 20)
print(s1)

Output:
-------
Student(name='Rahul', age=20)

* Yahan humne khud __init__() aur __repr__() likhe hain.

==============================================================================

2. Ab wahi kaam Data Class se karo:
-----------------------------------

CODE:
-----
from dataclasses import dataclass

@dataclass
class Student:
    name: str
    age: int

s1 = Student("Rahul", 20)
print(s1)

Output:
-------
Student(name='Rahul', age=20)

* Dekho, is baar humne __init__() aur __repr__() nahi likhe, 
  phir bhi dono kaam ho gaye! Python ne ye methods 
  automatically generate kar diye.

==============================================================================

3. Dono mein difference:
------------------------

Normal Class:
    __init__() khud likhna pad sakta hai
    __repr__() khud likhna pad sakta hai

Data Class:
    @dataclass lagao
    Python ye methods automatically generate kar sakta hai

* Yaad rakhna: Data Class ka use tab useful hota hai jab class ka main 
  purpose data ko rakhna aur represent karna ho, jaise Student, Employee, 
  Product ya Book ki details.

* @dataclass lagane ke liye from dataclasses import dataclass likhna zaroori 
  hai. Aur name: str, age: int batate hain ki in attributes ke expected types 
  kya hain; Python automatically in types ko enforce nahi karta.

==============================================================================
------------------------------------------------------------------------------
==============================================================================

DOUBT:
------
muje es code mai ek baat smj nhi aayi ki...

CODE:
-----
from dataclasses import dataclass

@dataclass
class Student:
    name: str
    age: int

s1 = Student("Rahul", 20)
print(s1)

* arguments ki values bina parameters ke kaise accept ho rhi hai ?

==============================================================================

* Iska jawab hai: @dataclass automatically __init__() method bana deta hai.

* Tumhare code mein __init__() dikh nahi raha, lekin Python usse background 
  mein generate kar deta hai.

1. Tumhara Data Class code:
---------------------------
from dataclasses import dataclass

@dataclass
class Student:
    name: str
    age: int

s1 = Student("Rahul", 20)
print(s1)

* Yahan Student("Rahul", 20) mein "Rahul" aur 20 arguments hain.

* Lekin ye arguments accept kaun kar raha hai? Automatically 
  generated __init__() method!

==============================================================================

2. Python internally aisa method generate karta hai:

* Tumhare Data Class code ko simple tarike se aise samajh 
  sakte ho:

class Student:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def __repr__(self):
        return f"Student(name={self.name!r}, age={self.age!r})"


Ab jab tum likhte ho:
---------------------
s1 = Student("Rahul", 20)

Toh values aise assign hoti hain:
---------------------------------
"Rahul"  -> name -> self.name
20       -> age  -> self.age

Aur print(s1) ka output hota hai:
---------------------------------
Student(name='Rahul', age=20)

==============================================================================

3. Toh kya __init__() likhna zaroori nahi hai ?

* Data Class mein basic __init__() khud likhne ki zaroorat nahi hoti. 
  @dataclass use karne par Python fields ke basis par ise automatically 
  generate kar deta hai.

* Ek important baat: name : str aur age: int ko yahan fields kehte hain. 
                            In fields ke basis par hi Python ko pata chalta 
                            hai ki generated __init__() mein kaun-se parameters 
                            hone chahiye.

* Yaad rakho              : Normal class mein aam taur par __init__() tum 
                            likhte ho; Data Class mein Python tumhare liye 
                            likh deta hai.