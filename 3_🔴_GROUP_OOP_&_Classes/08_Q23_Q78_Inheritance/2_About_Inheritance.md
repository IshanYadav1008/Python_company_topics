1. Inheritance kya hai?

* Inheritance ek aisa concept hai jisme ek Child Class, Parent 
  Class ke attributes aur methods ko inherit karke use kar sakti 
  hai.

* Iska sabse bada fayda hai ki humein same code baar-baar likhne 
  ki zaroorat nahi padti.

================================================================================

2. Python mein Inheritance implement kaise karte hain?

CODE:
-----
class Animal:  # Parent Class
    def eat(self):
        print("Animal is eating")


class Dog(Animal):  # Child Class
    def bark(self):
        print("Dog is barking")


d = Dog()
d.eat()
d.bark()

Output:
-------
Animal is eating
Dog is barking

================================================================================

3. Code ko samjho

Step 1: Parent Class banao
--------------------------
class Animal: ek Parent Class hai. Ismein eat() method bana hai.

--------------------------------------------------------------------------------

Step 2: Child Class banao
-------------------------
class Dog(Animal): mein brackets ke andar Animal likhne se Dog, 
                   Animal se inherit karti hai.

--------------------------------------------------------------------------------

Step 3: Object banao
--------------------
d = Dog() se Dog ka object bana.

--------------------------------------------------------------------------------

Step 4: Methods call karo
-------------------------
d.eat() Parent Class ka method call karta hai aur d.bark() Child 
Class ka method.

================================================================================

4. Inheritance ka main fayda

* Inheritance ke bina agar Dog ko eat() method chahiye, toh humein 
  woh method Dog mein bhi likhna pad sakta hai.

* Inheritance ke saath Dog, Animal ka eat() method use kar sakti hai, 
  bina usse dobara likhe.

# Table:

Sawal                              | Jawab
================================================================================
Inheritance kya hai?               | Parent Class ke attributes aur methods 
                                   | inherit karna
--------------------------------------------------------------------------------
Parent Class kya hai?              | Jis class ko doosri class inherit karti hai
--------------------------------------------------------------------------------
Child Class kya hai?               | Jo class Parent Class ko inherit karti hai
--------------------------------------------------------------------------------
Inheritance kaise implement        | Child Class ke naam ke baad brackets mein 
hota hai?                          | Parent Class likhkar
--------------------------------------------------------------------------------
class Dog(Animal) ka matlab?       | Dog, Animal se inherit karti hai
--------------------------------------------------------------------------------
Inheritance ka fayda kya hai?      | Code reuse hota hai, code dobara nahi 
                                   | likhna padta
--------------------------------------------------------------------------------

================================================================================
--------------------------------------------------------------------------------
================================================================================

5. Chhota sa practice question

Is code mein output kya aayega ?
--------------------------------
class Person:
    def introduce(self):
        print("I am a person")


class Student(Person):
    pass


s = Student()
s.introduce()

O/P: I am a person

--------------------------------------------------------------------------------

* Bilkul sahi! ✅ Output hoga: I am a person

Kyun?
-----
. Person Parent Class hai, jisme introduce() method hai.

. Student Child Class hai, jo Person ko inherit karti hai.

. pass ka matlab hai ki abhi Student class ke andar koi extra 
  code nahi likha.

. s = Student() se object bana.

. s.introduce() call karne par Python ko Student mein method 
  nahi mila, toh usne Parent Class Person ka method use kiya.

--------------------------------------------------------------------------------

Sawal                              | Jawab
-----------------------------------|-------------------------------------
Student mein introduce() hai?      | Nahi
Phir bhi s.introduce() chala?      | Haan
Kyun chala?                        | Student ne Person ko inherit kiya hai
pass ka matlab?                    | Filhaal koi extra code nahi