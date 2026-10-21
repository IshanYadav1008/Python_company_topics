# Python Decorators — Zero se Deep Level tak:

* Is baar bilkul starting se padhenge, jaise tum pehli baar decorator 
  dekh rahe ho. Pehle samjhenge ki decorator hai kya, dikhta kaisa hai 
  aur real life mein kyun use hota hai. Phir tumhare code ki har line 
  ka execution samjhenge, including return wrapper, func, aur 
  hello = my_decorator(hello).

Sabse pehle ek rule : hum ek concept samjhenge, phir usi par based agla 
                      concept seekhenge. Bina foundation ke aage nahi 
                      badhenge.

=================================================================================

1. Decorator hota kya hai ?
---------------------------

* Python mein decorator ek function hota hai jo doosre function ko input 
  mein lekar uske behavior mein extra functionality add kar sakta hai.

Isko simple language mein samjho:
---------------------------------
* Maan lo tumne ek function banaya hai jo order place karta hai.

def place_order():
    print("Order placed")

Ab tum chahte ho ki jab bhi order place ho:
-------------------------------------------
1. Pehle "Order started" print ho.
2. Phir order place ho.
3. Aakhir mein "Order completed" print ho.

- Tum original function ko change kar sakte ho. Lekin maan lo tumhare 
  paas 50 functions hain aur sabke liye logging ka same code chahiye.

- Har function mein baar-baar wahi code likhne ke bajay tum ek decorator 
  bana sakte ho jo ye extra kaam sambhale.

---------------------------------------------------------------------------------

Original function
Apna actual kaam karta hai
       |
       |
Decorator
Extra behavior add karta hai
       |
       |
Decorated function
Extra kaam + original kaam

- Important: Decorator ka matlab sirf wrapper nahi hai. Decorator woh function 
             hai jo doosre function ko decorate karta hai. wrapper uske andar 
             banaya jaane wala ek common technique hai.

=================================================================================

2. Sabse pehle Python ke 3 basic rules:
---------------------------------------

* Decorator samajhne ke liye bas ye teen cheezein clear honi chahiye.

Rule 1: def function banata hai:
--------------------------------
def hello():
    print("Hello!")

- Is code ko execute karne par Python hello naam ka function banata hai. 
  Abhi "Hello!" print nahi hota.

---------------------------------------------------------------------------------

Rule 2: () function ko chalata hai:
----------------------------------
hello()

Output:
-------
Hello!

---------------------------------------------------------------------------------

Rule 3: Function ko doosre function mein bhej sakte hain
--------------------------------------------------------
def hello():
    print("Hello!")

def run(func):
    func()

run(hello)

Output:
-------
Hello!

---------------------------------------------------------------------------------

* Yahan run(hello) mein hello function ko input ke roop mein diya gaya. 
  run() ke andar func usi function ko refer karta hai, isliye func() 
  original hello() ko chala deta hai.

Dhyan do:
---------
- hello   = function ka reference.
- hello() = function ko execute karna.
- func    = us function ko refer karne wala parameter.

* Ye teesra rule decorator ki foundation hai.

=================================================================================

3. Ab apna pehla decorator banate hain:
---------------------------------------

* Pehle hum ek decorator banayenge jo kisi function ke chalne se 
  pehle aur baad mein message print kare.

Ye code dekho:
--------------
def my_decorator(func):
    def wrapper():
        print("Function start")
        func()
        print("Function end")

    return wrapper

- Abhi is code ko run karne par koi message print nahi hoga, kyunki 
  humne my_decorator() ko call hi nahi kiya.

* Ab iske har part ka matlab samjho.

---------------------------------------------------------------------------------

Part A — my_decorator(func):
----------------------------

=> def my_decorator(func):

Ye decorator function hai.
--------------------------
- my_decorator iska naam hai. Naam kuch aur bhi rakh sakte ho.
- func ek parameter hai, jismein doosra function aayega.
- Jab hum my_decorator(hello) likhenge, tab func ko hello function milega.

---------------------------------------------------------------------------------

Part B — wrapper():
-------------------

def wrapper():
    print("Function start")
    func()
    print("Function end")

- Ye my_decorator ke andar ek naya function hai.

