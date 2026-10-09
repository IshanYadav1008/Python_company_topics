Q) teak hai mai wahi bol rah hu ki jab es tarah se value object mai assign 
   ho sakti hai toh phir init ka kya role reh jaata hai, kyuki phir toh 
   bina wajah extra line of code ban raha hai ?

------------------------------------------------------------------------------

ANS)  Bilkul — ab tumhara actual doubt clear hai. Tum keh rahe ho:

* “Agar get_age() ke andar hi self.age = age karke object mein 
   value store kar sakte hain, toh __init__ ki kya zarurat hai?”

Answer: __init__ zaroori nahi hai. Lekin uska role alag hai.

1. Bina __init__ ke bhi possible hai:
-------------------------------------
class Student:
    def set_age(self, age):
        self.age = age

    def get_age(self):
        return self.age

Use:
----
s1 = Student()
s1.set_age(20)
print(s1.get_age())

--> Ye perfectly valid hai. ✅
--> Yahan __init__ nahi hai.

==============================================================================

2. Toh __init__ kyun use karte hain?

* Kyuki hum aksar chahte hain ki object bante hi uske paas initial data ho.

CODE:
-----
class Student:
    def __init__(self, age):
        self.age = age

    def get_age(self):
        return self.age

Ab:
---
s1 = Student(20)

<------------------------------------------------->

* Object banate hi:

Student(20)
   ↓
__init__(age)
   ↓
self.age = 20

Ab object already ready hai:
----------------------------
=> print(s1.get_age())

Output:
-------
20

==============================================================================

# Dono approaches compare karo

Without __init__:
-----------------
s1 = Student()
s1.set_age(20)

--> 2 steps.

<---------------------------------------------->

With __init__:
--------------
s1 = Student(20)

--> 1 step.

==============================================================================

# Aur asli fayda

* Maan lo Student ke paas 3 cheezein honi hi chahiye:

CODE:
-----
class Student:
    def __init__(self, name, age, city):
        self.name = name
        self.age = age
        self.city = city

Ab:
---
s1 = Student("Rahul", 20, "Indore")

--> Object banate hi complete initial state mil gayi.

------------------------------------------------------------------------------

# Agar __init__ na ho, toh:

s1 = Student()
s1.set_name("Rahul")
s1.set_age(20)
s1.set_city("Indore")

--> Bahut extra steps.

------------------------------------------------------------------------------

Isliye mental model:
--------------------
__init__
   ↓
Object ko START mein initialize karta hai

setter
   ↓
Object banne KE BAAD value change karta hai

getter
   ↓
Current value read karta hai

------------------------------------------------------------------------------

* So tumhari baat technically correct hai:

__init__ compulsory nahi hai.

Lekin:
------
__init__ ka purpose “value assign karna possible banana” nahi hai; 
purpose hai object ko creation ke time initial state dena.

Aur ek important correction: get_age(self, age) mein value set karna 
getter ka normal role nahi hoga. Agar method value set kar raha hai,
woh setter/initializer ka kaam kar raha hai.

==============================================================================
------------------------------------------------------------------------------
==============================================================================

Q) Ab tumhara main question

"Agar maine bahut saari values initialize ki hain, toh kya har 
 value ke liye setter likhna padega?"

ANS) Nahi. Bilkul nahi.

**Ye bahut important hai:**

* Har attribute ke liye setter banana compulsory nahi hai.

Maan lo:
--------
class Student:

    def __init__(self, name, age, city):
        self.name = name
        self._age = age
        self.city = city

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):
        if value >= 0:
            self._age = value

Yahan 3 values hain:
--------------------
name
age
city

* Lekin setter sirf age ke liye banaya hai.

* Kyun? Kyuki hume age par validation chahiye:

=> if value >= 0:

<------------------------------------------------------------------>

* name ke liye setter ki zarurat nahi hai:

=> s1.name = "Rahul"

<------------------------------------------------------------------>

* city ke liye bhi zarurat nahi hai:

=> s1.city = "Indore"

<------------------------------------------------------------------>

* Lekin age mein control chahiye:

=> s1.age = -50

* Toh setter rok sakta hai: Age cannot be negative.

==============================================================================

Ekdum simple rule
-----------------

Normal value
    ↓
self.name = name
self.city = city

<----------------------------------------------------->

Special control/validation chahiye:
    ↓
@property
@age.setter

------------------------------------------------------------------------------

* Isliye @age.setter ka matlab ye nahi hai:

"Har variable ke liye setter banana padega."

Iska matlab sirf: "Jab age property ko bahar se change
                   kiya jaaye, toh ye special method 
                   use karo."

<----------------------------------------------------->

* Aur ek aur important point:

=> s1 = Student(20)  // mein 20 initial value hai → __init__ 
                        handle karta hai.

=> s1.age = 25       // mein 25 baad mein change ki gayi 
                        value hai → @age.setter handle 
                        karta hai.

=> print(s1.age)     // mein current value read ho rahi 
                        hai → @property getter handle 
                        karta hai.

__init__       → initial value
      ↓
@property      → value read
      ↓
@age.setter    → value change

* Ye teenon ka role alag hai.

==============================================================================
------------------------------------------------------------------------------
==============================================================================

Q) s1.age = 25 likhne se value change ho jaati hai vo toh smj aaye 
   lekin es tarah value setter method ko pass kaise hoti hai bina 
   paranthesis ka use kiye ?

------------------------------------------------------------------------------

* Exactly! Yehi @property + setter ka sabse important magic hai. 
  Tumhara question bilkul sahi hai.

--> Normally method ko value dene ke liye parentheses chahiye:

=> s1.set_age(25)

--> Lekin @age.setter ke case mein:

s1.age = 25  // likhte hain — parentheses nahi lagte.

------------------------------------------------------------------------------

Actually andar se kya hota hai? Python ko pata hai ki age ek property 
                                hai aur us property ka setter defined 
                                hai:

@age.setter
def age(self, value):
    self._age = value

* Toh jab Python dekhta hai:

=> s1.age = 25

woh samajhta hai: "age property ki value set ho rahi hai. 
                   Is property ka setter hai, toh setter 
                   ko 25 dekar chalao."

------------------------------------------------------------------------------

Conceptually:
-------------
s1.age = 25
     ↓
age property ka setter dhoondo
     ↓
age(self, value)
     ↓
value = 25
     ↓
self._age = 25

==============================================================================

# Compare karo

Normal setter:
--------------
def set_age(self, value):
    self._age = value

s1.set_age(25)   // Yahan tum khud method call kar rahe ho:

set_age(25)
        ↑
   parentheses

------------------------------------------------------------------------------

Property setter:
----------------
@age.setter
def age(self, value):
    self._age = value

s1.age = 25  // Yahan tum method ko directly call nahi kar rahe.

* Tum property ko value assign kar rahe ho, aur Python 
  automatically setter method ko call kar deta hai.

==============================================================================

* Isliye @age.setter ko aise yaad rakho:

=> s1.age = 25  // dekhne mein ye normal assignment lagta hai.

Lekin kyunki age property hai:
------------------------------
s1.age = 25
      ↓
Python: "age ka setter bana hua hai"
      ↓
setter automatically call
      ↓
value = 25

------------------------------------------------------------------------------

* Parentheses isliye nahi hain kyunki tum age() method ko manually 
  call nahi kar rahe; = operation Python ko setter trigger karne 
  deta hai.

* Aur isi wajah se property setter ka syntax convenient hai:

=> s1.age = 25

instead of:
-----------
=> s1.set_age(25)

* Dono ka purpose value change karna hai, bas interface/syntax 
  different hai.