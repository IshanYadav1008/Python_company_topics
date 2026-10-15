1. Exception Handling kya hoti hai ?

* Sabse pehle samjho ki exception kya hota hai.

* Exception ek aisi error hoti hai jo program run hote waqt 
  aati hai aur program ke normal execution ko rok sakti hai.

Example:
--------
a = 10
b = 0
print(a / b)

Output:
-------
ZeroDivisionError: division by zero

------------------------------------------------------------------------------

- Yahan hum 10 ko 0 se divide kar rahe hain, jo Python mein allowed nahi 
  hai. Isliye exception aati hai.

- Agar hum exception ko handle nahi karte, toh program error ke saath ruk 
  sakta hai.

- Exception Handling ka matlab hai program mein aane wali expected errors 
  ko handle karna, taaki program achhe tareeke se respond kar sake.

- For example, error aane par program crash karne ke bajaye message de 
  sakta hai: "Zero se divide nahi kar sakte!"

==============================================================================

2. try-except kya hota hai ?

* Python mein exception handle karne ke liye hum try-except ka use karte 
  hain.

- try     : Is block mein woh code likhte hain jisme exception aane ki 
            possibility hoti hai.

- except  : Agar try block mein exception aati hai, toh usse handle karne 
            ke liye yeh block execute hota hai.

Syntax:
-------
try:
    # Code jisme error aa sakti hai
    statement
except:
    # Error ko handle karne wala code
    statement

------------------------------------------------------------------------------

Example 1: try-except ka use:
-----------------------------
- Code ko dhyan se dekho.

CODE:
-----
a = 10
b = 0

try:
    print(a / b)

except:
    print("Kuch error aa gayi!")

print("Program continue ho raha hai.")

Output:
-------
Kuch error aa gayi!
Program continue ho raha hai.

------------------------------------------------------------------------------

Step-by-step kya hua ?
----------------------

Step 1: try block chala
Python ne 10 / 0 execute karne ki koshish ki.

Step 2: Exception aayi
Zero se division nahi ho sakta, isliye ZeroDivisionError aayi.

Step 3: except block chala
"Kuch error aa gayi!" print hua.

Step 4: Program aage chala
"Program continue ho raha hai." print hua.

* Dhyan do: try block mein exception aane ke baad us block ki baaki 
            statements skip ho jaati hain. Phir matching except block
            execute hota hai.
        
==============================================================================

3. Specific exception kaise handle karte hain ?

* Python mein sirf except: likhne ke bajaye specific exception handle 
                           karna generally better hota hai. 

Example:
--------
try:
    a = 10 / 0

except ZeroDivisionError:
    print("Zero se divide nahi kar sakte!")

Output:
-------
Zero se divide nahi kar sakte!

- Yahan ZeroDivisionError us exception ka naam hai jo zero se division 
  karne par aati hai.

------------------------------------------------------------------------------

# Kuch common exceptions:

Exception	            Kab aati hai?
-------------------------------------------------------------------------
ZeroDivisionError	    Zero se divide karne par
ValueError	            Value ka type sahi ho, par value invalid ho
TypeError	            Galat type ke objects par operation karne par
NameError	            Aise variable ka use karne par jo define nahi hai
FileNotFoundError	    Jab required file nahi milti
-------------------------------------------------------------------------

Ek aur example:
---------------
try:
    age = int("hello")

except ValueError:
    print("Please valid number enter karo!")

Output:
-------
Please valid number enter karo!

- Kyunki "hello" ko integer mein convert nahi kar sakte.

==============================================================================

4. Ek try ke saath multiple except:

* Ek try block mein alag-alag types ki exceptions aa sakti hain. 
  Unhe alag handle kar sakte hain.

CODE:
-----
try:
    a = int(input("Enter a number: "))
    print(100 / a)

except ValueError:
    print("Please number enter karo!")

except ZeroDivisionError:
    print("Zero allowed nahi hai!")

- Agar user abc enter kare, toh ValueError handle hogi.
- Agar user 0 enter kare, toh ZeroDivisionError handle hogi.
- Agar user 5 enter kare, toh output 20.0 hoga.

==============================================================================

5. Ab tumhari practice! 🧠

Question 1: Is code ka output kya hoga?

CODE:
-----
try:
    print(10 / 0)
except ZeroDivisionError:
    print("Error handled!")

print("Hello Python")

ANS) Error handled! phir Hello Python print hoga.

* Bilkul sahi! : Pehle division par exception aayegi, except use handle 
                 karega aur phir program Hello Python print karega.

Abhi ke liye bas 3 baatein yaad rakho:
--------------------------------------
1. try mein risky code likhte hain.
2. except mein exception handle karte hain.
3. Exception handle hone ke baad program aage continue kar sakta hai.

==============================================================================
------------------------------------------------------------------------------
==============================================================================

**IMP**
Yaar, bas ek baat samajh. Exception ka matlab error handle karna nahi hota.

Exception = program ke normal flow mein aane wali rukawat, jise Python ek 
            special mechanism se report karta hai.

Example:
--------
print("Hello")
print(10 / 0)
print("Bye")

- "Hello" print hoga.
- 10 / 0 par Python ZeroDivisionError exception raise karega.
- "Bye" print nahi hoga, kyunki exception ne normal flow rok diya.

Ab ye 3 cheezein alag hain:
---------------------------
- Exception: ZeroDivisionError — Python jis situation ko report 
                                 kar raha hai.

- Exception handling  : Us situation ke aane par kya karna hai.
- Custom exception    : Apne program ki kisi specific situation 
                        ke liye banayi hui exception, jaise 
                        AgeError.

* Ek line mein: Exception woh cheez hai jo normal execution ko 
                interrupt karti hai; handling us interruption 
                ko manage karne ka tareeka hai.