Iske andar humne teen kaam likhe hain:
--------------------------------------

1. Function start print karo.
2. func() se original function chalao.
3. Function end print karo.

* Andar alag function kyun banaya?

- Kyunki humein ye teen kaam decorator apply karte waqt nahi, balki 
  baad mein jab decorated function ko call karein, tab karwane hain.

- Agar hum ye print() statements seedhe my_decorator() mein likh dete, 
  to woh decorator apply karte hi execute ho jaate.

---------------------------------------------------------------------------------

Part C — return wrapper:
------------------------

=> return wrapper

* Ye poore concept ki sabse important line hai.

- Iska matlab hai: my_decorator() se wrapper function ko wapas bhejo.

- Yahan wrapper likha hai, wrapper() nahi. Isliye wrapper abhi execute 
  nahi hota.

* Aur return my_decorator kyun nahi?

  Kyunki my_decorator woh function hai jo decoration karta hai. Humein 
  uske andar banaya hua wrapper chahiye, jo original function ke saath 
  extra kaam karega.

---------------------------------------------------------------------------------

# Ek chhoti si comparison:

Code	              Matlab
-------------------------------------------------------------------------
return my_decorator   Decorator function ko hi return karo
-------------------------------------------------------------------------
return wrapper	      Naye wrapper function ko return karo
-------------------------------------------------------------------------
return wrapper()	  Wrapper ko abhi call karke uska result return karo
-------------------------------------------------------------------------

* Hamare example mein return wrapper sahi hai, kyunki humein wrapper ko 
  baad mein chalana hai.

=================================================================================

4. Ab tumhare original program ko execute karte hain
----------------------------------------------------

Poora program:
--------------
def hello():
    print("Hello!")


def my_decorator(func):
    def wrapper():
        print("Function start")
        func()
        print("Function end")
    return wrapper

hello = my_decorator(hello)
hello()

- Ab har line par Python kya karta hai, woh dekho.

---------------------------------------------------------------------------------

1. Original function banta hai

def hello():    
print("Hello!")

- Ab hello original function ko refer karta hai. Uske andar ka 
  print() abhi nahi chala.

---------------------------------------------------------------------------------

2. Decorator function banta hai

def my_decorator(func):    ...

- Ab Python ko pata hai ki my_decorator kya hai. Lekin abhi ye 
  function call nahi hua.

---------------------------------------------------------------------------------

3. Ye line execute hoti hai

hello = my_decorator(hello)

- Yahan my_decorator() sach mein call hota hai. Original hello 
  function usko input mein diya jaata hai. Isliye func original 
  hello ko refer karta hai.

---------------------------------------------------------------------------------

4. wrapper function banta hai aur return hota hai:

def wrapper():    ...return wrapper

- Python wrapper function banata hai aur uska reference my_decorator() 
  se wapas bhej deta hai. Wrapper ke andar ke statements abhi execute 
  nahi hue.

---------------------------------------------------------------------------------

5. Returned function hello mein assign hota hai

hello = my_decorator(hello)

- Assignment ki wajah se ab hello naam wrapper ko refer karta hai, 
  original function ko nahi.

---------------------------------------------------------------------------------

6. Ab hello() call hota hai

hello()

- Ab hello wrapper ko refer karta hai, isliye Python wrapper() execute 
  karta hai. Wrapper pehle start print karta hai, phir func() se original 
  hello() chalata hai, phir end print karta hai.

Output:
-------
Function start
Hello!
Function end

---------------------------------------------------------------------------------

Tumhare sabhi doubts ka seedha jawab:
-------------------------------------

- Kya my_decorator(hello) function call hai? Haan, bilkul.

- Kya decorator apply karte waqt call hota hai? Haan, my_decorator() us 
  waqt execute hota hai.

- Kya wrapper() us waqt call hota hai? Nahi. Us waqt sirf wrapper function 
  banta aur return hota hai.

- Phir wrapper() ko call kaun karta hai? Baad mein tumhara hello() call. 
  Kyunki hello ko wrapper se reassign kar diya gaya hai.

- Kya return wrapper aur wrapper() ek hi hain? Nahi. Pehla function return 
  karta hai, doosra function execute karta hai.

