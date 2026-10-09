1. Method Overriding kya hai?

* Jab Child Class, Parent Class ke method ke same naam ka method banati 
  hai aur uska apna implementation deti hai, toh use Method Overriding 
  kehte hain.

* Simple words mein: Parent Class ke method ko Child Class mein apne 
                     tareeke se define karna.

===============================================================================

2. Python example:
------------------
class Animal:        # Parent Class
    def sound(self):
        print("Animal makes a sound")


class Dog(Animal):   # Child Class
    def sound(self):
        print("Dog barks")


a = Animal()
d = Dog()

a.sound()
d.sound()

Output:
-------
Animal makes a sound
Dog barks

===============================================================================

3. Code ko samjho

Step 1: Parent Class
--------------------
* Animal mein sound() method hai, jo Animal makes a sound print karta 
  hai.

Step 2: Child Class
-------------------
* Dog, Animal se inherit karti hai. Lekin Dog apna sound() method bhi 
  banati hai aur usmein Dog barks print hota hai.

Step 3: Method call
-------------------
* a.sound() Parent Class ka method chalata hai, jabki d.sound() Child 
  Class ka apna method chalata hai.

Important: Jab Child Class mein same naam ka method define hota hai, 
           toh Dog object par sound() call karne par Child Class 
           wala method chalta hai, Parent Class wala nahi.

-------------------------------------------------------------------------------

# Table:

Sawal                                   | Jawab
========================================|======================================
Method Overriding kya hai?              | Child Class mein Parent method ko 
                                        | dobara define karna
-------------------------------------------------------------------------------
Method ka naam same hota hai?           | Haan
-------------------------------------------------------------------------------
Method ki implementation same hoti hai? | Zaroori nahi
-------------------------------------------------------------------------------
d.sound() par kaunsa method chalega?    | Dog class ka sound()
-------------------------------------------------------------------------------
a.sound() par kaunsa method chalega?    | Animal class ka sound()
-------------------------------------------------------------------------------
Method Overriding ka fayda?             | Child Class apna behaviour define 
                                        | kar sakti hai
-------------------------------------------------------------------------------

===============================================================================

4. Practice question

Agar code ye ho:
----------------
class Parent:
    def show(self):
        print("Parent")


class Child(Parent):
    def show(self):
        print("Child")


c = Child()
c.show()

Kya output aayega ? 
-------------------
Child

-------------------------------------------------------------------------------

Kyun?
-----
. Parent class mein show() method hai jo Parent print karta hai.
. Child class ne same naam show() ka apna method banaya hai.
. c = Child() se Child class ka object bana.
. c.show() call karne par Child class ka show() method chalta hai.

--> Isi ko Method Overriding kehte hain.

-------------------------------------------------------------------------------

Sawal                              | Jawab
-----------------------------------|----------------------------------------
Output kya hoga?                   | Child
Kyun?                              | Child class ne show() override kiya hai
Kaunsa method chalega?             | Child class ka show() method
Parent ka method bhi chalega?      | Nahi, automatically nahi

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Q) Sirf Method Overriding kaise karte hain ye yaad karna kaafi nahi hai 
   — ye kyun use karte hain, ye samajhna zyada zaroori hai.

ANS) 

1. Ek real example se samajh
----------------------------
* Maan le, tu ek game bana raha hai. Game mein alag-alag animals hain 
  aur har animal ki awaaz alag hai.

* Agar Method Overriding use nahi karein, toh har animal ke liye alag 
  method naam rakhne pad sakte hain:

CODE:
-----
class Dog:
    def dog_sound(self):
        print("Bhau bhau")

class Cat:
    def cat_sound(self):
        print("Meow meow")

* Ab Dog ke liye dog_sound() aur Cat ke liye cat_sound() yaad rakhna 
  padega.

===============================================================================

2. Method Overriding se kya fayda hua?

* Hum Parent Class mein ek common method sound() bana sakte hain aur 
  har Child Class mein uska apna behaviour define kar sakte hain.

CODE:
-----
class Animal:
    def sound(self):
        print("Animal makes a sound")


class Dog(Animal):
    def sound(self):
        print("Bhau bhau")


class Cat(Animal):
    def sound(self):
        print("Meow meow")


animals = [Dog(), Cat()]

for animal in animals:
    animal.sound()

Output:
-------
Bhau bhau
Meow meow

-------------------------------------------------------------------------------

Ab dhyan de:
------------
. Dono objects ke liye ek hi method naam hai: sound().
. Dog apni awaaz deta hai.
. Cat apni awaaz deti hai.
. Humein ye check karne ki zaroorat nahi ki object Dog 
  hai ya Cat. Hum dono par sound() call kar sakte hain.

--> Yahi iska main fayda hai!

===============================================================================

3. Asli fayda ek table mein:

