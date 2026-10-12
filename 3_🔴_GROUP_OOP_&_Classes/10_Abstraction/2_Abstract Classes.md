2. Abstract Class kya hoti hai?

Sabse pehle simple definition samjho:
-------------------------------------
* Abstract Class ek aisi class hoti hai jo doosri classes ke liye common 
  structure aur rules define karti hai.

* Iska use tab hota hai jab hum chahte hain ki kuch common methods har 
  Child class mein hon, lekin un methods ka actual kaam har Child class 
  apne hisaab se define kare.

==================================================================================

1. Ek simple example dekho:
---------------------------
* Maan lo hum Animal class bana rahe hain. Har animal sound karta hai, 
  lekin har animal ki sound alag hoti hai.

* Hum chahte hain ki har Animal ki Child class mein sound() method zaroor 
  ho.

class Animal:
    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        print("Bhau bhau")

class Cat(Animal):
    def sound(self):
        print("Meow meow")

* Is example mein Animal ek normal Parent class hai, Abstract Class nahi. 
  pass likhne se class abstract nahi ban jaati.

* Abhi Dog aur Cat dono sound() ko apne hisaab se define kar rahe hain, 
  lekin Python unhe aisa karne ke liye force nahi karta.

==================================================================================

2. Abstract Class ki zaroorat kyun hai ?

* Maan lo koi Child class sound() method banana bhool jaaye. Hum chahte 
  hain ki Python aisi class ka object banane hi na de.

* Iske liye Python mein ABC aur @abstractmethod use karte hain. Inhe agle 
  topics mein detail se padhenge.

Abhi bas ye code dekho:
-----------------------
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        print("Bhau bhau")

dog = Dog()
dog.sound()

Output:
-------
Bhau bhau

* Yahan Animal ek Abstract Class hai, aur sound() ek abstract method hai.

* Agar hum Dog mein sound() implement na karein aur Dog ka object banayein, 
  toh Python TypeError dega.

==================================================================================

3. Normal Class aur Abstract Class mein farak:

Normal Class                    | Abstract Class
--------------------------------|----------------------------------------
Object bana sakte hain.         | Direct object nahi bana sakte.
Methods implement kar sakti hai.| Abstract methods declare kar sakti hai.
Child ko method implement       | Abstract method implement karna
karne ke liye force nahi karti. | Child ke liye zaroori hota hai.

* Ek important baat: Abstract Class mein normal methods bhi ho sakte hain. 
                     Aur abstract method ko implement karna zaroori tab 
                     hota hai jab tum us Child class ka object banana 
                     chahte ho.


Yaad rakhne wali baat
---------------------
- Abstraction             : Concept hai — implementation ki details chhupana.
- Abstract Class          : Common structure aur rules define karne wali class.
- ABC aur @abstractmethod : Python mein Abstract Class banane aur abstract methods 
                            enforce karne ke tools.