* Ek baat aur: func() kaam kaise karta hai? Kyunki func mein original hello 
               function ka reference abhi bhi maujood hai. hello naam ko 
               wrapper se reassign karne ke baad bhi original function ka 
               reference func ke through available rehta hai.

=================================================================================

5. @my_decorator kya hai? Decorator ka actual syntax:

* Ab tak humne decorator manually apply kiya tha:

=> hello = my_decorator(hello)

- Python isi kaam ko short syntax mein likhne deta hai:

@my_decorator
def hello():
    print("Hello!")

hello()

Output:
-------
Function start
Hello!
Function end

---------------------------------------------------------------------------------

* Ye dono approaches equivalent hain:

Manual way
----------
def hello():    
print("Hello!")

hello = my_decorator(hello)

Decorator syntax
----------------
@my_decorator
def hello():    
print("Hello!")

- Yaad rakhna: @my_decorator Python ka decorator syntax hai. my_decorator 
               khud koi special keyword nahi hai; woh tumhara banaya hua 
               normal function hai.

- Python @my_decorator dekhkar function ko decorator se pass karta hai aur  
  uska returned function hello naam se assign karta hai.

=================================================================================

6. Real-life example: Logging decorator
---------------------------------------

- Ab samjho decorator practical project mein kyun useful hai.

- Maan lo tumhari website par multiple functions hain aur tumhe 
  record karna hai ki kaunsa function execute hua.

CODE:
-----
def logging_decorator(func):
    def wrapper():
        print("Starting function...")
        func()
        print("Function completed!")
    return wrapper

@logging_decorator
def place_order():
    print("Order placed successfully")

@logging_decorator
def cancel_order():
    print("Order cancelled")

place_order()
cancel_order()

Output:
-------
Starting function...
Order placed successfully
Function completed!
Starting function...
Order cancelled
Function completed!

---------------------------------------------------------------------------------

* Dekho, logging ka code ek hi baar likha. Dono functions ko woh behavior 
  mil gaya.

* Real applications mein logging decorators timestamps, function names, 
  errors aur execution details bhi record kar sakte hain.

Isi tarah decorators ka use in kaamon mein bhi hota hai:
--------------------------------------------------------
- Execution time : Function kitni der mein complete hua.
- Access control : Function chalane se pehle permissions check karna.
- Caching: Pehle se calculate kiya result dobara use karna.
- Authentication : Protected operations se pehle login check karna.

=================================================================================

7. Deep concept: func() aur wrapper() ka relation:
--------------------------------------------------

* Ab ek subtle baat samjho.

def my_decorator(func):
    def wrapper():
        print("Before")
        func()
        print("After")
    return wrapper

Ismein do functions hain:
-------------------------
- wrapper() — naye behavior ko control karta hai.
- func()    — original function ko execute karta hai.

Jab hum ye karte hain:
----------------------
hello = my_decorator(hello)

* To original function ka reference func mein save rehta hai. Baad 
  mein hello() call karne par wrapper chalta hai aur func() ke 
  through original function bhi chal jaata hai.

* Isi wajah se hum original function ko call karne ke aas-paas extra 
  kaam kar sakte hain.

* Ek aur important baat: wrapper original function ka result automatically 
                         return nahi karta. Agar original function value 
                         return karta hai, to decorator mein us value ko 
                         preserve karne ke liye return likhna chahiye.

=================================================================================

8. Arguments aur return value wale functions:
---------------------------------------------

* Abhi hamara wrapper sirf aise functions ke liye tha jinmein arguments 
  nahi hain. Ek general-purpose decorator mein hum *args aur **kwargs 
  use kar sakte hain.

CODE:
-----
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Function start")

        result = func(*args, **kwargs)

        print("Function end")
        return result

    return wrapper

@my_decorator
def add(a, b):
    return a + b

answer = add(10, 20)
print(answer)

Output:
-------
Function start
Function end
30

Yahan:
------
- *args positional arguments accept karta hai.
- **kwargs keyword arguments accept karta hai.
- result original function ki returned value rakhta hai.
- return result us value ko caller tak pahunchata hai.

* Ye decorator ab add(10, 20) jaise arguments wale functions 
  ko bhi support karta hai.

