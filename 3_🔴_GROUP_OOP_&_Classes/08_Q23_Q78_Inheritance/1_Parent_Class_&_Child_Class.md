1. Parent Class aur Child Class kya hoti hain?

* Parent Class : Woh class jiske attributes aur methods ko doosri class 
                 inherit kar sakti hai.

* Child Class  : Woh class jo Parent Class ke attributes aur methods ko 
                 inherit karti hai.

--> Simple example: Parent class mein Animal hai aur Child class mein 
                    Dog hai. Dog ek animal hai, isliye Dog class Animal 
                    ko inherit kar sakti hai.

=================================================================================

2. Python code example:
-----------------------
class Animal:  # Parent Class
    def eat(self):
        print("Animal is eating")


class Dog(Animal):  # Child Class
    def bark(self):
        print("Dog is barking")


d = Dog()
d.eat()   # Parent class ka method
d.bark()  # Child class ka method

Output:
-------
Animal is eating
Dog is barking

---------------------------------------------------------------------------------

# Code ko samjho

class Animal       : — Parent Class banayi.

class Dog(Animal)  : — Dog, Animal ki Child Class hai. Brackets mein 
                       Animal likhne se inheritance hota hai.

eat()                — Parent Class ka method hai.

bark()               — Child Class ka apna method hai.

d.eat()              — Child class ke object se Parent Class ka method 
                       call kiya.

d.bark()             — Child class ka apna method call kiya.

* Main baat: Inheritance ki wajah se Dog class ko eat() method dobara 
             likhne ki zaroorat nahi padi.

=================================================================================

3. Copy karne ke liye table

Sawal                              | Jawab
-----------------------------------|--------------------------------------------
Parent Class kya hai?              | Jis class se doosri class inherit karti hai
Child Class kya hai?               | Jo doosri class se inherit karti hai
Inheritance kaise likhte hain?     | class Dog(Animal):
Animal kaun si class hai?          | Parent Class
Dog kaun si class hai?             | Child Class
d.eat() kya call karta hai?        | Parent Class ka method
d.bark() kya call karta hai?       | Child Class ka method
Inheritance ka fayda kya hai?      | Code dobara likhne ki zaroorat kam hoti hai
-----------------------------------|--------------------------------------------