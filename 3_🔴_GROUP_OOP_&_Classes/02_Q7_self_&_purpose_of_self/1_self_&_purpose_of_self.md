# self kya hota hai?

* Sabse simple definition: self current object ko refer karta hai.

--> Yaani jis object ke through method call hua hai, self usi object 
    ko represent karta hai.

================================================================================

Q) self actually kya hai?

ANS) self current object ka reference hota hai.

Matlab self ke andar current object ka reference hota hai, 
jisse Python ko pata chalta hai ki method ke andar kis 
object par kaam karna hai.

================================================================================

CODE:
-----
class Student:
    def set_name(self, name):
        self.name = name

student1 = Student()
student1.set_name("Rahul")

Yahan:
------
self → student1 ka reference

Isliye:
-------
self.name = name

effectively:
------------
student1.name = "Rahul"

<---------------------------------------------------->

Notes ke liye:
--------------
* self is a reference to the current object.

Q) Aur agar koi pooche “self kya hai?”, seedha bolo:

ANS) “Self current object ko refer karne wala reference hai.”

* self keyword technically nahi hai; ye ek conventional 
  parameter name hai. Python mein first parameter ko 
  self naam dena convention hai.

================================================================================

1. Pehle simple example
-----------------------
class Student:

    def show(self):
        print("Hello")

Ab object banaya:
-----------------
student1 = Student()

Aur method call ki:
-------------------
student1.show()

<-------------------------------------------------------------->

* Yahan Python internally show() ko roughly aise treat karta hai:

Student.show(student1)

Isliye:
-------
def show(self):  // mein self ke andar student1 aa gaya.

So:
---
self → student1

================================================================================

2. Dusra object banate hain:

student2 = Student()
student2.show()

Ab internally roughly:
----------------------
Student.show(student2)

Toh:
----
self → student2

<-------------------------------------------------------------->

Iska matlab:
------------
student1.show()
      ↓
self = student1

<-------------------------------------------------------------->

student2.show()
      ↓
self = student2

* Isi ko self ka core concept samjho.

================================================================================

3. self ka purpose kya hai?

* self ka main purpose hai: self current object ko refer karta hai, jiske 
                            through hum us object ke attributes ko access 
                            aur class ke methods ko call karte hain.

Example:
--------
class Student:

    def set_name(self, name):
        self.name = name

Ab:
---
student1 = Student()
student1.set_name("Rahul")

Yahan:
------
self → student1
name → "Rahul"

<-------------------------------------------------------------->

Isliye:
-------
self.name = name

actually:
---------
student1.name = "Rahul"  // ho gaya.

================================================================================

4. Ye aur clearly dekho

CODE:
-----
class Student:

    def set_name(self, name):
        self.name = name

student1 = Student()
student2 = Student()

student1.set_name("Rahul")
student2.set_name("Aman")

<-------------------------------------------------------------->

Ab objects ke andar:
--------------------
student1
   ↓
name = "Rahul"


student2
   ↓
name = "Aman"

* Same class hai, same method hai, lekin self ki wajah se har 
  object ka apna data maintain hota hai.

================================================================================

5. self.name kyun likhte hain?

**Ye bahut important hai.**

def set_name(self, name):
    self.name = name

<-------------------------------------------------------------->

Yahan do name hain:
-------------------
* Right side name

self.name = name
             ↑
Ye function ka parameter hai.

<-------------------------------------------------------------->

* Left side self.name

self.name
    ↑
Ye object ka variable/attribute hai.

<-------------------------------------------------------------->

So:
---
self.name = name    // ka simple meaning: "Jo name mujhe mila hai, 
                                           usko current object ke 
                                           name mein store kar do."

================================================================================

6. Real-life analogy

* Socho ek school mein 2 students hain:

Rahul
Aman

Dono ke paas apna-apna:
-----------------------
name
age
marks   // hai.

<-------------------------------------------------------------->

Class:
------
class Student:  // ye batati hai ki student ke paas kya data 
                   hoga.

Objects:
--------
student1
student2       // actual students hain.

<-------------------------------------------------------------->

Ab:
---
self.name

ka matlab: "Jis student ki baat abhi ho rahi hai, uska name."

Agar:
-----
student1.set_name("Rahul")

--> toh self = student1.

Agar:
-----
student2.set_name("Aman")

-> toh self = student2.

================================================================================

7. self automatically aata hai?

* Haan, method call karte waqt Python current object ko automatically 
  first argument ke roop mein pass karta hai.

Tum likhte ho:
--------------
student1.show()

Python roughly samajhta hai:
----------------------------
Student.show(student1)

Isliye method mein:
-------------------
def show(self):     // self ke andar student1 aa jata hai.

Tum normally manually nahi likhte:
----------------------------------
student1.show(student1)  # ❌

================================================================================

8. self ka naam self hi hona zaroori hai ?? Technically nahi.

* Python mein first parameter ka naam kuch bhi ho sakta hai:

class Student:

    def show(x):
        print(x)

Ye technically work karega:
---------------------------
student1 = Student()
student1.show()

* Lekin convention hai ki hum self hi use karte hain.

Isliye hamesha:
---------------
def show(self):   // likhna best practice hai.

================================================================================

9. self sirf variables ke liye nahi hai

* “self ke through hum class mein defined methods ko current object 
   ke context mein call kar sakte hain.”

* Yahan “context” ka matlab hai: method ko ye pata hota hai ki 
  kaunse object ke liye kaam karna hai.

Example:
--------
=> student1.study()

* Yahan study() method ka context = student1 hai, 
  isliye self → student1 hota hai.

=> student2.study()

* Yahan context = student2, isliye self → student2 
  hota hai.

** Bas simple mein: context = “kis object ke liye method 
                               abhi kaam kar raha hai.”

--------------------------------------------------------------------------------

CODE:
-----
class Student:

    def study(self):
        print("Student is studying")

    def exam(self):
        self.study()
        print("Student is giving exam")

Ab:
---
student1 = Student()
student1.exam()

Output:
-------
Student is studying
Student is giving exam

Yahan:
------
self.study()

* ka matlab hai: Current object ka study() method call karo.

================================================================================

10. Sabse important example

* Is code ko dhyan se dekho:


CODE:
-----
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def introduce(self):
        print("My name is", self.name)
        print("My age is", self.age)


student1 = Student("Rahul", 20)
student2 = Student("Aman", 21)

student1.introduce()
student2.introduce()

<----------------------------------------------------->

Jab:
----
=> student1.introduce()   // call hota hai:

self → student1

toh:
----
self.name

means:
------
student1.name

Output:
-------
My name is Rahul
My age is 20

<----------------------------------------------------->

Aur jab:
--------
=> student2.introduce()   // call hota hai:

self → student2

toh:
----
self.name

means:
------
student2.name

Output:
-------
My name is Aman
My age is 21

================================================================================

🔥 self ka actual purpose
--------------------------

Q) Agar exam/interview mein pooche: "What is the purpose of self 
   in Python?"

Toh simple answer:
------------------
self current object ka reference hota hai, jiske through hum us 
object ke attributes ko access aur class mein defined methods ko 
current object ke context mein call karte hain.

--------------------------------------------------------------------------------

Ek line mein yaad rakho:
------------------------
self = "jis object ke liye abhi kaam ho raha hai"

Example:
--------
student1.show()  → self = student1
student2.show()  → self = student2