1. Sabse pehle: Attribute kya hota hai?

* Attribute = object ke andar stored data.

CODE:
-----
class Student:
    def __init__(self, age):
        self.age = age

Agar:
-----
s1 = Student(20)

toh:
----
s1
└── age = 20

* Yahan age ek instance attribute hai.

Hum directly kar sakte hain:
----------------------------
print(s1.age)    # GET
s1.age = 25      # SET

=================================================================================

2. Problem kya hai?

* Direct attribute mein koi bhi value daal sakte ho:

s1.age = 25
s1.age = 50
s1.age = -100

* Python automatically nahi jaanta ki: "Age negative nahi honi chahiye."

* Humein control/validation chahiye or Yahin se Getter/Setter useful 
  hote hain.

=================================================================================

3. Getter kya hota hai?

* Getter = kisi value ko GET/read karne ka mechanism.

Simple example:
---------------
class Student:
    def __init__(self, age):
        self._age = age

    def get_age(self):
        return self._age

Ab:
---
s1 = Student(20)
print(s1.get_age())

Output:
-------
20

Yahan:
------
def get_age(self):      // * Ye getter method hai.
    return self._age

Simple definition:
------------------
Getter ka kaam = value ko read/get karna.

=================================================================================

4. Setter kya hota hai?

* Setter = kisi value ko SET/change karne ka mechanism.

CODE:
-----
class Student:
    def __init__(self, age):
        self._age = age

    def set_age(self, value):
        self._age = value

Ab:
---
s1.set_age(25)

* _age change ho jayega: _age = 25

Simple definition:
------------------
Setter ka kaam = value ko set/change karna.

=================================================================================

5. Lekin Python mein @property kyun?

Normal getter mein:
-------------------
s1.get_age()        // likhna padta hai.

* Lekin Python humein ye convenient syntax deta hai:

=> @property

* Ab getter ko property bana sakte hain.

CODE:
-----
class Student:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

Ab:
---
s1.age  // likho, () nahi lagana.

=================================================================================

6. @property ka actual meaning

Ye:
---
@property
def age(self):
    return self._age

* ka matlab: "age ko property bana do."

Isliye:
-------
s1.age   // likhne par Python age() ke andar ka code execute 
            karta hai.

<----------------------------------------------------------->

Flow:
-----
s1.age
  ↓
@property wala age()
  ↓
return self._age
  ↓
20

<----------------------------------------------------------->

Important:
----------
* @property wala method getter ban jaata hai.

* Isliye Python mein alag se: @getter, likhne 
  ki zarurat nahi hoti.

=================================================================================

7. Ab _age kya hai?

**Ye bahut important hai.**

=> self._age = age  // mein _age property nahi hai.

* Ye simply instance attribute hai jisme actual value stored hai.

=> _age = actual stored value

Aur:
----
@property
def age(self):   // mein age property hai.

So:
---
age
↓
PROPERTY

_age
↓
STORED ATTRIBUTE

=================================================================================

8. age parameter kya hai?

* Ye bhi alag cheez hai.

=> def __init__(self, age):   // mein age parameter hai.

Agar:
-----
s1 = Student(20)

toh:
----
parameter age = 20

<------------------------------------------------------->

Phir:
-----
self._age = age

ka matlab:
----------
self._age = 20

<------------------------------------------------------->

So complete picture:
--------------------
def __init__(self, age):
                  ↑
              PARAMETER

<------------------------------------------------------->

self._age = age
     ↑
INSTANCE ATTRIBUTE
     ↑
actual value stored

<------------------------------------------------------->

@property
def age(self):
    ↑
 PROPERTY

=================================================================================

9. self.age vs self._age

* Ye tumhare liye sabse important distinction hai.

=> self.age

--> Normally: age naam ke attribute/property ko access karo.

=> self._age

--> _age naam ke attribute ko access karo.

Ye do alag names hain.

<------------------------------------------------------->

Example:
--------
self.age = 20
self._age = 50

Toh:
----
self.age  → 20

aur:

self._age → 50

=================================================================================

10. Property ke case mein hum _age kyun use karte hain?

Typical pattern:
----------------
class Student:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

Yahan:
------
age   → public property
_age  → internal stored value

Flow:
-----
s1.age
   ↓
age property
   ↓
self._age
   ↓
20

=================================================================================

11. self.age ko getter ke andar kyun nahi likhte?

Agar:
-----
@property
def age(self):
    return self.age

Toh dekho:
----------
s1.age
  ↓
age property
  ↓
return self.age
  ↓
self.age means age property
  ↓
age property
  ↓
return self.age
  ↓
age property
  ↓
...

* Ye recursion hai.

* Dhyah se dekho, "def age(self)" or "self.age" ye dono mai same name
  age hai.

---------------------------------------------------------------------------------

* Yahan koi for/while loop nahi hai.

