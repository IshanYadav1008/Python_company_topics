* Chalo, ab samajhte hain ki Data Class mein automatically generated 
  __repr__() kaise kaam karta hai.

1. Pehle ye code dekho:
-----------------------
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

* Ab sawal hai : humne __repr__() likha hi nahi, phir itna informative 
                 output kaise aaya ?

Jawab          : @dataclass ne __repr__() method automatically generate 
                 kar diya.

=========================================================================

2. Python automatically kya banata hai ?

* Conceptually, generated method kuch aisa hota hai:

def __repr__(self):
    return f"Student(name={self.name!r}, age={self.age!r})"

--> Ye samajhne ke liye hai; Python internally implementation 
    thodi alag ho sakti hai.

-------------------------------------------------------------------------

Jab tum likhte ho:
------------------
=> print(s1)

-------------------------------------------------------------------------

Toh process kuch aisa hota hai:
-------------------------------

print(s1)
    |
    v
__str__() available hai?
    |
    | Nahi
    v
__repr__() use hota hai
    |
    v
Student(name='Rahul', age=20)

* Yahan Data Class ne __str__() automatically generate nahi kiya. 
  Isliye print(s1) default behavior ke through generated __repr__() 
  ka use karta hai.

=========================================================================

3. Output mein field names aur values kahan se aayi ?

=> s1 = Student("Rahul", 20)

Object mein values hain:
------------------------
name = 'Rahul'
age  = 20

* Generated __repr__() in fields aur unki values ko informative 
  format mein dikhata hai:

=> Student(name='Rahul', age=20)

Is output se turant pata chalta hai:
------------------------------------
- Object kis class ka hai : Student
- name ki value kya hai   : 'Rahul'
- age ki value kya hai    : 20

=========================================================================

4. Agar fields badal dein toh ?

CODE:
-----
from dataclasses import dataclass

@dataclass
class Employee:
    name: str
    salary: int
    department: str

e1 = Employee("Amit", 30000, "IT")
print(e1)

Output:
-------
Employee(name='Amit', salary=30000, department='IT')

* Python ne fields ke according representation khud bana di. 
  Tumhe manually __repr__() likhne ki zaroorat nahi padi.

=========================================================================

5. Ek important difference yaad rakho:

__init__()  -> Object ke attributes initialize karta hai.
__repr__()  -> Object ki informative representation deta hai.

* Data Class mein dono methods automatically generate hote hain, jab 
 tak tum unhe disable ya khud define nahi karte.

* Yaad rakhne wali baat: @dataclass class ke fields se automatically 
  aisa __repr__() banata hai jo object ka naam aur uske fields ki 
  values readable form mein dikhata hai.

=========================================================================
-------------------------------------------------------------------------
=========================================================================

Doubt:
------
ye __str__ nni banta __repr__ banata hai ?

-------------------------------------------------------------------------

* Haan, bilkul! @dataclass automatically __repr__() banata hai, 
  lekin __str__() nahi banata.

Example:
--------
from dataclasses import dataclass

@dataclass
class Student:
    name: str
    age: int

s1 = Student("Rahul", 20)
print(s1)
print(repr(s1))

Output:
-------
Student(name='Rahul', age=20)
Student(name='Rahul', age=20)

=========================================================================

Dono ka output same kyun hai?
-----------------------------

1. @dataclass ne __repr__() generate kiya.

2. __str__() define nahi hai.

3. print(s1) pehle __str__() use karne ki koshish karta hai. 
   Jab woh nahi milta, toh __repr__() use karta hai.

4. repr(s1) seedha __repr__() use karta hai.

-------------------------------------------------------------------------

Yaad rakho:
-----------
- @dataclass → automatically __init__() aur __repr__() generate 
  karta hai.

- __str__() → automatically generate nahi karta.

- Agar tum apna __str__() likh do, toh print(s1) uska output 
  dikhayega.