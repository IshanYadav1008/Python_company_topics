1. Agar except: pass bad practice hai, toh Python mein pass hai hi kyun?
------------------------------------------------------------------------

* Sabse pehle ek correction:

. pass khud bad practice nahi hai.
. pass Python ka perfectly valid keyword hai.

Bad practice specific situation mein hai:
-----------------------------------------
try:
    x = 10 / 0

except:
    pass

* Yahan problem "pass" nahi, balki error ko silently ignore kar dena hai.

-----------------------------------------------------------------------------------

pass actually karta kya hai?
----------------------------

* Python mein kuch places par syntax ke liye code block 
  hona zaroori hota hai.

Example:
--------
if age > 18:
    pass

. Yahan hum keh rahe hain: "Agar age 18 se greater hai, abhi kuch nahi karna."
. Ye valid situation ho sakti hai.

-----------------------------------------------------------------------------------

# Ek aur example

* Maan lo tum abhi function bana rahe ho, lekin uska code baad mein likhoge:

def calculate_salary():
    pass

Agar pass nahi hota aur tum likhte:
-----------------------------------
=> def calculate_salary():   // toh Python ko indentation ke andar kuch chahiye.

* pass basically bolta hai: "Yahan intentionally kuch nahi karna."

-----------------------------------------------------------------------------------

# Toh exception wale example mein problem kya hai?

try:
    x = 10 / 0

except:
    pass

Iska meaning hai:
-----------------
Error hua
   ↓
except ne error pakda
   ↓
kuch bhi mat karo
   ↓
aage badho

. Problem ye hai ki tumhe pata hi nahi chalega ki error hua.

<--------------------------------------------------------------->

* Agar production application mein koi important problem aa 
  rahi ho aur tum:

except:
    pass    // kar do, toh problem chup jaayegi.

Better:
-------
try:
    x = 10 / 0

except ZeroDivisionError:
    print("Cannot divide by zero")

. Ab error ko properly handle kiya.

-----------------------------------------------------------------------------------

So remember:
------------
=> pass         // ❌ nahi

=> except: pass // ❌ problematic

Lekin:
------
if condition:
    pass

ya:
---

def future_function():
    pass

* bilkul valid use cases hain.

===================================================================================

2. ValueError humne banaya hai ya Python mein pehle se hai?
-----------------------------------------------------------

* ValueError Python mein pehle se defined hai, Humne nahi banaya.

* Python ke paas bahut saare built-in exception types hain.

jaise:
------
ValueError
TypeError
ZeroDivisionError
IndexError
KeyError
FileNotFoundError
NameError             // etc.

Example:
--------
int("hello")    // Python khud ValueError raise kar sakta hai.

-----------------------------------------------------------------------------------

# Lekin tumhara actual doubt bahut interesting hai:

Tum keh rahe ho: "Agar ValueError Python ka hai, toh humne raise 
                  ValueError(...) karke error kaise raise kar diya? 
                  Phir toh Python hi raise kar raha hai?"

. Yahan "error type" aur "error raise karna" alag concepts hain.

-----------------------------------------------------------------------------------

# ValueError ko ek ready-made category samjho:

* Python ne pehle se ek category/type bana rakhi hai:

=> ValueError

Jaise school mein categories ho sakti hain:
-------------------------------------------
Student
Teacher
Principal

. Tumne categories nahi banayi. Categories already exist karti hain.

. Lekin tum decide kar sakte ho: "Is particular situation ko ValueError 
                                  category mein daalna hai."

-----------------------------------------------------------------------------------

Example
-------
age = -5

if age < 0:
    raise ValueError("Age cannot be negative")

* Yahan humne ValueError create nahi kiya.

* Humne Python ko bola: "Python, is situation mein ValueError 
                         raise karo aur ye message do."

So:
---
ValueError
    ↑
Python mein pehle se defined exception type

Aur:
----
raise ValueError("Age cannot be negative")

. ka meaning: "Abhi isi point par ek ValueError exception 
               raise karo."

-----------------------------------------------------------------------------------

# Lekin Python ko kaise pata chala ki -5 invalid hai?

* Python ko pata nahi tha.
* Ye sabse important point hai.

Python ke liye:
---------------
age = -5           // bilkul valid hai.

. Python ko negative number se koi problem nahi.

Ye valid hai:
-------------
age = -5
print(age)

Output: -5

. Python khud ValueError nahi dega.

-----------------------------------------------------------------------------------

# Humne business rule banaya

* Humne decide kiya: "Hamare program mein age negative nahi honi chahiye."

Isliye:
-------
if age < 0:
    raise ValueError("Age cannot be negative")

Yahan:
------
Python ka rule         : -5 ek valid integer hai ✅

Hamare program ka rule : Age -5 nahi ho sakti ❌

* Toh humne condition aur decision banaya, lekin exception type 
  ValueError Python se liya.

===================================================================================

*** Ye difference bahut important hai ***

Case 1 — Python khud exception raise karta hai:

=> x = 10 / 0

Python dekhta hai:
------------------
10 / 0
   ↓
mathematical operation allowed nahi
   ↓
ZeroDivisionError

* Yahan Python ne automatically exception raise ki.

-----------------------------------------------------------------------------------

Case 2 — Hum manually exception raise karte hain:

=> age = -5

if age < 0:
    raise ValueError("Age cannot be negative")

* Yahan Python ko negative integer se problem nahi thi.

* Humne khud decide kiya ki ye situation hamare program mein invalid hai.

* Phir Python ke existing ValueError type ko use karke exception raise kar di.

-----------------------------------------------------------------------------------

# raise ka role

Ye line:
--------
=> raise ValueError("Age cannot be negative")

basically:
----------
ValueError type choose karo
        ↓
message attach karo
        ↓
exception raise karo
        ↓
normal execution stop/interrupt karo

-----------------------------------------------------------------------------------

# Aur except usko pakad sakta hai

Ab dekho:
---------
try:
    age = -5

    if age < 0:
        raise ValueError("Age cannot be negative")

except ValueError as e:
    print(e)

Output: Age cannot be negative

Flow:
-----
age = -5
   ↓
age < 0 ?
   ↓
True
   ↓
raise ValueError(...)
   ↓
exception generate
   ↓
except ValueError
   ↓
print(e)

===================================================================================

# Ek analogy jo yaad rahegi

* Socho Python ne tumhe different types ke alarm already diye hue hain:

ValueError           → value related problem
TypeError            → type related problem
ZeroDivisionError    → zero se division
IndexError           → invalid index

* Tumhare paas ye alarms already available hain.

* Ab tum apne program mein decide karte ho: "Agar age negative ho, toh 
                                             ValueError wala alarm baja 
                                             do."

=> raise ValueError("Age cannot be negative")

. Tumne alarm banaya nahi, Tumne existing alarm ko trigger kiya.

-----------------------------------------------------------------------------------

*** Final difference — ye yaad rakhna ***

ValueError
    ↓
Python mein pehle se defined exception TYPE

raise ValueError(...)
↓
Hum us existing exception type ko
manually RAISE/TRIGGER kar rahe hain.

<----------------------------------------------------->

Aur:
----

x = 10 / 0
↓
Python khud automatically ZeroDivisionError raise karta hai.

===================================================================================

Ek line mein:
-------------
Exception type Python provide kar sakta hai, lekin kis situation mein us 
exception ko manually raise karna hai, ye programmer decide kar sakta hai.