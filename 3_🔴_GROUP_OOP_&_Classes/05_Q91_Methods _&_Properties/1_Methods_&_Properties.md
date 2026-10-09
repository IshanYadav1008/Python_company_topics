1. Sabse pehle: Class hoti kya hai?

* Class ko abhi simple language mein blueprint / design samjho.

Example:
--------
class Student:
    pass

* Ye Student ek design hai.

Is design se hum objects bana sakte hain:
-----------------------------------------
student1 = Student()
student2 = Student()

Ab:
---
Student  → Blueprint

student1 → Object
student2 → Object

Jaise:
------
* Car ek blueprint hai
* BMW ki ek actual car object ho sakti hai.

==================================================================================

2. Class ke andar hum kya rakh sakte hain?

* Class ke andar mainly do important cheezein hoti hain:

Class
│
├── Data → Attributes
│
└── Behaviour/Kaam → Methods

Example:
--------
class Student:

    name = "Rahul"       # Data / Attribute

    def study(self):     # Kaam / Method
        print("Student is studying")

Yahan:
------
name       → Attribute
study()    → Method

* Ab Method ko samjho.

==================================================================================

3. Method kya hota hai?

* Sabse simple definition: Class ke andar jo function hota hai, 
                           use method kehte hain.

* Python mein normally hum function aise likhte hain:

<-------------------------------------------------------------->

def greet():
    print("Hello")   // Ye ek function hai.

<-------------------------------------------------------------->

* Lekin agar ye class ke andar hai:

class Student:

    def greet(self):
        print("Hello")

--> To greet() ek method hai.

<-------------------------------------------------------------->

Yaad rakho:
-----------

Function
    ↓
Class ke bahar

Method
    ↓
Class ke andar

==================================================================================

4. Method ka kaam kya hai?

* Method kisi action/behaviour ko represent karta hai.

Student kya kar sakta hai?
--------------------------
study
eat
sleep
play
introduce

<-------------------------------------------------------------->

* Toh hum methods bana sakte hain:

class Student:

    def study(self):
        print("Student is studying")

    def play(self):
        print("Student is playing")

    def sleep(self):
        print("Student is sleeping")

Yahan:
------
study()  → action
play()   → action
sleep()  → action

--> Ye sab methods hain.

==================================================================================

5. self kya hai?

* Abhi self ko bahut deep mein mat le jao.

* Bas itna samjho: self current object ko refer karta hai.

Example:
--------
class Student:

    def introduce(self):
        print("Hello, I am a student")

Object:
-------
s1 = Student()

Method call:
------------
s1.introduce()

* Yahan Python internally roughly ye samajhta hai:

s1 → introduce()  // Aur self us s1 ko refer karta hai.

* Isliye instance methods mein generally:

def introduce(self):  // likhte hain.

==================================================================================

6. Method ko real life se samjho

* Socho tumhare paas ek mobile phone hai.

Mobile ke paas kuch data hai:
-----------------------------
Brand = Samsung
Color = Black
Battery = 80%    // Ye attributes/data hain.

<-------------------------------------------------------------->

* Mobile kuch kaam bhi kar sakta hai:

call()
camera()
play_music()
take_photo()

* Ye methods/actions hain.

<-------------------------------------------------------------->

So:
---

Object
│
├── Data
│   ├── brand
│   ├── color
│   └── battery
│
└── Actions
    ├── call()
    ├── camera()
    └── take_photo()

--> Python OOP mein exactly isi tarah sochna hai.

==================================================================================
----------------------------------------------------------------------------------
==================================================================================

7. Ab aate hain Properties par

* Yahan students ko sabse zyada confusion hota hai.

Pehle attribute samjho.
-----------------------
class Student:

    def __init__(self, name):
        self.name = name

Object:
-------
s1 = Student("Rahul")

Ab:
---
print(s1.name)

Output:
-------
Rahul

* Yahan name ek attribute hai.
* Hum simply bol sakte hain: s1 ka name kya hai?
* Aur Python directly value de deta hai.

==================================================================================

8. To Property kya hai?

* Property ko abhi simple language mein aise samjho:

* Property ek aisa mechanism hai jisse hum kisi value ko attribute 
  ki tarah access kar sakte hain, lekin us value ko access karne 
  ke peeche logic bhi laga sakte hain.

Ye line thodi difficult hai.
----------------------------
Isliye example se samjho.

Normal attribute:
-----------------
s1.age             // Direct value mil gayi.

----------------------------------------------------------------------------------

* Lekin maan lo tum chahte ho ki age lene se pehle kuch calculation ho.

Example:
--------
User ki birth year = 2000
Current year       = 2026

age                = 2026 - 2000

* Hum chahte hain user simply likhe:

=> person.age   // Aur Python internally calculation karke age de de.

* Yahan property useful hoti hai.

==================================================================================

9. Property ka sabse simple idea

* Normally method ko call karte hain:

=> person.get_age()   // () dekhkar pata chal raha hai ki ye 
                            method hai.

<-------------------------------------------------------------->

* Property ke saath:

=> person.age   // Hum () nahi lagate.

# Matlab

Method:
-------
person.get_age()
       ↑
    action call


Property:
---------
person.age
       ↑
 value ko attribute
 ki tarah access

* Yahi property ka core idea hai.

==================================================================================

10. @property kya karta hai?