=================================================================================

9. Common mistakes:
-------------------

Galti	                          Sahi understanding
--------------------------------------------------------------------------
return wrapper ko call samajhna	  Ye function return karta hai, execute 
                                  nahi.
--------------------------------------------------------------------------
return wrapper() likhna           Wrapper turant execute ho jaayega
--------------------------------------------------------------------------
return my_decorator likhna	      Aam taur par galat function return hoga
--------------------------------------------------------------------------
func ko func() samajhna	          func reference hai, func() call hai
--------------------------------------------------------------------------
Original result return na karna   Decorated function ki return value lose 
                                  ho sakti hai.
--------------------------------------------------------------------------
Har decorator mein wrapper    	  Wrapper common technique hai, compulsory 
zaroori samajhna                  rule nahi.
--------------------------------------------------------------------------

=================================================================================

10. Final revision — poora decorator ek nazar mein:
---------------------------------------------------

CODE:
-----
def my_decorator(func):
    def wrapper():
        print("Before")
        func()
        print("After")
    return wrapper

def hello():
    print("Hello!")

hello = my_decorator(hello)
hello()

---------------------------------------------------------------------------------

# Execution ka order:

1. my_decorator(hello) call hota hai
Original function input mein milta hai
          |
2. wrapper return hota hai
Abhi wrapper execute nahi hua
          |
3. hello wrapper ko refer karta hai
Assignment ke baad
          |
4. hello() wrapper ko chalata hai
Before → Hello! → After

* Agar tum sirf ek baat yaad rakhna chahte ho:

  Decorator function doosre function ko input mein lekar uske 
  behavior ko modify karne ke liye ek naya function return kar 
  sakta hai. wrapper() woh function hai jo extra behavior aur 
  original function ko ek saath chalata hai.

=================================================================================
---------------------------------------------------------------------------------
=================================================================================

Doubt:
------
mera 1st doubt toh ye hai ki...

def logging_decorator(func):
    def wrapper():
        print("Starting function...")
        func()
        print("Function completed!")
    return wrapper


@logging_decorator
def place_order():
    print("Order placed successfully")


@logging_decorator
def cancel_order():
    print("Order cancelled")


place_order()
cancel_order()

es program mai pehle toh ye batao ki ye @logging_decorator actully kr
kya rha hai or jaise place_order() krne pr def place_order(): call hoga
toh ye output kaise aa raha hai ?

Starting function...
Order placed successfully
Function completed!

or isme ye func() kya hai or kyu hai ?


or 2nd doubt ye hai ki ise dry run krke samjhai kyuki ye muje smj nhi
aaya ki kaise chl rha hai or kaise kya value pass ho rhi hai ?
isme ye  wrapper(*args, **kwargs) *args or **kwargs kya kr rhe hai
or isme kya value or kaise or kaha se aa rhi hai ye sab samjhana...

def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Function start")

        result = func(*args, **kwargs)

        print("Function end")
        return result

    return wrapper


@my_decorator
def add(a, b):
    return a + b   // add = my_decorator(add)
                      add == wrapper

answer = add(10, 20)  // wrapper(10, 20)
print(answer)

---------------------------------------------------------------------------------

Chalo, dono doubts ko ek-ek karke samajhte hain. Sabse important baat: 

* @logging_decorator original function ko replace karke uski jagah 
  wrapper function rakh deta hai. Ab dry run se dekho kaise.

=================================================================================

Doubt 1: @logging_decorator, func() aur output kaise aa raha hai ?
------------------------------------------------------------------

Tumhara code:
-------------
def logging_decorator(func):
    def wrapper():
        print("Starting function...")
        func()
        print("Function completed!")
    return wrapper

@logging_decorator
def place_order():
    print("Order placed successfully")

@logging_decorator
def cancel_order():
    print("Order cancelled")

place_order()
cancel_order()

---------------------------------------------------------------------------------

1. @logging_decorator actually kya karta hai ?\

Ye code:
--------
@logging_decorator
def place_order():
    print("Order placed successfully")

Python ke liye exactly iske equivalent hai:
-------------------------------------------
def place_order():
    print("Order placed successfully")

place_order = logging_decorator(place_order)

