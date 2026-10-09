1. Instance Attribute

* Instance attribute ki value har object ke liye alag ho sakti 
  hai.

* Usually ise __init__() ke andar self ke saath define karte hain.

CODE:
-----
class Student:
    def __init__(self, name, age):   // Yahan name aur age instance 
        self.name = name                attributes hain.
        self.age = age

s1 = Student("Rahul", 20)
s2 = Student("Aman", 22)

print(s1.name)  # Rahul
print(s2.name)  # Aman

s1.name → Rahul
s2.name → Aman

--> Dono objects ki values alag hain.

=========================================================================

2. Class Attribute

* Class attribute class ke andar directly define hota 
  hai, __init__() ke bahar.

* Iski value generally sabhi objects ke liye common 
  hoti hai.

CODE:
-----
class Student:
    school = "ABC School"   # Class Attribute

    def __init__(self, name):
        self.name = name    # Instance Attribute

s1 = Student("Rahul")
s2 = Student("Aman")

print(s1.name)    # Rahul
print(s2.name)    # Aman

print(s1.school)  # ABC School
print(s2.school)  # ABC School

<--------------------------------------------------->

Yahan:
------
name   → Instance Attribute
school → Class Attribute

=========================================================================

# Easy Difference

| Instance Attribute                    | Class Attribute                         |
| ------------------------------------- | --------------------------------------- |
| Object-specific hota hai              | Class-specific hota hai                 |
| Har object ki value alag ho sakti hai | Generally sab objects ke liye same      |
| `self` ke saath define hota hai       | Class ke andar directly define hota hai |
| `self.name`                           | `Student.school`                        |

=========================================================================

Ek line mein yaad rakho 🧠
--------------------------
Instance Attribute = "Har object ka apna data"
Class Attribute    = "Puri class ka common data"

Example:
--------
class Car:
    wheels = 4                 # Class Attribute

    def __init__(self, color):
        self.color = color     # Instance Attribute

* Yahan 4 wheels sab cars ke common hain, lekin color har 
  car ka alag ho sakta hai.