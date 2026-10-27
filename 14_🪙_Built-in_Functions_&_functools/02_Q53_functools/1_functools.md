# functools in Python:

1. Sabse pehle: functools kya hai ?
-----------------------------------

* Python mein kuch functions aise hote hain jo doosre functions ke saath kaam 
  karte hain. Jaise kisi function ko baar-baar chalne se bachana, function 
  mein kuch arguments pehle se set karna, ya function ko wrap karna.

- In kaamon ke liye Python ek built-in module deta hai, jiska naam hai functools.

Simple words mein: functools Python ki ek built-in library hai jisme aise tools 
                   hain jo functions ko manage karne aur unke behavior ko 
                   customize karne mein help karte hain.

Isko use karne ke liye:
-----------------------
=> import functools

Ya kisi specific tool ko import kar sakte ho:
---------------------------------------------
=> from functools import lru_cache

=================================================================================

2. Real example se samjho:
--------------------------

* Maan lo tum ek application bana rahe ho jo baar-baar kisi user ka data 
  calculate karta hai. Ek function same input ke liye same result deta 
  hai, lekin calculation expensive hai.

- Har baar wahi calculation dobara karne ke bajaye, tum result ko cache 
  kar sakte ho.

  Yahan functools ka @lru_cache kaam aata hai.

Example 1: @lru_cache — result ko yaad rakhna:
----------------------------------------------
from functools import lru_cache

@lru_cache(maxsize=128)
def square(n):
    print("Calculating...")
    return n * n

print(square(5))
print(square(5))
print(square(5))

Output:
-------
Calculating...
25
25
25

- Pehli baar square(5) call hua, calculation hui. Agli baar same argument 
  5 diya, toh cached result mil gaya aur function ke andar ka print() 
  dobara nahi chala.

- Real project mein : expensive calculations ya baar-baar use hone wale 
                      results ko cache karne mein useful ho sakta hai.

- Dhyan rahe        : caching tab useful hoti hai jab same inputs par 
                      result same rehna chahiye. Har function ko cache 
                      karna sahi nahi hota.

=================================================================================

3. partial() — function mein kuch values pehle se set karna:
------------------------------------------------------------

* Maan lo tum ek function banate ho jo discount calculate karta hai.

CODE:
-----
from functools import partial

def calculate_price(price, discount):
    return price - (price * discount / 100)

student_price = partial(calculate_price, discount=20)

print(student_price(1000))
print(student_price(500))

Output:
-------
800.0
400.0

- Yahan partial() ne discount=20 pehle se set kar diya. Ab tum 
  student_price() ko sirf price de sakte ho.

- Real project mein: jab same function ko baar-baar ek hi 
  configuration ya argument ke saath call karna ho, tab 
  useful hai.

=================================================================================

4. @wraps — function ki original identity bachana:
--------------------------------------------------

* Kabhi-kabhi tum ek function ke around doosra function lagate ho, 
  jaise logging ya timing ke liye. Isse original function ka naam 
  aur documentation wrapper ke naam se replace ho sakte hain.

- functools.wraps is problem ko avoid karne mein help karta hai.

CODE:
-----
from functools import wraps

