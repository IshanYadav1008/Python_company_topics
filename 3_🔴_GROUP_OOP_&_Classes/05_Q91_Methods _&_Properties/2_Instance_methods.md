1. Sabse pehle "Instance" kya hota hai?

* Instance = Class se bana hua object.

Example:
--------
class Student:
    pass

* Yahan Student ek class hai.

Ab:
---
s1 = Student()
s2 = Student()

Yahan:
------
Student → Class

s1 → Instance/Object
s2 → Instance/Object

* Matlab s1 aur s2 dono Student class ke instances hain.

=================================================================================

2. Method kya hota hai?

* Humne pehle padha tha: Class ke andar bana hua "function = Method".

Example:
--------
class Student:

    def study(self):
        print("Student is studying")

* study() yahan ek method hai.

Ab agar:
--------
s1 = Student()  // toh hum method ko call kar sakte hain:
s1.study()

Output:
-------
Student is studying

=================================================================================

3. Toh Instance Method kya hai?

* Ab naam ko todte hain: Instance + Method

Matlab: Aisa method jo kisi particular instance/object ke 
        saath kaam karta hai = Instance Method.

Example:
--------
class Student:

    def study(self):
        print("Student is studying")

* study() ek instance method hai.

* Kyun? Kyunki ise hum object ke through call kar rahe hain:

=> s1.study()

=================================================================================

4. self sabse important hai

* Instance methods mein tumhe mostly ye dikhega:

=> def study(self):  // Yahan self kya hai?

* Simple answer: self current object ko represent karta hai.

Example:
--------
class Student:

    def introduce(self):
        print("I am a student")

Ab:
---
s1 = Student()
s1.introduce()

* Yahan self → s1 ko refer karega.

<--------------------------------------------------------->

Agar:
-----
s2 = Student()
s2.introduce()

toh:
----
self → s2

=================================================================================

5. Ek diagram se samjho:

              Student Class
                   │
          ┌────────┴────────┐
          ↓                 ↓
         s1                s2
       Object            Object
          │                 │
          ↓                 ↓
   introduce(self)    introduce(self)
          │                 │
     self = s1          self = s2

* Isliye self ka matlab "current object" hai.

=================================================================================

6. Instance Method ka real use tab samajh aayega jab object ka data use karein:

Ab ek proper example:
---------------------
class Student:

    def __init__(self, name):
        self.name = name

    def introduce(self):
        print("My name is", self.name)

Object:
-------
s1 = Student("Rahul")

Ab:
---
s1.introduce()

Output:
-------
My name is Rahul

<------------------------------------------------------->

# Yahan kya hua?

Step 1
------
s1 = Student("Rahul")   // s1 bana aur:
self.name = "Rahul"     // ho gaya.

<------------------------------------------------------->

Step 2
------
s1.introduce()

* Python ko current object s1 mila.

* Isliye method ke andar: self ka matlab s1 hai.

Aur:
----
self.name    // ka matlab: s1.name

To output:
----------
My name is Rahul

=================================================================================

7. self.name ka matlab kya hai?

**Ye bahut important hai.**

# self.name

ko todho:
---------
self
 ↓
current object

name
 ↓
us object ka attribute

Toh:
----
self.name   // = current object ka name

<---------------------------------------------->

* Agar current object s1 hai:

=> self.name   // means: s1.name

* Agar current object s2 hai:

=> self.name   // means: s2.name

=================================================================================

8. Ab do objects ka example:

CODE:
-----
class Student:

    def __init__(self, name):
        self.name = name

    def introduce(self):
        print("My name is", self.name)

Ab:
---
s1 = Student("Rahul")
s2 = Student("Aman")

* Dono ke paas apna name hai:

s1.name → Rahul
s2.name → Aman

Ab:
---
s1.introduce()

Output:
-------
My name is Rahul

<-------------------------------------------->

# Aur:

s2.introduce()

Output:
-------
My name is Aman

<-------------------------------------------->

* Same method, lekin different result.

--> Kyun ? Kyuki self current object ke according 
           change hota hai.

=================================================================================

9. Isko ek real-life example se samjho

* Socho ek school mein 2 students hain:

Rahul
Aman

* Dono ke paas same ability hai:

study()
introduce()
play()

<--------------------------------------------------->

* Lekin jab Rahul introduce() karega:

My name is Rahul

* Aman karega:

My name is Aman

