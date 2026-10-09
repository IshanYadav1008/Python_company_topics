Q) __init__() kya hai?

ANS) 

__init__() Method

__init__() Python class ka ek special method hai jo object create 
           hone ke turant baad automatically call hota hai.

CODE:
-----
class Student:
    def __init__(self, name):
        self.name = name

Iska purpose kya hai?
---------------------
__init__() ka purpose: object create hone ke turant baad uske andar 
                       initialization wala code automatically execute 
                       karna.

=> student1 = Student("Rahul")

* Yahan object bante hi __init__() automatically chala, aur:

=> self.name = name

ne:
---

=> student1.name = "Rahul"  // set kar diya.

Short mein:
-----------
__init__() → object bante hi automatically chalne wala method.

Purpose    → object ko starting values/data dena.

=================================================================================

Purpose
-------
Iska purpose hai object create hone ke baad initialization wala code 
automatically execute karna.

Example:
--------
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

student1 = Student("Rahul", 20)

* Jab student1 create hota hai, Python automatically __init__() ko 
  call karta hai.

---------------------------------------------------------------------------------

__init__() ke andar:

self.name = name
self.age = age

* ye lines actual mein object ke attributes mein values set karti hain.

---------------------------------------------------------------------------------

Yahan:
------
self             → current object ko refer karta hai.
self.name = name → current object ke name attribute mein value set karta hai.
self.age = age   → current object ke age attribute mein value set karta hai.

__init__() → in lines ko object creation ke turant baad automatically execute 
             karwata hai.

Short Definition
----------------
__init__() = object create hone ke turant baad automatically call hone wala 
             special method, jiske andar initialization ka code likha jata 
             hai.

=================================================================================
---------------------------------------------------------------------------------
=================================================================================

__init__() kya hota hai ?
-------------------------

* __init__() Python class ka ek special method hai.

* Iska main purpose hai: Jab naya object initialize ho, 
                         uski starting state/data set karna.

Example:
--------
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

student1 = Student("Rahul", 20)

* Python object ko initialize karte waqt __init__() ko call karta hai.

Conceptually:
-------------
self → student1
name → "Rahul"
age  → 20

* "self.name = name" ka matlab: "student1.name = "Rahul"
* "self.age  = age"  ka matlab: "student1.age  = 20"

Final object:
-------------
student1
   |
   ├── name = "Rahul"
   └── age  = 20
-------------------------------------------------------------------------------

*** Important: ***
------------------

* __init__() ka kaam object banana nahi, balki newly created object 
  ko initialize/setup karna hai.

* Python mein technically object creation aur initialization alag 
  steps hain. Abhi beginner level par itna yaad rakhna enough hai:

* __init__() = new object ki starting values set karna.

===============================================================================

# __init__() ko ek "setup machine" samjho

Class:
------
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

Object:
-------
student1 = Student("Rahul", 20)


# Flow:

          Student(...)
               ↓
        ┌─────────────┐
        │ New Object  │
        └──────┬──────┘
               ↓
          __init__()
               ↓
      ┌─────────────────┐
      │ Initial Setup   │
      │                 │
      │ name = Rahul    │
      │ age  = 20       │
      └────────┬────────┘
               ↓
         Ready Object

===============================================================================

# Ab exact answer: __init__() kyun bana?

* Python ke designers ne object-oriented programming mein ye 
  common need dekhi:

"Jab object create ho, toh usko automatically initial values/setup 
 dene ka ek standard place hona chahiye."

Isliye classes mein special method:
-----------------------------------
__init__()   // provide kiya gaya.

* Tum class ke andar ise define karte ho:

class Student:

    def __init__(self, name, age):
        ...

. Aur object initialization ke process mein Python ise automatically 
  call karta hai.

===============================================================================

Ek line ka mantra:
------------------
__init__() object banane ka purpose nahi hai; object ko banne ke 
process mein "initial setup" dene ka standard method hai.