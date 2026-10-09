1. super() kya hai?

* super() ka use Child Class ke andar se Parent Class ke methods 
  ko call karne ke liye hota hai.

Pehle ek example dekh.
----------------------
class Parent:
    def show(self):
        print("Parent class")

class Child(Parent):
    def show(self):
        print("Child class")
        super().show()

c = Child()
c.show()

Output:
-------
Child class
Parent class

================================================================================

2. Code kaise kaam kar raha hai?

Step 1: c.show()
----------------
--> Child Class ka show() method call hota hai.

Step 2: print("Child class")
----------------------------
--> Output mein Child class print hota hai.

Step 3: super().show()
----------------------
--> Python Parent Class ka show() method call karta hai.

Step 4: Parent ka output
------------------------
--> Parent class print hota hai.

================================================================================

3. super() ka fayda kya hai?

* Maan le Parent Class mein pehle se kuch useful code hai aur Child 
  Class ko bhi apna extra kaam karna hai.

* super() se Parent ka code dobara likhe bina use kar sakte hain.

CODE:
-----
class Animal:
    def eat(self):
        print("Animal is eating")

class Dog(Animal):
    def eat(self):
        super().eat()
        print("Dog is eating")

d = Dog()
d.eat()

Output:
-------
Animal is eating
Dog is eating

* Yahan Dog Parent ka eat() method bhi chala raha hai aur apna extra 
  behaviour bhi add kar raha hai.

* Dhyan do: Agar super().eat() hata dein, toh sirf Dog is eating print 
            hoga.

================================================================================

4. Copy karne ke liye table:

Sawal                                    | Jawab
=========================================|======================================
super() kya hai?                         | Parent class ke methods tak pahunchne 
                                         | ka tareeka
--------------------------------------------------------------------------------
super().show() kya karta hai?            | Parent ka show() method call karta 
                                         | hai
--------------------------------------------------------------------------------
Kya super() compulsory hai?              | Nahi
--------------------------------------------------------------------------------
super() ka fayda kya hai?                | Parent ka code dobara likhe bina 
                                         | use karna
--------------------------------------------------------------------------------
Kya Child apna code bhi chala sakti hai? | Haan
--------------------------------------------------------------------------------

================================================================================

5. Practice question

* Is code ka output kya hoga ?

CODE:
-----
class Parent:
    def greet(self):
        print("Hello from Parent")

class Child(Parent):
    def greet(self):
        print("Hello from Child")
        super().greet()

c = Child()
c.greet()

O/P:
----
Pehle Hello from Child, phir Hello from Parent

--------------------------------------------------------------------------------

Bilkul sahi! ✅ Tera jawab correct hai.

Output:
-------
Hello from Child
Hello from Parent

Kyun?
-----
1. c.greet() se Child class ka greet() method chalta hai.
2. print("Hello from Child") pehle execute hota hai.
3. super().greet() Parent class ka greet() method call 
   karta hai.
4. Isliye Hello from Parent baad mein print hota hai.

Sawal                         | Jawab
------------------------------|----------------------------------
Pehle kya print hoga?         | Hello from Child
super().greet() kya karega?   | Parent ka greet() method call karega
Baad mein kya print hoga?     | Hello from Parent