<--------------------------------------------------->

Method same hai:

=> introduce()

* Lekin object alag hai.

* Isi wajah se ise Instance Method kehte hain.

=================================================================================

10. Instance Method ka basic structure

Generally:
----------
class ClassName:

    def method_name(self):
        # code

Example:
--------
class Car:

    def start(self):
        print("Car started")

Object:
-------
car1 = Car()

Method call:
------------
car1.start()

=================================================================================

11. Instance Method arguments bhi le sakta hai

Example:
--------
class Student:

    def greet(self, person):
        print("Hello", person)

Ab:
---
s1 = Student()
s1.greet("Rahul")

Output:
-------
Hello Rahul

<-------------------------------------------->

* Yahan : self, current object hai.

* Aur   : person, normal argument hai.

=================================================================================

12. self ko manually pass karna padta hai ?? Normally nahi.

Tum likhte ho:
--------------
=> s1.introduce()

Python internally roughly:
--------------------------
=> Student.introduce(s1)    // jaisa treat karta hai.

Isliye:
-------
=> def introduce(self):  // mein self automatically current object 
                            ko receive karta hai.

Important
---------
Tum normally ye nahi likhte:

❌ s1.introduce(s1)

Bas:
----
✅ s1.introduce()

=================================================================================

13. Instance Method vs Normal Function

Normal Function
---------------
def add(a, b):
    return a + b

* Ye class ke bahar hai.

<------------------------------------------------>

Instance Method
---------------
class Calculator:

    def add(self, a, b):
        return a + b

* Ye class ke andar hai aur self ke through object 
  se connected hai.

Use:
----
c1 = Calculator()
print(c1.add(10, 20))

Output:
-------
30

=================================================================================

14. Instance Method ka main purpose kya hai?

* Instance method ka main purpose hai: Object ke data ke saath kaam karna.

Example:
--------
class BankAccount:

    def __init__(self, balance):
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

Ab:
---
account = BankAccount(1000)
account.deposit(500)
print(account.balance)

Output:
-------
1500

* Yahan deposit() instance method hai.

* Kyunki ye current object's: self.balance, ko modify kar raha hai.

=================================================================================

15. Instance Method ka deeper meaning

Technically, jab tum likhte ho:
-------------------------------
=> account.deposit(500)

* Python method ko current object ke context ke saath bind karta hai.

Conceptually:
-------------
account.deposit(500)

roughly:
--------
BankAccount.deposit(account, 500)

<---------------------------------------------------->

So:
---
account
   ↓
self

<---------------------------------------------------->

Aur:
----
500
   ↓
amount

<---------------------------------------------------->

* Isliye method ke andar:

=> self.balance  // se hum current account ka balance 
                    access kar paate hain.

=================================================================================

16. Instance Method ki 3 main characteristics:

① Class ke andar hota hai
--------------------------
class Student:

    def study(self):
        ...

② First parameter generally self hota hai:
-------------------------------------------
def study(self):

③ Object ke through call hota hai:
----------------------------------
s1.study()

* Aur ye object ke instance data ke saath kaam kar sakta hai:

self.name
self.age
self.balance

=================================================================================

17. Attribute + Instance Method together

Ab sab concepts ko connect karo:
--------------------------------
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def introduce(self):
        print("My name is", self.name)

    def study(self):
        print(self.name, "is studying")

Yahan:
------
Student
│
├── name       → Instance Attribute
├── age        → Instance Attribute
│
├── introduce() → Instance Method
└── study()     → Instance Method

Object:
-------
s1 = Student("Rahul", 20)

Ab:
---
s1.introduce()  → Rahul

Aur:
----
s1.study()      → Rahul is studying

=================================================================================

18. Ek line mein Instance Method
--------------------------------

Instance Method = Class ke andar bana hua method jo particular object/instance
                  ke saath kaam karta hai aur generally self ke through us 
                  object ka data access karta hai.

=================================================================================

🧠 Abhi ke liye ye 5 cheezein pakki kar lo:

Class
 ↓
Object/Instance
 ↓
Instance Method
 ↓
self
 ↓
self.attribute

Example:
--------
class Student:

    def __init__(self, name):
        self.name = name

    def introduce(self):
        print(self.name)

Yahan:
------
Student            → Class
s1                 → Instance/Object
name               → Instance Attribute
introduce()        → Instance Method
self               → Current Object
self.name          → Current Object ka name