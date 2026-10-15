1. else kya hota hai ?

* else tab execute hota hai jab try block mein koi exception nahi aati.

CODE:
-----
try:
    a = 10 / 2
except ZeroDivisionError:
    print("Error aa gayi!")
else:
    print("Koi error nahi aayi!")

Output: Koi error nahi aayi!

* Agar try mein error aati, toh except chalta aur else nahi chalta.

==============================================================================

2. finally kya hota hai?

* finally block normally har situation mein execute hota hai, chahe 
  exception aaye ya na aaye.

CODE:
-----
try:
    a = 10 / 0
except ZeroDivisionError:
    print("Error aa gayi!")
finally:
    print("Ye hamesha execute hoga!")

Output:
-------
Error aa gayi!
Ye hamesha execute hoga!

- finally ka use aksar files ya doosre resources ko close ya clean up 
  karne ke liye hota hai.

==============================================================================

3. Teeno mein difference kya hai ?

Block	          Kab execute hota hai?
-----------------------------------------------------------------
try	              Risky code execute karta hai
except	          Matching exception aane par
else	          Jab try mein exception nahi aati
finally	          Normally dono cases mein, error aaye ya na aaye
-----------------------------------------------------------------

==============================================================================

4. Ek example mein sab samjho:

CODE:
-----
try:
    print("Try block")
    x = 10 / 2

except ZeroDivisionError:
    print("Except block")

else:
    print("Else block")

finally:
    print("Finally block")

Output:
-------
Try block
Else block
Finally block

- Kyunki division successful hui, isliye except skip hua, else chala 
  aur phir finally chala.

==============================================================================

5. Ab teri baari! 🧠

* Agar code mein 10 / 0 kar dein, toh output kya hoga?

CODE:
-----
try:
    x = 10 / 0
except ZeroDivisionError:
    print("Error")
else:
    print("Success")
finally:
    print("Done")

O/P: Error, Done

Bilkul sahi yaar : except error handle karega, else nahi chalega 
                   kyunki exception aayi, aur finally execute hoga.