Sawal                                  | Jawab
=======================================|=======================================
Method Overriding kyun karte hain?     | Child Class ka behaviour alag rakhne 
                                       | ke liye
-------------------------------------------------------------------------------
Same method naam kyun rakhte hain?     | Objects ko use karna aasan hota hai
-------------------------------------------------------------------------------
Parent ka method kyun override karein? | Jab Child ko apna behaviour chahiye
-------------------------------------------------------------------------------
Kya isse code kam ho sakta hai?        | Haan, khaaskar jab bahut saari Child 
                                       | Classes hon
-------------------------------------------------------------------------------
Kya har baar overriding zaroori hai?   | Nahi
-------------------------------------------------------------------------------

-------------------------------------------------------------------------------

* Sabse important baat: Method Overriding tab use karte hain jab Parent Class 
                        ka method sabhi Child Classes ke liye common ho, 
                        lekin har Child Class ko us kaam ko apne tareeke 
                        se karna ho.


* Jaise Animal.sound() common idea hai, lekin Dog bhonkta hai aur Cat meow 
  karti hai.

Aur ek baat: Method Overriding aur Inheritance alag cheezein hain. Inheritance 
             se Child Class Parent ka code use kar sakti hai; overriding se 
             Child Class us method ka behaviour apne hisaab se badal sakti 
             hai.

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

* Teri confusion samajh aa gayi. Tu animal ko object samajh raha hai, lekin 
  Python mein animal variable ka naam hai aur Animal() object banata hai. 
  Dono alag cheezein hain.

1. Pehle ye example dekh:
-------------------------
class Animal:
    pass

animal = Animal()
dog    = Animal()

Ismein:
-------
Animal   → class ka naam.
Animal() → ek naya object banata hai.
animal   → pehle object ko refer karne wala variable.
dog      → doosre object ko refer karne wala variable.

-------------------------------------------------------------------------------

Variable: animal
        |
Object 1 — Animal()

Variable: dog
        |
Object 2 — Animal()

* Dono variables alag objects ko refer kar rahe hain.

-------------------------------------------------------------------------------

* Bhai, yahan bas ek chhoti si baat hai: Animal same class hai, 
  lekin Animal() do baar likhne se do alag objects bante hain.

Ye code dekh:
-------------
class Animal:
    pass

animal = Animal()
dog = Animal()

Ismein:
-------
Animal          → ek hi class hai.
Pehla Animal()  → Object 1 banata hai.
Doosra Animal() → Object 2 banata hai.

<------------------------------------------------------>

Aise samajh:
------------

                                Animal class
                                Ek blueprint

               Object 1                          Object 2
               --------                          --------
               Animal()                          Animal()
               Variable: animal                  Variable: dog

* Jaise ek hi blueprint se do ghar ban sakte hain, waise hi 
  ek class se kai objects ban sakte hain.

<------------------------------------------------------>

Ek chhota test:
---------------
a = Animal()
b = Animal()
print(a is b)

Output:
-------
False

* is check karta hai ki dono variables usi ek object ko 
  refer karte hain ya nahi. Yahan False aayega, kyunki 
  dono alag objects hain.

===============================================================================

2. Ab asli confusion: ek variable alag objects ko kaise refer karta hai?

Ye code dekh:
-------------
animals = [Dog(), Cat()]

for animal in animals:
    animal.sound()

* Maan le list mein do objects hain: pehle Dog() aur phir Cat().

-------------------------------------------------------------------------------

# Loop aise chalta hai:

Pehli baar:
-----------
animal         → Dog object
animal.sound() → Bhau bhau

Doosri baar:
------------
animal         → Cat object
animal.sound() → Meow meow

* Aisa kyun ? Kyunki for loop har baar list se agla object leta hai 
  aur variable animal ko us object ko refer karne deta hai.

* animal koi fixed Dog ya Cat object nahi hai. Woh sirf variable ka 
  naam hai.

-------------------------------------------------------------------------------

3. Ek aur important difference:

animal = Animal()
dog = Dog()

* Yahan animal aur dog do alag variables hain, aur dono alag objects ko 
  refer karte hain.

Lekin:
------
animal = Dog()
animal = Cat()

* Yahan pehli line mein animal Dog object ko refer karta hai. Doosri line 
  mein wahi variable ab Cat object ko refer karta hai.

-------------------------------------------------------------------------------

Sawal                                              | Jawab
===================================================|===========================
animal = Animal() mein object kya hai?             | Animal() se bana object
-------------------------------------------------------------------------------
animal kya hai?                                    | Variable ka naam
-------------------------------------------------------------------------------
Kya variable aur object same hain?                 | Nahi
-------------------------------------------------------------------------------
Kya variable doosre object ko refer kar sakta hai? | Haan
-------------------------------------------------------------------------------
For loop mein animal kya karta hai?                | Har baar agle object ko 
                                                   | refer karta hai
-------------------------------------------------------------------------------