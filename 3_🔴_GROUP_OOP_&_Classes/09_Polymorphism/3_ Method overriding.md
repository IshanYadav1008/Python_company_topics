* Method Overriding ko shuru se dobara padhne ki zaroorat nahi hai. 
  Hum ise pehle hi padh chuke hain.

* Bas Polymorphism ke context mein iska connection yaad kar lo:

--> Method Overriding : Child class, Parent class ke method ko apne hisaab 
                        se dobara define karti hai.

--> Polymorphism      : Same method call se alag objects ka alag behavior 
                        mil sakta hai.

--> Connection        : Method Overriding, Polymorphism achieve karne ka 
                        ek tareeka hai.

===================================================================================

# Dono examples compare karo:

1. Inheritance mein Method Overriding

class Animal:
    def sound(self):
        print("Animal sound")

class Dog(Animal):
    def sound(self):
        print("Bhau bhau")

--> Yahan Dog, Animal ko inherit karta hai aur apna sound() method define 
    karta hai. Ye Method Overriding hai.

===================================================================================

2. Polymorphism ke example mein:

animals = [Animal(), Dog()]

for animal in animals:
    animal.sound()

Output:
-------
Animal sound
Bhau bhau

--> Yahan humne same method call karke dono objects ka alag behavior 
    dekha. Ye Polymorphism hai, jo yahan Method Overriding ki madad 
    se achieve hua.

Yaad rakho:
-----------
- Method Overriding = method ko dobara define karna.
- Polymorphism      = same method call se alag behavior milna.