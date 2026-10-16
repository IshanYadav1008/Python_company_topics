Iska simple matlab hai: apni banayi hui class ko is tarah banana ki 
                        uska object with ke saath use ho sake.

1. Pehle normal class dekho:
----------------------------
class Rahul:
    def hello(self):
        print("Hello!")

r = Rahul()
r.hello()   

Output:
-------
Hello!

- Yahan r.hello() hum khud call kar rahe hain.

==============================================================================

2. Ab class ko context manager banate hain:

CODE:
-----
class Rahul:
    def __enter__(self):
        print("Kaam shuru")

    def __exit__(self, exc_type, exc_value, traceback):
        print("Kaam khatam")

with Rahul():
    print("Main kaam kar raha hoon")

Output:
-------
Kaam shuru
Main kaam kar raha hoon
Kaam khatam

==============================================================================

3. Ye chala kaise ?
-------------------
1. class Rahul: — humne class banayi.

2. __enter__() aur __exit__() — class ke andar special methods define 
   kiye.

3. with Rahul(): — Rahul class ka object banaya aur with mein use kiya.

4. Python ne __enter__() call kiya, isliye Kaam shuru print hua.

5. Phir andar ka code chala, isliye Main kaam kar raha hoon print hua.

6. Block khatam hua, toh Python ne __exit__() call kiya aur Kaam khatam 
   print hua.

Yaad rakhna: Kisi class ko with ke saath use karne ke liye usmein 
             __enter__() aur __exit__() methods define karte hain.

- Isi ko Class Behaving as Context Manager kehte hain.