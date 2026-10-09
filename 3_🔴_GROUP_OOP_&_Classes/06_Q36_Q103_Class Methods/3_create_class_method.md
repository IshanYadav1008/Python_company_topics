1. Sabse basic class method:

CODE:
-----
class Student:

    @classmethod
    def show_school(cls):
        print("ABC School")

Yahan 3 important cheezein hain:
--------------------------------
@classmethod
def show_school(cls):
@classmethod

* Python ko bolta hai: Ye normal instance method nahi, 
                       class method hai.

cls
---
cls current class ko represent karta hai.

show_school
------------
Class method ka naam.

==============================================================================

2. Class method ko call kaise karte hain?

Class ke naam se:
-----------------
Student.show_school()

Output:
-------
ABC School

Flow:
-----
Student.show_school()
        ↓
   class method
        ↓
   cls = Student

==============================================================================

3. cls ka actual use

* Ab thoda useful example:

CODE:
-----
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

--> Yahan: cls.school, ka matlab : Current class ka school attribute.
--> Aur current class hai        : Student

Toh conceptually:
-----------------
cls.school
   ↓
Student.school
   ↓
"ABC School"

==============================================================================

4. Class method se class ki value change bhi kar sakte hain

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

<------------------------------------------------->

Yahan:
------
Student.change_school("XYZ School")

ke time:
--------
cls        = Student
new_school = "XYZ School"

Phir:
-----
cls.school = new_school

actually:
---------
Student.school = "XYZ School"  // jaisa kaam karta hai.

==============================================================================

5. Isko Instance Method se compare karo:

Instance Method
---------------
class Student:

    def show_name(self):
        print(self.name)

Call:
-----
s1.show_name()

Yahan: s1 → self, Matlab specific object.

------------------------------------------------------------------------------

Class Method
------------
class Student:

    school = "ABC"

    @classmethod
    def show_school(cls):
        print(cls.school)

Call:
-----
Student.show_school()

Yahan: Student → cls, Matlab class.

==============================================================================

6. Class method mein parameter bhi ho sakta hai

Bilkul.

Jaise:
------
class Student:

    school = "ABC School"

    @classmethod
    def change_school(cls, new_school):
        cls.school = new_school

Yahan:
------
--> cls

aur

--> new_school

* do alag cheezein hain:

<----------------------------------------------->

cls
 ↓
current class

<----------------------------------------------->

new_school
 ↓
method ko di gayi value

<----------------------------------------------->

Call:
-----
Student.change_school("XYZ School")

toh:
----
cls        = Student
new_school = "XYZ School"

==============================================================================

7. self aur cls ko ek baar aur crystal clear karo

Ye yaad rakhna:

INSTANCE METHOD
---------------
def show(self):
       ↑
       object


CLASS METHOD
------------
@classmethod
def show(cls):
       ↑
       class

<---------------------------------------------------->

Example:
--------
s1 = Student()
s2 = Student()

Instance method mein:
---------------------
s1.show()
   ↓
self = s1

s2.show()
   ↓
self = s2

<---------------------------------------------------->

Class method mein:
------------------
Student.show()

    Student
       ↓
      cls

* Dono objects ke through bhi call karo:

s1.show()
s2.show()

* class method hone ki wajah se cls phir 
  bhi Student class ko refer karega.

==============================================================================

8. Class method kab banate hain?

* Jab method ka kaam individual object ka nahi, class-level 
  data/behavior ka ho.

Example:
--------
class Student:

    school = "ABC School"

    @classmethod
    def change_school(cls, name):
        cls.school = name

change_school() ko ye nahi jaana:
---------------------------------
Rahul ka naam kya hai?
Aman ki age kya hai?

Usko sirf ye karna hai:
-----------------------
Student class ka school change karo

Isliye:
-------
@classmethod

==============================================================================

Ekdum short notes:
-----------------
@classmethod
      ↓
Method ko class method banata hai

     cls
      ↓
Current class ko refer karta hai

Class method
      ↓
Class-level data/behavior ke liye

------------------------------------------------------------------------------

Example:
--------
class Student:

    school = "ABC School"

    @classmethod
    def change_school(cls, name):
        cls.school = name


print(Student.school)
Student.change_school("XYZ School")
print(Student.school)

<---------------------------------------------->

Output:
-------
ABC School
XYZ School

Yaad rakhne ka formula:
-----------------------
self → object
cls  → class

* @classmethod → method ko class ke saath bind karo