def logger(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Function is running")
        return func(*args, **kwargs)
    return wrapper

@logger
def greet():
    """Greets the user."""
    print("Hello!")

print(greet.__name__)

Output:
-------
greet

- @wraps(func) original function ka naam aur metadata preserve karne mein 
  help karta hai.

- Real project mein: decorators likhte waqt, jaise logging, authentication 
                     ya timing wrappers mein, ye kaafi useful hai.

=================================================================================

5. reduce() — values ko combine karte jaana:
--------------------------------------------

* reduce() list ki values ko step-by-step combine karke ek final result 
  nikalta hai.

CODE:
-----
from functools import reduce

numbers = [1, 2, 3, 4]
result  = reduce(lambda a, b: a + b, numbers)
print(result)

Output:
10


- Calculation: 1 + 2 = 3, phir 3 + 3 = 6, phir 6 + 4 = 10.

- Lekin simple total nikalna ho, toh sum(numbers) zyada readable hai. 
  reduce() tab samajhna useful hai jab tum existing code mein dekho 
  ya values ko kisi custom logic se combine karna ho.

=================================================================================

6. Internship ke liye kis order mein seekhna hai ?
--------------------------------------------------

1. @lru_cache
-------------
Repeated calculations aur caching samjho.
Pehle seekho

2. partial()
-----------
Reusable functions aur fixed arguments samjho.

3. @wraps
---------
Decorators aur function wrapping ke saath seekho.

4. reduce()
-----------
Iska behavior samjho, lekin simple sum ke liye sum() prefer karo.

* Ek important baat: functools ka har tool har project mein use nahi hota. 
                     Tumhe pehle inka purpose aur basic syntax samajhna 
                     hai. Phir jab codebase mein ye dikhein, tab confidently 
                     samajh paoge.

=================================================================================
---------------------------------------------------------------------------------
=================================================================================

Doubt:1
-------
# muje es code mai

from functools import partial

def calculate_price(price, discount):
    return price - (price * discount / 100)

student_price = partial(calculate_price, discount=20)

print(student_price(1000))
print(student_price(500))

- ye smj nhi aaya ki hum jab aise arguments de rhe hai
print(student_price(1000)) 

- toh ye yaha calculate_price mai kaise jaa rha hai, 
student_price = partial(calculate_price, discount=20)

=================================================================================

Part 1: partial() kaise kaam karta hai ?
--------------------------------------

Tumhara code:
-------------
from functools import partial

def calculate_price(price, discount):
    return price - (price * discount / 100)

student_price = partial(calculate_price, discount=20)

print(student_price(1000))
print(student_price(500))

<----------------------------------------------------------->

Step 1: Pehle calculate_price function bana
-------------------------------------------
def calculate_price(price, discount):
    return price - (price * discount / 100)

* Abhi humne sirf function define kiya hai. Function ke andar 
  ka code abhi execute nahi hua.

Ye function do arguments maangta hai:
-------------------------------------
- price    — product ki original price.
- discount — discount percentage.

* Jaise calculate_price(1000, 20) ka result 800.0 hoga.

<----------------------------------------------------------->

Step 2: Ab ye line dekho
------------------------
student_price = partial(calculate_price, discount=20)

Is line ka matlab hai: Ek naya callable banao jo calculate_price 
                       ko call karega aur discount=20 pehle se 
                       set rakhega.

- Yaani ab har baar discount dene ki zaroorat nahi hai. Sirf price 
  dena hoga.

Is line ke baad
---------------
=> student_price

Original function : calculate_price
Fixed argument    : discount = 20

Conceptually, ise aise samajh sakte ho:
---------------------------------------
student_price(price)
# internally:
calculate_price(price, discount=20)

* Dhyan do: partial() yahan calculate_price ko turant execute nahi 
            karta. Ye ek naya callable taiyar karta hai, jise baad 
            mein call kar sakte ho.

<----------------------------------------------------------->

Step 3: Ab print(student_price(1000)) ka dry run:
-------------------------------------------------

* Jab Python ye line chalata hai:

=> print(student_price(1000))

Toh ye steps hote hain:
-----------------------
1. Call hota hai
----------------
=> student_price(1000)

2. Arguments combine hote hain
------------------------------
=> price    = 1000
=> discount = 20 (pehle se fixed)

3. Original function execute hota hai:
--------------------------------------
=> calculate_price(1000, discount=20)


Calculation hoti hai
---------------------
1000 - (1000 * 20 / 100)
1000 - 200 = 800.0

<----------------------------------------------------------->

Step 4: Ab second call ka dry run
---------------------------------
=> print(student_price(500))

- Is baar student_price ko 500 milta hai. Discount ab bhi 20 hai.

calculate_price(500, discount=20)

# 500 - (500 * 20 / 100)
# 500 - 100
# 400.0

o/p: 400.0

---------------------------------------------------------------------------------

Ab sabse important baat:
------------------------
Tumne poochha tha ki student_price(1000) se argument calculate_price() 
mein kaise jaata hai.

Kyunki partial() ne calculate_price ko reference ke roop mein lekar ek 
callable banaya tha, jisme discount=20 fix tha. Jab tum student_price(1000) 
call karte ho, toh partial tumhare diye hue 1000 aur pehle se fixed 
discount=20 ko original function tak pahucha deta hai.

Compare karo:
-------------
# Without partial
calculate_price(1000, 20)

# With partial
student_price(1000)

Dono ka result same hai: 800.0.

=================================================================================
---------------------------------------------------------------------------------
=================================================================================

Doubt:2
-------

muje es code ka dry run abhi bhi smj nhi aaya ki isme kya or kaise ho 
rha hai or kyu ho raha hai ??

CODE:
-----
from functools import wraps

def logger(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Function is running")
        return func(*args, **kwargs)
    return wrapper

@logger
def greet():
    """Greets the user."""
    print("Hello!")

print(greet.__name__)

=================================================================================

* Bilkul bhai! Ab hum dono examples ko ek hi concept ke through, line-by-line 
  dry run karenge. Tumhare pehle wale doubt ko bhi cover karenge: apple() 
  aur greet() function ke bahar hain, phir bhi wrapper kaise chalta hai ? 

Hum 3 cheezein samjhenge:
-------------------------
1. @my_decorator / @logger ke baad function ke saath kya hota hai.

2. @wraps(func) kyun likhte hain, jab apple wale example mein sirf 
   wrapper() tha.

3. greet.__name__ kya hai aur iska use kyun hota hai.

=================================================================================

Part 1 — Apple wala example, complete dry run:
----------------------------------------------

Ye code dekho:
--------------
def my_decorator(func):
    def wrapper():
        print("Basket opened")
        func()
        print("Basket closed")
    return wrapper

@my_decorator
def apple():
    print("Apple")

apple()

---------------------------------------------------------------------------------

Step 1: Python pehle decorator banata hai
-----------------------------------------
=> def my_decorator(func):

* Python my_decorator naam ka function bana deta hai. Abhi iske andar ki 
  lines execute nahi hoti.

---------------------------------------------------------------------------------

Step 2: Python original apple function banata hai
-------------------------------------------------
def apple():
    print("Apple")

- Ab apple naam original function ko refer karta hai.

* Is waqt agar hum original function ko call karein, toh:
=> apple()

output hoga:
------------
Apple

- Lekin abhi humne apple() call nahi kiya. Python bas function 
  define kar raha hai.

---------------------------------------------------------------------------------

Step 3: Ab @my_decorator aata hai
---------------------------------
@my_decorator
def apple():
    print("Apple")

* Python isko aise treat karta hai:

def apple():
    print("Apple")

apple = my_decorator(apple)

- Ab dhyan dena : my_decorator(apple) mein jo apple diya hai, woh original 
                  apple function hai.

Decorator ke andar:
-------------------
=> def my_decorator(func):  // toh func ko original apple function milta hai.

Yaani:
------
- func    → original apple function
- wrapper → ek naya function jo extra kaam karega

---------------------------------------------------------------------------------

Step 4: return wrapper ke baad
------------------------------

=> return wrapper    // Ye wrapper function ko return karta hai. Phir 
                        assignment complete hota hai:

=> apple = wrapper

* Ab apple naam original function ko directly refer nahi karta. Ab woh 
  wrapper ko refer karta hai.

* Lekin original function gayab nahi hua! func ke through wrapper ke 
  paas uska reference abhi bhi hai.

---------------------------------------------------------------------------------

Step 5: Ab function ke bahar apple() likha hai
----------------------------------------------

=> apple()

* Tumhara pehla doubt yahi tha ki ye toh function ke bahar hai.

* Haan, bahar hai! Lekin Python dekhta hai ki apple ab kis 
  function ko refer kar raha hai.

Abhi:
-----
=> apple = wrapper

Isliye:
-------
apple()

ka matlab hai:
--------------
wrapper()

<------------------------------------------------------>

Ab wrapper ki lines ek-ek karke chalengi:
-----------------------------------------
print("Basket opened")

Output:
-------
Basket opened

<------------------------------------------------------>

Phir:
-----
func()

- func original apple function ko refer karta hai, isliye 
  "Apple" print hota hai.

Phir wrapper mein wapas aakar:
------------------------------
print("Basket closed")

Output:
-------
Basket closed

Final output:
-------------
Basket opened
Apple
Basket closed

- Apple example ka main point: wrapper() ek naya function hai. return 
  wrapper usko wapas deta hai, aur apple = wrapper ke baad apple() 
  usi wrapper ko chalata hai.

=================================================================================

Part 2 — Ab functools.wraps wala example
----------------------------------------

* Pehle complete code ko sahi format mein dekh lo:

CODE
----
from functools import wraps

def logger(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Function is running")
        return func(*args, **kwargs)
    return wrapper

@logger
def greet():
    """Greets the user."""
    print("Hello!")

print(greet.__name__)
greet()

Iska output hai:
----------------
greet
Function is running
Hello!


- Ab har line ka matlab samajhte hain.

---------------------------------------------------------------------------------

Step 1: from functools import wraps
-----------------------------------
=> from functools import wraps

- Python ki built-in library functools se hum wraps naam ka tool la 
  rahe hain.

- Ye tool decorator ke andar original function ki information, jaise 
  uska naam aur docstring, wrapper mein preserve karne mein help karta 
  hai.

---------------------------------------------------------------------------------

Step 2: logger function banta hai
---------------------------------
=> def logger(func):

* Ye apple example ke my_decorator(func) jaisa hi hai.

- logger decorator ka naam hai.
- func original function ko receive karega.

* Abhi logger ke andar ka code execute nahi hua.

---------------------------------------------------------------------------------

Step 3: @logger ke neeche greet function banta hai
--------------------------------------------------
@logger
def greet():
    """Greets the user."""
    print("Hello!")

* Python isko conceptually aise treat karta hai:

def greet():
    """Greets the user."""
    print("Hello!")

greet = logger(greet)

* Ab original greet function logger ke func parameter mein 
  chala jaata hai.

* Bilkul apple example ki tarah!

---------------------------------------------------------------------------------

Step 4: Ab is line ko samjho — @wraps(func)
-------------------------------------------
@wraps(func)
def wrapper(*args, **kwargs):

Yahan do alag decorators hain:
------------------------------
- @logger      — greet function ke bahar laga hai.
- @wraps(func) — wrapper function ke bahar laga hai.

* @wraps(func) ka matlab hai ki wrapper ko original func ki pehchaan 
  aur documentation preserve karne ke liye set up karo.

Isko aise samajh sakte ho:
--------------------------
- Original function : greet
- Naya function     : wrapper
- @wraps(func)      : wrapper ko original function ki metadata 
                      copy/preserve karne mein madad karta hai.

* Agar @wraps(func) nahi lagate, toh decorated function ka __name__ aam 
  taur par wrapper hota. @wraps(func) ke saath uska naam greet preserve 
  hota hai.

* Apple example mein humne @wraps use nahi kiya, kyunki hum sirf decorator 
  ka basic kaam samajh rahe the. Lekin real projects mein @wraps useful 
  hota hai, kyunki functions ka naam aur documentation sahi rakhna 
  important hota hai.

---------------------------------------------------------------------------------

Step 5: wrapper(*args, **kwargs) kya hai ?
------------------------------------------

def wrapper(*args, **kwargs):
    print("Function is running")
    return func(*args, **kwargs)

* Ye apple wale wrapper() jaisa hi hai, bas thoda flexible hai.

- *args function ko positional arguments lene deta hai.
- **kwargs function ko named arguments lene deta hai.

* Abhi greet() koi argument nahi leta, isliye ye dono empty rehte 
  hain.

<--------------------------------------------------------------->

Jab wrapper call hota hai:
--------------------------
1. "Function is running" print hota hai.
2. func(*args, **kwargs) original greet() ko call karta hai.
3. Original function "Hello!" print karta hai.

- return original function ka result caller ko wapas deta hai. 
  Is example mein greet() kuch return nahi karta, isliye result 
  None hota hai.

---------------------------------------------------------------------------------

Step 6: return wrapper
----------------------

=> return wrapper

- Bilkul apple example ki tarah, logger wrapper ko return karta hai.

Iske baad:
----------
greet = wrapper

- Yaani greet naam ab wrapper ko refer karta hai. Original greet 
  function ka reference func ke through available rehta hai.

=================================================================================

Part 3 — Sabse important: greet.__name__ kya hai ?
--------------------------------------------------

Ye line dekho:
--------------
print(greet.__name__)

Isko 3 parts mein samjho.
-------------------------

1. greet
--------
* Ye function ka naam hai jiske through hum function ko refer 
  kar rahe hain.

2. __name__
-----------
* Ye Python mein function ka naam batane wala special attribute 
  hai.

Example:
--------
def mango():
    print("Mango")

print(mango.__name__)

Output:
-------
mango

- Dhyan do : yahan mango() nahi likha. Isliye function execute nahi 
             hota; sirf uska naam print hota hai.

3. print(greet.__name__)
------------------------
- Iska matlab hai: "greet function ka naam batao aur print karo."

- Is line se wrapper() execute nahi hota.

---------------------------------------------------------------------------------

Q) @wraps(func) lagane se kya farq padta hai?

Dono cases compare karo.


* Kya @wraps(func) use kiya hai   ? Haan, @wraps(func) laga hai.

* print(greet.__name__) ka output ? greet, Original function ka 
                                    naam preserve hua.

---------------------------------------------------------------------------------

Part 4 — Poore program ka final dry run
---------------------------------------

* Ab program ko upar se neeche tak dekho.

1. Python logger function define karta hai.

2. Python original greet function define karta hai.

3. @logger ki wajah se greet = logger(greet) hota hai.

4. Logger, wrapper return karta hai. Ab greet naam wrapper ko 
   refer karta hai.

5. @wraps(func) original function ka naam preserve karta hai, 
   isliye greet.__name__ ka output greet aata hai.

6. print(greet.__name__) sirf naam print karta hai; wrapper 
   call nahi hota.

7. Phir greet() call hota hai, jo wrapper chalata hai.

8. Wrapper "Function is running" print karta hai, phir original 
   function ko call karta hai, jo "Hello!" print karta hai.

Final output:
-------------
greet
Function is running
Hello!

---------------------------------------------------------------------------------

Live project mein ye kyun useful hai?
-------------------------------------
Maan lo tum ek logger decorator bana rahe ho jo har function ke chalne par 
log print karta hai. Agar @wraps(func) nahi lagaoge, toh debugging ke waqt 
decorated function ka naam wrapper dikh sakta hai. @wraps(func) se original 
naam aur documentation preserve rehte hain, jisse debugging aur tools kaam 
karte waqt function ko pehchanna aasaan hota hai.

Bas dono concepts alag rakhna:
------------------------------
- @logger function ke execution mein extra behavior add karta hai.
- @wraps(func) original function ki pehchaan preserve karta hai.
- greet.__name__ function ka naam batata hai.
- greet() function ko execute karta hai.

=================================================================================
---------------------------------------------------------------------------------
=================================================================================

Doubt:
------
return wrapper se greet naam automatically wrapper nahi ban jaata. 
Ye sirf wrapper function ko return karta hai.

---------------------------------------------------------------------------------

Case 1: Normal decorator — @wraps ke bin
----------------------------------------
def logger(func):
    def wrapper():
        func()
    return wrapper

@logger
def greet():
    print("Hello!")

print(greet.__name__)

Output:
-------
wrapper

* Kyun? greet = logger(greet) hota hai. logger wrapper return karta hai, 
  toh greet ab wrapper ko refer karta hai. Lekin wrapper ka apna naam 
  abhi bhi wrapper hai.

---------------------------------------------------------------------------------

Case 2: @wraps(func) ke saath
-----------------------------
from functools import wraps

def logger(func):
    @wraps(func)
    def wrapper():
        func()
    return wrapper

@logger
def greet():
    print("Hello!")

print(greet.__name__)

Output:
-------
greet

---------------------------------------------------------------------------------

# Toh extra kaam kya kiya ?

Code	                  Kaam
--------------------------------------------------------------------------
return wrapper	        Wrapper function return kiya
--------------------------------------------------------------------------
greet = logger(greet)	  greet naam ko returned wrapper se associate kiya
--------------------------------------------------------------------------
@wraps(func)	          Wrapper ki metadata mein original function ka naam, 
                        docstring etc. preserve kiye

* Ek line mein: return wrapper batata hai kaunsa function return karna 
                hai; @wraps(func) batata hai us wrapper ko original 
                function ki pehchaan bhi deni hai.

* Dono alag kaam hain. @wraps(func) ke bina bhi decorator chalega, bas 
  function ki metadata wrapper wali ho sakti hai.