* Yaani Python pehle original place_order function banata hai. 
  Phir us function ko logging_decorator() mein bhejta hai.

<---------------------------------------------------------------->


# Ab isko step-by-step dekho.

1. Original function banta hai:

def place_order():
    print("Order placed successfully")

- Python function banata hai, lekin abhi uske andar ka print() 
  nahi chalta.

<---------------------------------------------------------------->

2. Decorator ko original function milta hai:

=> logging_decorator(place_order)

- func naam ke parameter mein original place_order function aa 
  jata hai.

<---------------------------------------------------------------->

3. wrapper function banta hai:

def wrapper():
    print("Starting function...")
    func()
    print("Function completed!")

- Ye function abhi execute nahi hota. Sirf banaya jata hai.

<---------------------------------------------------------------->

4. return wrapper se wrapper wapas milta hai:

=> return wrapper

- Ab assignment ke kaaran place_order naam original function ki 
  jagah wrapper ko refer karta hai.

---------------------------------------------------------------------------------

2. Toh place_order() karne par kaunsa function call hota hai ?

- wrapper() call hota hai, original place_order() directly nahi.

- Kyunki decorator lagne ke baad place_order naam ab wrapper ko 
  refer kar raha hai.

=> place_order()

Ab wrapper ke andar execution hota hai:
---------------------------------------
=> print("Starting function...")

Output:
-------
Starting function...

Phir ye line aati hai:
----------------------
=> func()

---------------------------------------------------------------------------------

3. func() kya hai aur kyun hai ?
--------------------------------

* Jab Python ne ye execute kiya tha:

=> logging_decorator(place_order)

- toh original place_order function func parameter mein aaya tha.

- Isliye func original function ka reference rakhta hai.

---------------------------------------------------------------------------------

Naam	                  Kis function ko refer karta hai ?
------------------------------------------------------------
func	                  Original place_order function
wrapper	                  Extra code chalane wala function
place_order	              Decorator lagne ke baad wrapper function

Isliye:
-------
=> func()  // ka matlab hai original function ko call karo.

- Original function chalta hai aur print karta hai:
=> Order placed successfully

- Phir wrapper ki next line chalti hai:
=> print("Function completed!")

Final output:
-------------
Starting function...
Order placed successfully
Function completed!

- cancel_order() ke saath bhi yahi process hota hai. Bas uske func mein 
  original cancel_order function hota hai, isliye beech mein Order 
  cancelled print hota hai.

- Ek line mein: wrapper pehle aur baad ka extra kaam karta hai; func() 
                original function ka kaam karwata hai.

=================================================================================

Doubt 2: *args, **kwargs aur result ka dry run:
-----------------------------------------------

* Ab tumhara doosra program:

CODE:
-----
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Function start")

        result = func(*args, **kwargs)

        print("Function end")
        return result

    return wrapper

@my_decorator
def add(a, b):
    return a + b

answer = add(10, 20)
print(answer)

- Pehle samjho *args aur **kwargs kis problem ko solve karte hain.

---------------------------------------------------------------------------------

1. *args aur **kwargs kya hain ?

* Maan lo function hai:

def add(a, b):
    return a + b

* Ise aise call karte hain:

=> add(10, 20)

- Yahan 10 aur 20 positional arguments hain. Ye a aur b mein jaate 
  hain.

- Lekin decorator ke wrapper() ko bhi ye arguments receive karne 
  padenge, taaki woh original function ko aage bhej sake.

Lsliye likhte hain:
-------------------
=> def wrapper(*args, **kwargs):

- *args positional arguments ko ek tuple mein collect karta hai.
- **kwargs keyword arguments ko ek dictionary mein collect karta hai.

Example:
--------
def show(*args, **kwargs):
    print(args)
    print(kwargs)

show(10, 20, name="Rahul", city="Indore")

Output:
-------
(10, 20)
{'name': 'Rahul', 'city': 'Indore'}

* Dhyan do: args aur kwargs sirf conventional names hain. Tum unke 
            naam kuch aur bhi rakh sakte ho; * aur ** important hain.

---------------------------------------------------------------------------------

2. Ab poore program ka dry run:
-------------------------------

Step 1: add function banta hai

