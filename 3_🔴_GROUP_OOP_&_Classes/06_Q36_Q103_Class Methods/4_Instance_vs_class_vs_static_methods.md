# Instance Method vs Class Method vs Static Method

Sabse pehle ek line ka rule yaad rakho:
---------------------------------------
Instance Method → object ke liye
Class Method    → class ke liye
Static Method   → na object, na class — normal utility/function

Aur unke first parameters:
--------------------------
Instance Method → self
Class Method    → cls
Static Method   → koi automatic self/cls nahi

===============================================================================

1. Instance Method

* Ye hum already padh chuke hain.

* Instance method ka connection particular object se hota hai.

CODE:
-----
class Student:

    def __init__(self, name):
        self.name = name

    def show_name(self):
        print(self.name)

Ab objects:
-----------
s1 = Student("Rahul")
s2 = Student("Aman")

s1.show_name()
s2.show_name()

Output:
-------
Rahul
Aman

<------------------------------------------------------>

Yahan kya hua?
--------------
s1.show_name()

Python internally roughly:
--------------------------
Student.show_name(s1)

So:
---
self = s1

<------------------------------------------------------>

Aur:
----
s2.show_name()

roughly:
--------
Student.show_name(s2)

So:
---
self = s2

<------------------------------------------------------>

Isliye:
-------
self.name

* ka matlab hai: jis object ne method call kiya, us 
                 object ka name

===============================================================================

2. Class Method

* Class method ka connection class se hota hai.

Isme @classmethod lagate hain.
------------------------------
class Student:

    school = "ABC School"

    @classmethod
    def show_school(cls):
        print(cls.school)

Call:
-----
Student.show_school()

Output:
-------
ABC School

<------------------------------------------------------>

Yahan:
------
cls = Student

Conceptually:
-------------
Student.show_school()

roughly:
--------
Student.show_school(Student)

So:
---
cls → Student class

<------------------------------------------------------>

# Instance method vs class method

Instance Method
      ↓
    self
      ↓
 particular object

Class Method
      ↓
     cls
      ↓
     class

===============================================================================

3. Static Method

# Ab third type.

Static method ko: "@staticmethod", se banate hain.

Example:
--------
class Student:

    @staticmethod
    def add(a, b):
        return a + b

Call:
-----
print(Student.add(10, 20))

Output:
-------
30

<------------------------------------------------------>

Notice karo:
------------
def add(a, b):

isme:
-----
self ❌
cls  ❌

* kuch bhi automatically nahi aata.

Sirf:
-----
a
b

* normal parameters hain.

===============================================================================

# Static Method ko simple language mein samjho

Maan lo class hai:
------------------
class Student:

* Aur usme ek calculation hai:

@staticmethod
def add(a, b):
    return a + b

* Kya add() ko kisi particular student ki information chahiye ? Nahi.

* Kya add() ko Student class ki information chahiye ? Nahi.

Bas do numbers chahiye:
-----------------------
10
20

--> Isliye static method suitable hai.

-------------------------------------------------------------------------------

Ab teenon ko ek hi class mein dekho:
------------------------------------
class Student:

    school = "ABC School"

    def __init__(self, name):
        self.name = name

    # Instance Method
    def show_name(self):
        print(self.name)

    # Class Method
    @classmethod
    def show_school(cls):
        print(cls.school)

    # Static Method
    @staticmethod
    def add(a, b):
        return a + b

Ab:
---
s1 = Student("Rahul")

Instance Method
---------------
s1.show_name()

Output:
-------
Rahul    // Kyunki method ko s1 object chahiye.

show_name()
    ↓
self = s1
    ↓
self.name
    ↓
Rahul

-------------------------------------------------------------------------------

Class Method
------------
Student.show_school()

Output:
-------
ABC School

* Kyunki method ko Student class chahiye.

show_school()
      ↓
   cls = Student
      ↓
   cls.school
      ↓
  ABC School

-------------------------------------------------------------------------------

Static Method
-------------
Student.add(10, 20)

Output:
-------
30

Kyunki isko:
------------
object ki zarurat nahi
class ki zarurat nahi

Bas:
----
a = 10
b = 20  // chahiye.

===============================================================================

# Sabse important comparison

| Method          | Decorator       | First automatic parameter | Kis se related? |
| --------------- | --------------- | ------------------------- | --------------- |
| Instance Method | None            | `self`                    | Object          |
| Class Method    | `@classmethod`  | `cls`                     | Class           |
| Static Method   | `@staticmethod` | Nothing                   | Neither         |


Yaad rakho:
-----------
INSTANCE → self    → OBJECT
CLASS    → cls     → CLASS
STATIC   → nothing → INDEPENDENT

===============================================================================

# Ek real-life example

Maan lo:
--------
class Student:

    school = "ABC School"

    def __init__(self, name):
        self.name = name

    def introduce(self):
        print("My name is", self.name)

    @classmethod
    def show_school(cls):
        print("School:", cls.school)

    @staticmethod
    def add_marks(a, b):
        return a + b

<---------------------------------------------------->

introduce()
-----------
s1 = Student("Rahul")
s1.introduce()

Output:
-------
My name is Rahul

* Ye instance method hai because Rahul wale specific 
  object ki information chahiye.

-------------------------------------------------------------------------------

show_school()
-------------
Student.show_school()

Output:
-------
School: ABC School

* Ye class method hai because school class-level information hai.

-------------------------------------------------------------------------------

add_marks()
-----------
Student.add_marks(80, 90)

Output:
170

* Ye static method hai because calculation ke liye na s1 chahiye, 
  na Student ki information.

===============================================================================

# Ek bahut important difference

Suppose:
--------
class Student:

    def show_name(self):
        print(self.name)

Yahan:
------
self.name   // hai, Matlab method ko object ka data chahiye.

-------------------------------------------------------------------------------

Class method:
-------------
@classmethod
def show_school(cls):
    print(cls.school)

Yahan:
------
cls.school  // hai, Matlab method ko class ka data chahiye.

-------------------------------------------------------------------------------

Static:
-------
@staticmethod
def add(a, b):
    return a + b

Yahan:
------
self ❌
cls ❌

* Matlab method ko object/class ka data nahi chahiye.

===============================================================================

Ek simple decision trick 🧠
---------------------------

* Jab method bana rahe ho, khud se ye question pucho:

Question 1: 
-----------
Kya mujhe particular object ka data chahiye?

Example:
--------
self.name
self.age

→ Instance Method

-------------------------------------------------------------------------------

Question 2:
-----------
Kya mujhe class-level data chahiye?

Example:
--------
cls.school
cls.count

→ Class Method

-------------------------------------------------------------------------------

Question 3:
-----------
Kya mujhe object ya class dono mein se kisi ki information nahi chahiye?

Example:
--------
add(a, b)

→ Static Method

===============================================================================

Final mental picture:
---------------------

                 METHODS
                    │
        ┌───────────┼───────────┐
        ↓           ↓           ↓
    INSTANCE      CLASS       STATIC
        │           │           │
      self         cls        nothing
        │           │           │
     Object       Class      Independent
        │           │           │
 self.name      cls.school    add(a,b)

Ek line mein:
-------------
Instance method object ke saath kaam karta hai, class method class ke 
saath kaam karta hai, aur static method sirf logically class ke andar 
rakhi hui normal utility function hoti hai.