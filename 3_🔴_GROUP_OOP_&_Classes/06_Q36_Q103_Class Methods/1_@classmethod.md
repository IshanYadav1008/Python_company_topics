1. Sabse pehle: @classmethod hota kya hai?

* Python mein methods ke different types hote hain.

Abhi tak tumne Instance Method padha:
-------------------------------------
class Student:

    def show(self):
        print("Hello")

Isme:
-----
s1 = Student()
s1.show()

* show() object (s1) ke saath kaam karta hai.
* Isliye usme: self, aata hai.

--------------------------------------------------------------------------------

* Ab @classmethod mein method object ke saath nahi, class ke saath 
  associated hota hai.

Example:
--------
class Student:

    @classmethod
    def show(cls):
        print("Hello")

--> Yahan: cls, aata hai.

--------------------------------------------------------------------------------

Basic difference:
-----------------
Instance Method
      ↓
object ke saath kaam
      ↓
self

<----------------------------------------------->

Class Method
      ↓
class ke saath kaam
      ↓
cls

================================================================================

2. cls kya hai?

* Jaise : self, ka matlab hota hai : current object
* Waise : cls, ka matlab hota hai  : current class

Example:
--------
class Student:

    @classmethod
    def show(cls):
        print(cls)

Agar call karo:
---------------
Student.show()   // toh cls ke andar Student class aa jaati hai.

<--------------------------------------------------------------->

Conceptually:
-------------
Student.show()
       ↓
show(Student)
       ↓
cls = Student

* Yaani: cls, class ko refer karta hai.

================================================================================

3. Ek real simple example

Maan lo Student class hai:
--------------------------
class Student:

    school = "ABC School"

    @classmethod
    def show_school(cls):
        print(cls.school)

Ab:
---
Student.show_school()

Output:
-------
ABC School

Yahan:
------
cls.school

* ka matlab: jis class par class method call hua hai, 
             us class ka school attribute.

================================================================================

4. self vs cls

Ye difference bahut important hai.

Instance Method:
----------------
class Student:

    def show_name(self):
        print(self.name)

Agar:
-----
s1      = Student()
s1.name = "Rahul"
s1.show_name()

toh:
----
s1
 ↓
self

--> self = specific object

--------------------------------------------------------------------------------

Class Method:
-------------
class Student:

    school = "ABC School"

    @classmethod
    def show_school(cls):
        print(cls.school)

Call:
-----
Student.show_school()

toh:
----
Student
   ↓
 cls

--> cls = class

================================================================================

5. @classmethod kyun use karte hain?

Sabse common reason:
--------------------
Jab method ko individual object ki information ki zarurat na ho, 
balki class-level information ke saath kaam karna ho.

Example:
--------
class Student:

    school = "ABC School"

    @classmethod
    def change_school(cls, new_school):
        cls.school = new_school

Ab:
---
print(Student.school)
Student.change_school("XYZ School")
print(Student.school)

Output:
-------
ABC School
XYZ School

--------------------------------------------------------------------------------

* Yahan change_school() ko kisi specific student ki zarurat nahi hai.

* Usko sirf Student class ka school change karna hai.

Isliye:
-------
@classmethod  // use kiya.

================================================================================

6. self hota toh kya hota?

Instance method mein:
---------------------
def change_school(self, new_school):

* likh sakte ho, lekin logically galat design hoga agar kaam 
  class-level hai.

* Kyuki self kisi specific student ko represent karta hai:

s1 → self
s2 → self
s3 → self

* Lekin school sab students ke liye class-level hai:

--> Student → cls

Isliye:
-------
@classmethod
def change_school(cls, new_school):

// better hai.

================================================================================

7. Kya class method ko object se call kar sakte hain ? Haan.

Example:
--------
class Student:

    @classmethod
    def hello(cls):
        print("Hello")

Tum kar sakte ho:
-----------------
Student.hello()

Aur:
----
s1 = Student()
s1.hello()

* Dono possible hain.

* Lekin class method mein Python ko class hi milti hai as cls.

So:
---
Student.hello()
       ↓
cls = Student

Aur:
----
s1.hello()
   ↓
cls = Student

--> Yaani class method ka focus class hai, object nahi.

================================================================================

8. @classmethod mein decorator kyun lagate hain?

Ye:
---
@classmethod
def show(cls):

* Python ko batata hai: "Is method ko class method treat karo."

<--------------------------------------------------------------->

# Agar @classmethod hata do:

class Student:

    def show(cls):
        print(cls)

--> Toh ye normal instance method ban jayega.

--> Phir Python normally expect karega ki show() 
    ko object ke through call kiya jaye.

Isliye:
-------
@classmethod, important hai.

================================================================================

9. Ek important comparison

Abhi tak:

Instance Method
---------------
class Student:

    def show(self):
        print("Student")

object → self

Call:
-----
s1.show()

--------------------------------------------------------------------------------

Class Method
------------
class Student:

    @classmethod
    def show(cls):
        print("Student")

class → cls

Call:
-----
Student.show()

================================================================================

10. __init__ se iska kya relation hai?

* Tumne abhi __init__ padha hai, toh ye connection important hai.

* __init__ normally object ko initialize karta hai:

CODE:
-----
class Student:

    def __init__(self, name):
        self.name = name

Yahan:
------
Student("Rahul")
      ↓
object
      ↓
__init__
      ↓
self.name = "Rahul"

--> Ye instance level ka kaam hai.

--------------------------------------------------------------------------------

Class method:
-------------
class Student:

    school = "ABC"

    @classmethod
    def change_school(cls, name):
        cls.school = name

* Ye class level ka kaam hai.

So:
---
__init__
   ↓
object ki initial information

@classmethod
   ↓
class-level information/behavior

================================================================================

11. Ek real-life mental model

Socho:
------
Student = School ka system/template

s1 = Rahul
s2 = Aman
s3 = Priya

* Instance method: Sirf Rahul ka kaam // s1.study()

Yahan:
------
s1 → self

<------------------------------------------------------>

Class method
------------
Puri Student class ka kaam:

Student.change_school(...)

Yahan:
------
Student → cls

================================================================================

12. Sabse important yaad rakhne wali line

Instance Method → self → object ke saath kaam
Class Method    → cls → class ke saath kaam

Aur:

@classmethod
------------
Python ko batata hai: "Is method ko class ke saath bind karo."

================================================================================

Abhi ke liye tumhara mental map:
--------------------------------

CLASS
 │
 ├── Instance Method
 │      ↓
 │     self
 │      ↓
 │   specific object
 │
 └── Class Method
        ↓
       cls
        ↓
      class