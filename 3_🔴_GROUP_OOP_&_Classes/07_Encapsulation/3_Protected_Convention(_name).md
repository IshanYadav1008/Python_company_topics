1. Protected Convention hota kya hai?

* Python mein kisi attribute ya method ke naam ke aage single 
  underscore _ lagane ko internal use ka signal maana jaata hai.

Example:
--------
self._age = age  // Yahan _age ek attribute hai.

Single underscore ka convention kehta hai:
------------------------------------------
Is attribute ko class ke internal use ke liye rakho. Bahar se ise 
directly access karne se bacho, jab tak zaroorat na ho.

Dhyan do: Python ise strictly protect nahi karta. Ye programmer 
          ko diya gaya ek signal hai.

===============================================================================

2. Public aur _protected mein kya difference hai?

* Pehle same example dono tarah se dekho.

Public
------
class Student:
    def __init__(self):
        self.age = 20
s = Student()
print(s.age)

# Allowed

* Normal public attribute.

<------------------------------------------------------->

Single underscore
-----------------
class Student:
    def __init__(self):
        self._age = 20
s = Student()
print(s._age)

# Still allowed

* Internal use ka signal.

-------------------------------------------------------------------------------

* Dono examples mein code chalega aur output 20 aayega.

Toh phir _age likhne ka fayda kya hai ?
---------------------------------------
Fayda ye hai ki doosre programmers ko pata chalta hai ki _age class 
ka internal detail hai, jise bina zarurat directly use ya modify 
nahi karna chahiye.

===============================================================================

3. Kya _age ko change kar sakte hain?

* Haan, Python mein kar sakte ho.

CODE:
-----
class Student:
    def __init__(self, age):
        self._age = age

s = Student(20)
s._age = 25
print(s._age)

Output:
-------
25

* Python ne koi error nahi diya, kyunki single underscore 
  access ko block nahi karta.

-------------------------------------------------------------------------------

Isliye yaad rakho:
------------------
.  age — normal public naming.
. _age — internal use ka signal.
. _age likhne se value store karne ka tareeka nahi badalta.
. _age likhne se Python automatic access restriction nahi lagata.

===============================================================================

4. Protected Convention, methods par bhi apply hota hai

* Abhi tak humne attribute dekha. Method ke naam ke aage bhi single 
  underscore laga sakte hain.

CODE:
-----
class Student:
    def __init__(self, age):
        self._age = age

    def _show_age(self):
        print(self._age)

Yahan:
------
. _age ek attribute hai.
. _show_age() ek method hai.
. Dono ko internal use ke liye maana gaya hai.

-------------------------------------------------------------------------------

* Lekin bahar se call karna technically possible hai:

s = Student(20)
s._show_age()

Output:
-------
20

* Python ise bhi block nahi karega.

===============================================================================

5. Inheritance mein _age ka kya use hai?

* Maan lo ek parent class hai aur usse ek child class banayi gayi hai.

CODE:
-----
class Person:
    def __init__(self, age):
        self._age = age

class Student(Person):
    def show_age(self):
        print(self._age)


s = Student(20)
s.show_age()

Output:
-------
20

* Child class Student, parent class Person ke _age attribute 
  ko access kar sakti hai.

* Single underscore inheritance mein access ko block nahi 
  karta. Ye bas convention hai ki attribute internal 
  implementation ka part hai.

===============================================================================

6. Quick revision:

Sawal                              | Jawab
-----------------------------------|--------------------------------
_age ka matlab?                    | Internal use ka signal
Bahar se access kar sakte hain?    | Haan
Bahar se modify kar sakte hain?    | Haan
Python restriction lagata hai?     | Nahi
Child class access kar sakti hai?  | Haan, agar attribute available hai

Sabse important line: Python mein Protected Convention (_name) ek naming 
                      convention hai, actual access restriction nahi.

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Q) Ab ek chhota sa question: agar class mein self._marks = 80 likha hai, 
   toh kya s._marks = 100 likhne par Python error dega, ya value change 
   ho jayegi?

ANS) Value change ho jayegi. Bilkul sahi! ✅

-------------------------------------------------------------------------------

CODE:
-----
class Student:
    def __init__(self):
        self._marks = 80

s = Student()
s._marks = 100

print(s._marks)  # 100

* Kyun? Python mein _marks protected hone ka sirf ek convention hai. 
        Python khud access ko block nahi karta.

Yaad rakho:
-----------
marks   → Public
_marks  → Protected convention (internal use ka signal)
__marks → Private-style (aage samjhenge)