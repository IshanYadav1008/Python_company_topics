5. self kya hota hai?
---------------------

Ye sabse important point hai.

* self Python ka built-in keyword nahi hai.

* self ek normal parameter name hai jo Python programmers 
  convention ke taur par use karte hain.

* Lekin us parameter mein Python automatically current object 
  pass karta hai.

Example:
--------
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

Jab:
----
student1 = Student("Rahul", 20) // hota hai.

Toh conceptually:
-----------------
Student.__init__(student1, "Rahul", 20)   // jaisa samajh sakte ho.

Isliye:
-------
self → student1
name → "Rahul"
age  → 20

===============================================================================

6. self.name = name ko properly samjho
--------------------------------------

* Ye line beginners ko sabse zyada confuse karti hai:

=> self.name = name

Isko do parts mein tod do:
--------------------------

=> Left side  : self.name
. Matlab: Current object ka name attribute.

=> Right side : name
. Matlab: Function mein aayi hui name ki value.

So:
---
=> self.name = name

* ka simple Hindi meaning: Current object ke name attribute 
                           mein name parameter ki value daal do.
 
Same:
-----
=> self.age = age

means: Current object ke age attribute mein age parameter ki 
       value daal do.

===============================================================================

# Complete example WITH __init__()

class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def introduce(self):
        print("My name is", self.name)
        print("My age is", self.age)


student1 = Student("Rahul", 20)
student2 = Student("Aman", 22)

student1.introduce()
student2.introduce()

Output:
-------
My name is Rahul
My age is 20

My name is Aman
My age is 22

-------------------------------------------------------------------------------

Isme kya hua?
-------------

Jab:
----
=> student1 = Student("Rahul", 20)

toh:
----
self → student1
name → Rahul
age  → 20

Aur:
----
self.name = name
self.age = age

se:
---
student1
   |
   ├── name = "Rahul"
   └── age  = 20

ban gaya.

<------------------------------------------------------->

Phir:
-----
=> student2 = Student("Aman", 22)

ke time:
--------
self → student2
name → Aman
age  → 22

Toh:
----
student2
   |
   ├── name = "Aman"
   └── age  = 22

* Dono objects alag hain aur unka data bhi alag hai.

===============================================================================

8. Complete example WITHOUT __init__()
--------------------------------------

* Ab same kaam bina __init__() ke karte hain:

class Student:
    pass


student1 = Student()
student2 = Student()

student1.name = "Rahul"
student1.age = 20

student2.name = "Aman"
student2.age = 22

print(student1.name)
print(student1.age)

print(student2.name)
print(student2.age)

Output:
-------
Rahul
20
Aman
22

. Ye bhi perfectly possible hai.

<------------------------------------------------------->

Difference kya hua?
-------------------

Without __init__():

=> student1 = Student()

. object ban gaya, lekin uske andar automatically 
  name aur age nahi aaye.

Hume manually likhna pada:
--------------------------
=> student1.name = "Rahul"
=> student1.age  = 20

. Aur second object ke liye phir:

=> student2.name = "Aman"
=> student2.age  = 22

===============================================================================

9. WITH vs WITHOUT __init__()
-----------------------------

Without __init__():
-------------------
class Student:
    pass

student1 = Student()

student1.name = "Rahul"
student1.age = 20

* Tumhe manually data set karna padega.

<------------------------------------------------------->

With __init__():
----------------
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age


student1 = Student("Rahul", 20)

. Object banate hi initial data set ho gaya.

<------------------------------------------------------->

Isliye __init__() ka main benefit:
----------------------------------

1. Code clean hota hai
2. Repeated setup nahi karna padta
3. Har object ko required starting data diya ja sakta hai
4. Class ka structure clear hota hai

===============================================================================

10. Agar __init__() na ho toh kya object ban sakta hai?
-------------------------------------------------------

# Haan, bilkul.
---------------
class Student:
    pass

student1 = Student()   // Ye valid hai.

Lekin:
------
print(student1.name)   // karoge toh error aayega, kyunki name 
                          automatically bana hi nahi tha.

Tumhe pehle:
------------
=> student1.name = "Rahul"  // karna padega.

===============================================================================

11. Ek complete mental picture 🧠
---------------------------------

* Isko yaad rakhna:

                 CLASS
            ┌───────────────┐
            │    Student    │
            │               │
            │  __init__()   │
            │  introduce()  │
            └───────┬───────┘
                    │
             creates/initializes
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
      OBJECT 1             OBJECT 2
      student1              student2
          │                   │
     name = Rahul          name = Aman
     age  = 20             age  = 22

Ek line mein:
-------------
* Class      → design/blueprint
* Object     → class se bana actual instance
* __init__() → object ki initial state set karta hai
* self       → current object ko refer karta hai

===============================================================================

Final Question
--------------
Q) What is the purpose of the __init__ method in a Python class?

ANS:
----
__init__ method ka purpose Python class se banne wale naye object ki 
initial state ko initialize karna hota hai. Iske through hum object 
ke attributes ko starting values dete hain. Ye method object creation 
ke process ke dauran automatically call hota hai.

Example:
--------
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

* Yahan __init__() naye Student object ke name aur age ki initial values 
  set kar raha hai.