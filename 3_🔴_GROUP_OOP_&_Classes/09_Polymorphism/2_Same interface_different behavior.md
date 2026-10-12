Same Interface, Different Behavior kya hota hai?

* Iska simple matlab hai: Kaam karne ka tareeka (method call) same hota hai, 
                          lekin usse milne wala result object ke hisaab se 
                          alag hota hai.

====================================================================================

Pehle dono words samjho:
------------------------

# Same Interface: 

1. Same Interface ka matlab
---------------------------
* Alag-alag objects ke liye method call karne ka tareeka same hona.

Example:
-------
dog.sound()
cat.sound()

* Dono mein .sound() likha hai. Yaani dono objects ko sound karwane 
  ke liye hum same naam ka method use kar rahe hain. Yahi Same Interface 
  hai.

------------------------------------------------------------------------------------

# Different Behavior:

2. Different Behavior ka matlab:
--------------------------------

* Same method call karne par alag objects ka alag result dena.

- dog.sound() → Bhau bhau
- cat.sound() → Meow meow

--> Dono mein .sound() call hua, lekin Dog ne bhaukne ki awaaz 
    di aur Cat ne meow ki. Yahi Different Behavior hai.

------------------------------------------------------------------------------------

Ek line mein yaad rakho:
------------------------
- Same Interface     : Method call karne ka tareeka same.
- Different Behavior : Method call karne ka result alag.

====================================================================================

Example dekho
-------------
class Dog:
    def sound(self):
        print("Bhau bhau")

class Cat:
    def sound(self):
        print("Meow meow")

dog = Dog()
cat = Cat()

dog.sound()
cat.sound()

Output:
-------
Bhau bhau
Meow meow

------------------------------------------------------------------------------------

Ab samjho ki kya hua:
---------------------
- Dog ke liye humne dog.sound() call kiya.
- Cat ke liye humne cat.sound() call kiya.
- Dono ko use karne ka tareeka same hai: .sound()        --> Same Interface.
- Lekin Dog ne Bhau bhau aur Cat ne Meow meow print kiya --> Different Behavior.

* Yaani interface same hai (sound()), lekin behavior different hai.

====================================================================================

Iska Polymorphism se kya connection hai?
----------------------------------------
* Same Interface, Different Behavior, Polymorphism ko samajhne ka 
  ek basic idea hai.

* Ye concept Method Overriding se bhi achieve ho sakta hai aur Duck 
  Typing se bhi. Dono examples mein objects ko sound() method se use 
  kar sakte hain, lekin unka behavior alag hota hai.

* Ek line mein yaad rakho: Same Interface, Different Behavior ka matlab 
                           hai — method call karne ka tareeka same, lekin 
                           object ke hisaab se uska behavior alag.