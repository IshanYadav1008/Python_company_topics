* Yaar, Create Context Manager ka matlab hai Python mein apna khud 
  ka context manager banana, jo with ke saath kaam kare.

# Simple example se samjho.

1. Pehle concept samjho:
------------------------
* Python mein hum pehle se aise context manager use karte hain:

with open("data.txt", "w") as file:
    file.write("Hello")

- Yahan Python ka open() humein context manager deta hai.
- Create Context Manager mein hum khud aisa mechanism banayenge, 
  jisse with use kar sakein.

============================================================================

2. Apna Context Manager banao:
------------------------------

class MyContext:
    def __enter__(self):
        print("Kaam shuru")

    def __exit__(self, exc_type, exc_value, traceback):
        print("Kaam khatam")


with MyContext():
    print("Main apna kaam kar raha hoon")

Output:
-------
Kaam shuru
Main apna kaam kar raha hoon
Kaam khatam

============================================================================

3. Code mein kya ho raha hai?

- class MyContext:  — humne apni class banayi.
- __enter__()       — with block shuru hote hi call hota hai.
- __exit__()        — with block khatam hote hi call hota hai.
- with MyContext(): — humne apne context manager ko use kiya.

* Dhyan do: __exit__() ke andar diye gaye exc_type, exc_value aur 
            traceback exception ki information ke liye hote hain.

============================================================================

4. Ek line mein difference:
---------------------------

- Context Manager            : Jo resource ya task ko manage karta hai.
- Create Context Manager     : Apna khud ka context manager banana.
- __enter__() aur __exit__() : Uske setup aur cleanup ko define karne wale 
                               methods.

Abhi tumhara goal            : Is code ko samajhna hai ki with MyContext() 
                               likhne par pehle __enter__(), phir block ka 
                               code aur aakhir mein __exit__() chalta hai.