* Python mein property banane ke liye commonly:

# @property use karte hain.

Example:
--------
class Student:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

Ab:
---
s1 = Student(20)
print(s1.age)

Output:
-------
20

<-------------------------------------------------------------->

# Dhyan do:

Humne likha:
------------
s1.age

not

s1.age()

* Kyun ? Kyuki @property ne age() method ko property ki 
         tarah access karne diya.

==================================================================================

11. Method vs Property — Main Difference

**Ye bahut important hai.**

Method
------
Method usually kaam/action represent karta hai.

=> student.study()
=> student.walk()
=> student.introduce()

Question:
---------
"Student kya kar raha hai?"

Answer:
-------
Study, walk, introduce.

----------------------------------------------------------------------------------

Property
--------
Property generally kisi value/data ko access karne ke liye hoti hai.

=> student.name
=> student.age
=> student.email

Question:
---------
"Student ke paas kya value hai?"

Answer:
-------
Name, age, email.

==================================================================================

12. Lekin property aur normal attribute mein difference kya?

**Ye next important point hai.**

Normal attribute:
-----------------
class Student:

    def __init__(self, age):
        self.age = age

Yahan:
------
s1.age  // directly stored value access karta hai.

----------------------------------------------------------------------------------

Property:
---------
class Student:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

Ab:
---
s1.age  // likhne par Python actually property ke logic ko execute karta hai.

----------------------------------------------------------------------------------

Matlab:
-------
Normal Attribute

s1.age
   ↓
stored value

----------------------------------------------------------------------------------

Property:
---------
s1.age
   ↓
property ka logic
   ↓
value

* Isi wajah se property powerful hai.

==================================================================================

13. Ek real-life example

* Socho ATM hai or Tum ATM mein balance dekhte ho : Balance → ₹10,000

* Tum simply dekhna chahte ho                     : balance

Lekin system ke andar bahut saara logic ho sakta hai:
-----------------------------------------------------
Account check karo
↓
Transactions calculate karo
↓
Current balance nikalo
↓
Balance return karo

<-------------------------------------------------------------->

User ko ye sab nahi dikh raha.
------------------------------

* User ko simply: "account.balance" jaisa interface mil raha hai.

* Property ka idea kuch aisa hi hai: simple access outside, logic inside.

==================================================================================

14. Methods + Properties ek class mein

Ab dono ko ek saath dekho:
--------------------------
class Student:

    def __init__(self, name, age):
        self.name = name
        self._age = age

    def study(self):
        print(self.name, "is studying")

    @property
    def age(self):
        return self._age

Object:
-------
s1 = Student("Rahul", 20)

Ab:
---
s1.name     → Attribute

s1.age      → Property

s1.study()  → Method

To:
---
Student
│
├── name
│   └── Attribute
│
├── age
│   └── Property
│
└── study()
    └── Method

==================================================================================

15. Abhi Getter/Setter ko kahan rakhein?

Abhi bas itna samjho:
---------------------
@property
    ↓
Property banata hai
    ↓
Getter
    ↓
Value read karne ka logic

<-------------------------------------------------------------->

Aur baad mein:
--------------
@property
    ↓
Getter

@property_name.setter
    ↓
Setter
    ↓
Value change karne ka logic

<-------------------------------------------------------------->

Example:
--------
class Student:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):              # Getter
        return self._age

    @age.setter
    def age(self, value):       # Setter
        self._age = value

* Lekin getter/setter ko abhi ratne ki zarurat nahi hai. Pehle 
  methods aur property ka concept strong karo.

==================================================================================

16. Sabse important mental model 🧠

Isko yaad kar lo:
-----------------

CLASS
  ↓
Object ka design
  ↓
┌──────────────────────────┐
│ Data                     │
│ ↓                        │
│ Attributes / Properties  │
│                          │
│ Kaam                     │
│ ↓                        │
│ Methods                  │
└──────────────────────────┘

<-------------------------------------------------------------->

Attribute
---------
"Mere paas kya data hai?"

=> student.name
=> student.age

<-------------------------------------------------------------->

Method
------
"Main kya kaam kar sakta hoon?"

=> student.study()
=> student.play()

<-------------------------------------------------------------->

Property
--------
"Mujhe data attribute ki tarah chahiye, lekin uske access ke 
 peeche logic/control ho."

=> student.age

==================================================================================

17. Ekdum short mein
--------------------

| Concept     | Simple meaning                             | Example             |
| ----------- | ------------------------------------------ | ------------------- |
| Attribute   | Object ka data                             | `student.name`      |
| Method      | Object ka action/kaam                      | `student.study()`   |
| Property    | Controlled data access                     | `student.age`       |
| `@property` | Method ko property jaisa access karata hai | `student.age`       |
| Getter      | Value read karta hai                       | `return self._age`  |
| Setter      | Value change/set karta hai                 | `self._age = value` |

==================================================================================

Aur tumhare current topic ka flow:
----------------------------------

Methods & Properties
       ↓
Method kya hai?
       ↓
Instance Method
       ↓
Property kya hai?
       ↓
@property
       ↓
Getter
       ↓
Setter

Abhi tumhe sirf itna pakka karna hai:
-------------------------------------
Method    = kaam/action
Attribute = data
Property  = data ko attribute ki tarah access karne ka controlled mechanism