* Ye teeno @dataclass ke advanced features/options hain. Inka use 
  Data Class ke behavior ko control ya customize karne ke liye 
  hota hai.

1. frozen=True — Object ko modify hone se rokna:

* Iska matlab hai ki object banne ke baad uske fields ko normal 
  assignment se change nahi kar sakte.

CODE:
-----
from dataclasses import dataclass

@dataclass(frozen=True)
class Student:
    name: str
    age: int

s1 = Student("Rahul", 20)
print(s1.name)
s1.age = 21  # Error

Output:
-------
Rahul
dataclasses.FrozenInstanceError

* Yahan s1.age = 21 karne par error aayega, kyunki class mein 
                 frozen=True hai.

* Yaad rakho: frozen=True object ko normal tareeke se modify 
              hone se rokta hai. Lekin ise har situation mein 
              completely immutable nahi samajhna chahiye.

============================================================================

2. order=True — Objects ko compare aur sort karna:

* Is option se Python ordering methods automatically generate 
  karta hai, jisse objects ko <, > aur sorting mein use kar 
  sakte ho.

CODE:
-----
from dataclasses import dataclass

@dataclass(order=True)
class Student:
    name: str
    age: int

s1 = Student("Amit", 20)
s2 = Student("Rahul", 18)

print(s1 < s2)

Output:
-------
True

* Kyun ? Python pehle name compare karta hai. "Amit" alphabetically 
         "Rahul" se pehle aata hai, isliye result True hai.

* Important: Comparison fields ke order mein hota hai. Agar pehla 
             field equal ho, tab Python agla field compare karta 
             hai.

============================================================================

3. field() — Kisi field ki settings customize karna:

* field() ka use kisi particular field ke liye extra settings dene 
  mein hota hai, jaise default value, comparison mein include karna 
  ya repr() mein dikhana.

Example:
--------
from dataclasses import dataclass, field

@dataclass
class Student:
    name: str
    age: int = field(default=18, repr=False)

s1 = Student("Rahul")
print(s1)
print(s1.age)

Output:
-------
Student(name='Rahul')
18

----------------------------------------------------------------------------

Yahan:
------
- default = 18    — Agar age ki value nahi di, toh default 18 hoga.
- repr    = False — age ko generated __repr__() ke output mein nahi 
                    dikhaya jayega.

* Dhyan do: age ko default value mili hai, isliye Student("Rahul") 
            likhna valid hai.

============================================================================

# Teeno mein difference:

frozen=True  --> Object ke fields ko modify karne se rokta hai.

order=True   --> Objects ke liye ordering/comparison methods 
                 generate karta hai.

field()      --> Kisi specific field ki settings customize karta 
                 hai.

Inhe bolte kya hain ?
---------------------
- "frozen=True" aur "order=True" — @dataclass ke options/parameters.

- field()                        — dataclasses module ka function, 
                                   jisse field ki settings define 
                                   hoti hain.