@my_decorator
def add(a, b):
    return a + b

Ye equivalent hai:
------------------
def add(a, b):
    return a + b

add = my_decorator(add)

* Original add function my_decorator() ko diya jata hai. 
  Decorator ke andar:

=> def my_decorator(func):   // Ab func original add function 
                                ko refer karta hai.

Phir wrapper function banta hai aur:
------------------------------------
=> return wrapper

- ke through return hota hai.

- Ab add naam wrapper ko refer karta hai.

<-------------------------------------------------------->

Step 2: add(10, 20) call hota hai

=> answer = add(10, 20)

- Yaad rakho, ab add naam wrapper ko refer kar raha hai. Isliye 
  effectively ye call hota hai:

=> wrapper(10, 20)

- Wrapper ke andar:
=> def wrapper(*args, **kwargs):

Arguments collect hote hain:
----------------------------
Variable	      Value
args	          (10, 20)
kwargs	          {}

* kwargs empty hai kyunki humne koi keyword argument 
  nahi diya.

<-------------------------------------------------------->

Step 3: Function start print hota hai:
--------------------------------------

=> print("Function start")

Output:
-------
Function start

<-------------------------------------------------------->

Step 4: Ye important line execute hoti hai:
-------------------------------------------

=> result = func(*args, **kwargs)

<-------------------------------------------------------->

Isko todkar samjho:
-------------------
- func original add(a, b) function hai.
- args ki value (10, 20) hai.
- *args tuple ko unpack karke arguments 10 aur 20 bhejta hai.
- **kwargs empty dictionary ko keyword arguments ke roop mein 
    bhejta hai; yahan bhejne ke liye koi keyword argument nahi 
    hai.

Isliye ye line effectively iske barabar hai:
--------------------------------------------
=> result = original_add(10, 20)

Original function mein:
-----------------------
def add(a, b):    
return a + b

Ab values assign hoti hain:
---------------------------
a = 10
b = 20

Calculation:
------------
return 10 + 20   // Original function 30 return karta hai.


Ab wrapper ki line:
-------------------
=> result = func(*args, **kwargs)

- mein result ki value 30 ho jaati hai.

- Important: return a + b 30 ko return karta hai; print() 
             nahi karta. Isliye abhi 30 screen par nahi 
             dikhta.

<-------------------------------------------------------->

Step 5: Function end print hota hai:
------------------------------------

* Ab wrapper ki agli line execute hoti hai:

=> print("Function end")

Output:
-------
Function end

<-------------------------------------------------------->

Step 6: return result:
----------------------

=> return result

- result ki value 30 hai, toh wrapper bhi 30 return karta hai.

Isliye:
-------
answer = add(10, 20)

ke baad:
--------
answer = 30

Aur phir:
---------
print(answer)

- Output mein 30 print hota hai.

=================================================================================

3. Complete output
------------------
Function start
Function end
30

=================================================================================

4. *args, **kwargs aur func(*args, **kwargs) mein difference:
-------------------------------------------------------------

- Ye teen cheezein confuse mat karna:

Code	                Kaam
---------------------------------------------------------------------
*args	                Positional arguments collect karta hai; call 
                        mein unpack bhi kar sakta hai
---------------------------------------------------------------------
**kwargs	            Keyword arguments collect karta hai; call mein 
                        unpack bhi kar sakta hai
---------------------------------------------------------------------
func(*args, **kwargs)	Collected arguments ko original function tak 
                        bhejta hai
---------------------------------------------------------------------

---------------------------------------------------------------------------------

* Example mein args = (10, 20) tha. Lekin agar hum aise call karte:

=> add(a=10, b=20)

* toh wrapper ke andar values hoti:

=> args   = ()
=> kwargs = {'a': 10, 'b': 20}

* Phir:
=> func(*args, **kwargs)

- effectively original function ko aise call karta:
=> original_add(a=10, b=20)

. Result phir bhi 30 hoga.

Sabse important takeaway : *args aur **kwargs wrapper ko alag-alag arguments
                           wale functions ke saath kaam karne dete hain. 
                           func(*args, **kwargs) arguments original function 
                           ko bhejta hai, aur return result original function 
                           ka result caller tak wapas pahunchata hai.