* Problem ye hai ki property khud ko hi dobara access kar rahi hai.

Isliye:
-------
@property
def age(self):
    return self._age

* use karte hain, Because _age normal stored attribute hai, property nahi.

=================================================================================

12. Lekin number property mein self.age use kar sakte hain?

Haan!

Example:
--------
class Student:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

    @property
    def number(self):
        return self.age

* Ye perfectly fine hai.

* Kyun?

Because:
--------
number property
      ↓
self.age
      ↓
age property
      ↓
self._age
      ↓
20

* Yahan koi property khud ko call nahi kar rahi.

<------------------------------------------------------->

Problem sirf:
-------------
@property
def age(self):
    return self.age   // mein hai.

Because:
--------
age → age → age → age...

=================================================================================

13. Ab Setter

Getter:
-------
@property
def age(self):
    return self._age

* Ab humein value change/set bhi karni hai.

<------------------------------------------------------->

Setter:
-------
@age.setter
def age(self, value):
    self._age = value

<------------------------------------------------------->

Complete:
---------
class Student:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):
        self._age = value

=================================================================================

14. @age.setter ka meaning:

@age.setter
def age(self, value):

* Python ko bol raha hai: "age property ke liye ye SETTER hai."

So:
---
s1.age      → getter

s1.age = 25 → setter

<------------------------------------------------------->

Yaad rakho:
-----------
GET:

s1.age
   ↓
getter

<------------------------------------------------------->

SET:
----
s1.age = 25
   ↓
setter

=================================================================================

15. Setter ka actual benefit — validation

* Ab hum setter mein rules laga sakte hain:

CODE:
-----
class Student:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):
        if value >= 0:
            self._age = value
        else:
            print("Age cannot be negative")

Ab:
---
s1.age = 25  → allowed.

Lekin:
------
s1.age = -10 → rejected.

Flow:
-----
s1.age = -10
       ↓
   setter
       ↓
value >= 0 ?
       ↓
     NO
       ↓
 reject

* Yahi Setter ka main practical benefit hai:

* Value set karne se pehle control/validation laga sakte ho.

=================================================================================

16. Getter bhi control de sakta hai

* Getter sirf stored value return karne ke liye hi nahi hota.

Example:
--------
@property
def age(self):
    return 2026 - self.birth_year  // Yahan age directly store nahi hui.

* Python calculation karke age de raha hai.

So property ka use:
-------------------
1. value read karna
2. calculation karna
3. access control
4. logic lagana

etc. ke liye ho sakta hai.

=================================================================================

17. Getter + Setter ka complete mental model

* Isko notes mein ye diagram zaroor likhna:

                 Student Object
                       │
                       ↓
                  _age = 20
                 (stored data)
                       ↑
                       │
              ┌────────┴────────┐
              │                 │
           GETTER             SETTER
              │                 │
       @property             @age.setter
              │                 │
          s1.age           s1.age = 25
              │                 │
              ↓                 ↓
          _age read          _age change

=================================================================================

18. Getter vs Setter — one-line definitions:

Getter
------
Getter = value ko read/get karne ka mechanism.

@property
def age(self):
    return self._age

<------------------------------------------------------->

Setter
------
Setter = value ko set/change karne ka mechanism.

@age.setter
def age(self, value):
    self._age = value

=================================================================================

19. Normal attribute vs Getter/Setter:

Normal attribute
----------------
class Student:
    def __init__(self, age):
        self.age = age

Direct:
-------
s1.age
s1.age = 25

* No special control.

---------------------------------------------------------------------------------

Getter/Setter property:
-----------------------
class Student:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):
        if value >= 0:
            self._age = value

Ab:
---
s1.age       → getter

s1.age = 25  → setter

* Aur setter mein validation bhi laga sakte ho.

=================================================================================

20. Sabse important 7 points — notes ke liye:

1. Attribute = object ke andar stored data.

2. Getter = value GET/read karne ka mechanism.

3. Setter = value SET/change karne ka mechanism.

4. @property = getter ko attribute-style access deta hai.

5. @age.setter = age property ka setter banata hai.

6. _age = usually internal stored attribute.

7. age = property/interface jiske through _age ko 
         access/control karte hain.

---------------------------------------------------------------------------------

Final pattern yaad karo:
------------------------
class Student:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):              # GETTER
        return self._age

    @age.setter
    def age(self, value):       # SETTER
        if value >= 0:
            self._age = value
        else:
            print("Age cannot be negative")


# Object create
s1 = Student(20)

# Getter
print("Initial age:", s1.age)

# Setter
s1.age = 25

# Getter again
print("Updated age:", s1.age)

Output
------
Initial age: 20
Updated age: 25


Ek line ka mental model:
------------------------
--> age  = bahar se access karne ka door.
--> _age = andar rakhi actual value.

--> Getter door se value nikalta hai
--> Setter door se value change karta hai.