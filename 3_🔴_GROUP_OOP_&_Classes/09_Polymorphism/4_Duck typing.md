# Duck Typing kya hoti hai ?

* Duck Typing Python ka ek tareeka hai jisme object ki class dekhne 
  ke bajaye hum dekhte hain ki woh object kya kaam kar sakta hai.

Simple example se samjho.
-------------------------
Socho tumhare paas Dog aur Cat ki classes hain. Dono alag classes 
hain, lekin dono mein sound() method hai.

CODE:
-----
class Dog:
    def sound(self):
        print("Bhau bhau")

class Cat:
    def sound(self):
        print("Meow meow")

animals = [Dog(), Cat()]

for animal in animals:
    animal.sound()

Output:
-------
Bhau bhau
Meow meow

==============================================================================

Ismein Duck Typing kahan hai ?
------------------------------
1. Dog aur Cat alag classes hain.
2. Dono kisi common Parent class ko inherit nahi kar rahi hain.
3. Lekin dono ke paas sound() method hai.
4. Hum bina ye check kiye ki object Dog hai ya Cat, seedha 
   animal.sound() call kar dete hain.
5. Har object apna kaam kar deta hai.

* Yahi Duck Typing hai: Object kis class ka hai, isse zyada important 
                        hai ki woh required kaam kar sakta hai ya nahi.

==============================================================================

# "Duck Typing" naam kahan se aaya ?

Iske peeche ek famous idea hai:
-------------------------------
* "If it walks like a duck and quacks like a duck, treat it like a duck."

* Matlab, agar koi cheez battakh ki tarah chalti hai aur awaaz nikaalti hai, 
  toh use battakh ki tarah treat karo.

* Python mein bhi, agar object ke paas required method hai aur woh use chala 
  sakta hai, toh hum us method ko use kar sakte hain. Uski class ka naam same 
  hona zaroori nahi hai.

==============================================================================

# Method Overriding aur Duck Typing mein farak:

Method Overriding                         | Duck Typing
------------------------------------------|-----------------------------------
Child class, Parent class ka method       | Alag classes ke objects same 
dobara define karti hai.                  | required method provide kar sakte 
                                          | hain.
                                          |
Inheritance hoti hai.                     | Inheritance zaroori nahi hai.
                                          |
Example: Dog(Animal)                      | Example: independent Dog aur Cat 
                                          |          classes


Yaad rakho: Duck Typing mein inheritance hona zaroori nahi hai. Lekin object 
            ke paas woh method ya behavior hona chahiye jise code use kar 
            raha hai.

==============================================================================

Ab tak humne Polymorphism ke do tareeke dekhe hain:

- Method Overriding : Inheritance ke saath alag behavior.
- Duck Typing       : Required method hone par alag classes ke objects 
                      ko same tareeke se use karna.