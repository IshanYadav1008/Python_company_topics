1. Code Reusability (Code ko dobara use karna)

* Parent Class ka method Child Class mein dobara likhne ki 
  zaroorat nahi hoti.

CODE:
-----
class Animal:
    def eat(self):
        print("Eating")

class Dog(Animal):
    pass

d = Dog()
d.eat()

Output:
-------
Eating

* Fayda: Dog class mein eat() dobara nahi likhna pada.

==============================================================================

2. Code Duplication kam hota hai

* Agar Dog, Cat aur Cow sabko eat() method chahiye, toh ek hi Parent 
  Class Animal mein method likh sakte hain. Teeno Child Classes use 
  inherit kar sakti hain.

==============================================================================

3. Code ko Maintain karna aasan hota hai

* Agar Parent Class ke eat() method mein change karna ho, toh use ek hi 
  jagah change kar sakte hain. Child Classes us updated method ko inherit 
  karti hain, jab tak woh method khud override na karein.

==============================================================================

4. Code ko Extend karna aasan hota hai

* Child Class Parent Class ke methods use karne ke saath apne naye 
  methods bhi bana sakti hai.

CODE:
-----
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    def bark(self):
        print("Barking")

* Yahan Dog, eat() bhi use kar sakti hai aur apna bark() method bhi.

==============================================================================

# Table

Sawal                                | Jawab
==============================================================================
Inheritance ka main fayda?           | Code reusability
------------------------------------------------------------------------------
Code reusability kya hai?            | Parent Class ka code dobara use karna
------------------------------------------------------------------------------
Code duplication kaise kam hota hai? | Same code baar-baar nahi likhna padta
------------------------------------------------------------------------------
Maintenance ka fayda?                | Common code ko ek jagah update kar sakte 
                                       hain.
------------------------------------------------------------------------------
Code extend karne ka matlab?         | Child Class mein naye methods add karna
------------------------------------------------------------------------------

* Yaad rakh: Inheritance ka main fayda hai code reuse karna, duplicate code 
             kam karna aur code ko maintain karna aasan banana.