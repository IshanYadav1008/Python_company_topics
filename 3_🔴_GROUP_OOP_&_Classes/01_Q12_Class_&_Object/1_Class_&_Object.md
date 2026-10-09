1. OOPs hota kya hai?

OOP = Object-Oriented Programming

Simple language mein:
---------------------
Program ko objects ke form mein organize karna OOP hai.

Real life mein humare paas objects hote hain:
---------------------------------------------
Car
Student
Mobile
Bank Account
Employee

-------------------------------------------------------------------------------

* Har object ke paas generally do cheezein hoti hain:

Data/Properties
---------------
* Object ke baare mein information.

Example: Student
----------------
name   = "Rahul"
age    = 20
course = "Python"

<---------------------------------------------------->

Behaviour/Methods
-----------------
* Object kya kaam kar sakta hai.

study()
sleep()
attend_class()

* Python mein hum class ke through ye structure banate
  hain.

===============================================================================

2. Class kya hoti hai?

Class ko simple words mein:
---------------------------
Class ek "blueprint/design/template" hoti hai jiske basis par 
objects banaye jaate hain.

Real-life example:
------------------
* Socho tumhare paas house ka blueprint hai.

--> Blueprint khud ghar nahi hai.

Blueprint bas batata hai:
-------------------------
2 rooms
1 kitchen
1 bathroom

* Us blueprint ke basis par actual houses ban sakte hain.

-------------------------------------------------------------------------------

Similarly:
----------
Class  = Blueprint
Object = Actual thing

Example
-------
class Student:
    pass

* Yahan Student ek class hai, Abhi class ke andar kuch nahi hai, 
  isliye pass likha hai.

===============================================================================

3. Object kya hota hai?

* Object class ka actual instance hota hai.

  Matlab class ek design hai aur object us 
  design se bani actual entity hai.

Example:
--------
class Student:
    pass

Ab Student class se objects banate hain:
----------------------------------------
student1 = Student()
student2 = Student()
student3 = Student()

Yahan:
------
Student   → Class

student1  → Object
student2  → Object
student3  → Object

* Teeno objects same class se bane hain.

===============================================================================

4. Ek real-life example

* Maan lo humare paas ek class hai:

class Car:
    pass

--> Car ek blueprint hai.

<------------------------------------------->

* Ab hum cars create karte hain:

car1 = Car()
car2 = Car()
car3 = Car()

Ab:
---
Car
│
├── car1
├── car2
└── car3

* Car              → class
* car1, car2, car3 → objects

===============================================================================

5. Class ke andar data kaise rakhen?

* Ab maan lo hume har student ka:

. name
. age
. course     // store karna hai.

-------------------------------------------------------------------------------

* Hum __init__() ka use karenge.

CODE:
-----
class Student:

    def __init__(self, name, age, course):
        self.name   = name
        self.age    = age
        self.course = course

Ab object banate hain:
----------------------
student1 = Student("Rahul", 20, "Python")
student2 = Student("Aman", 21, "Java")

Ab:
---
print(student1.name)
print(student1.age)
print(student1.course)

Output:
-------
Rahul
20
Python

<--------------------------------------------->

Aur:
----
print(student2.name)
print(student2.age)
print(student2.course)

Output:
-------
Aman
21
Java

===============================================================================

6. Yahan actually hua kya?

**Ye part bahut important hai.**

Jab humne likha:
----------------
student1 = Student("Rahul", 20, "Python")  // Python ne Student class ka 
                                              ek object create kiya.

Aur ye values:
--------------
Rahul
20
Python

--> us object ke andar store ho gayi.

-------------------------------------------------------------------------------

Conceptually:
-------------
student1
   │
   ├── name   → "Rahul"
   ├── age    → 20
   └── course → "Python"

Aur:
----

student2
   │
   ├── name   → "Aman"
   ├── age    → 21
   └── course → "Java"

* Dono objects same class se bane hain, lekin dono ke data alag hain.

===============================================================================

7. self kya hai?

* Ye OOPs ka bahut important concept hai.

Abhi bas itna samjho:
---------------------
self current object ko represent karta hai.

Example:
--------
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

Jab:
----
student1 = Student("Rahul", 20)

toh roughly:
------------
self = student1

Isliye:
-------
self.name  // ka matlab hua: student1 ka name

<------------------------------------------------------>

Aur jab:
--------
student2 = Student("Aman", 21)

toh:
----
self = student2

Isliye:
-------
self.name // ab student2 ka name refer karega.

===============================================================================

8. self.name aur name mein difference

**Ye bahut important hai.**

class Student:

    def __init__(self, name):
        self.name = name

Right side:
-----------
name       → jo value function ko mili.

Left side:
----------
self.name  → object ke andar banaya gaya variable.

-------------------------------------------------------------------------------

Example:
--------
student1 = Student("Rahul")

Toh:
----
name       → "Rahul"
self.name  → student1.name

Matlab:
-------
self.name = name   // essentially object ke andar value store kar raha hai.

===============================================================================

9. Class mein methods bhi bana sakte hain

* Abhi humne sirf data store kiya.

* Lekin object ka behaviour bhi define kar sakte hain.

CODE:
-----
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def study(self):
        print(self.name, "is studying")

Object:
-------
student1 = Student("Rahul", 20)

-------------------------------------------------------------------------------

Method call:
------------
student1.study()

Output:
-------
Rahul is studying

<------------------------------------------->

Another object:
---------------
student2 = Student("Aman", 21)
student2.study()

Output:
-------
Aman is studying

Notice karo:
------------
same method, lekin different object ke according different output.

===============================================================================

10. Class + Object ka complete picture

CODE:
-----
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def study(self):
        print(self.name, "is studying")


student1 = Student("Rahul", 20)
student2 = Student("Aman", 21)

student1.study()
student2.study()

-------------------------------------------------------------------------------

Isko mentally aise dekho:

              CLASS
             Student
                │
       ┌────────┴────────┐
       ↓                 ↓
    OBJECT 1          OBJECT 2
    student1          student2
       │                 │
 name = Rahul        name = Aman
 age = 20            age = 21
       │                 │
       ↓                 ↓
   study()            study()

===============================================================================

11. Ek line mein yaad rakho

Class : "Object kaisa hoga, iska blueprint."
Object: "Class se bana hua actual instance."

Example:
--------
class Dog:
    pass

Dog → Class

dog1 = Dog()
dog2 = Dog()

--> dog1, dog2 → Objects

===============================================================================

12. Ek bahut important analogy

Restaurant ka example lo 🍽️
---------------------------
Recipe        → Class
Actual dish   → Object

Recipe mein likha hai:
----------------------
Pizza:
- cheese
- sauce
- toppings  // Ye class/blueprint jaisa hai.

<----------------------------------------------->

Ab recipe ke basis par:
-----------------------
Pizza 1
Pizza 2
Pizza 3   // ban sakti hain. Ye objects hain.

* Har pizza same recipe se bana hai, lekin toppings/dimensions 
  alag ho sakte hain.

===============================================================================

# Abhi ke liye bas ye 5 cheezein pakki karo:

OOP
 ↓
Class
 ↓
Object
 ↓
__init__
 ↓
self

<-------------------------------------------->

Aur basic syntax:
-----------------
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def study(self):
        print(self.name, "is studying")


student1 = Student("Rahul", 20)
student1.study()