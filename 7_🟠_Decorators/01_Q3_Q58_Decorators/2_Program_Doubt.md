* Bilkul! Tumhe my_decorator(add) se wrapper return hone ke baad 
  execution flow kahan jaata hai, bas yahi point clear nahi ho 
  raha. Chalo isko ekdum basic se, line-by-line samajhte hain.

Sabse pehle ek baat yaad rakho:
-------------------------------
* Python mein jab koi function return karta hai, toh woh apne 
  caller ke paas wapas jaata hai. Uske baad Python next 
  statement execute karta hai.

- Ab isi rule ko tumhare program mein apply karte hain.

================================================================================

1. Pehle poora program dekho:
-----------------------------
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

Hum is program ko 3 phases mein samjhenge:
------------------------------------------
- Phase 1: add function define hona.
- Phase 2: Decorator ka chalna aur wrapper return hona.
- Phase 3: add(10, 20) call hona aur answer milna.

--------------------------------------------------------------------------------

* Lekin upr waale program mai values kch es tarah hongi toh unhe hum
  us tarah likh kar program ko likh rhe hai jisse flow smjne mai easy
  ho sake:

CODE:
-----
def my_decorator(func):                 // func == add
    def wrapper(*args, **kwargs):
        print("Function start")

        result = func(*args, **kwargs)  // func == add, add(10,20)

        print("Function end")
        return result

    return wrapper

@my_decorator       
def add(a, b):
    return a + b   
                   
// add = my_decorator(add)
// add = wrapper

answer = add(10, 20)  // add(10,20) == wrapper(10,20)
print(answer)

================================================================================

2. Phase 1 — my_decorator function define hua:
----------------------------------------------
=> def my_decorator(func):

- Is line ka matlab hai ki Python my_decorator naam ka function bana 
  raha hai.

- Dhyan do: abhi function ke andar ki lines execute nahi hui hain. 
            Python ne sirf function ko define kiya hai.

-------------------------------------------------------------------------------

Uske baad:
----------
def add(a, b):    
return a + b

- Ye add function ka original code hai.

- Iska kaam hai do numbers ko add karke result return karna.

* Lekin yahan ek important baat hai: kyunki add ke upar decorator laga hai, 
                                     isliye Python normal tareeke se add ko 
                                     final naam assign nahi karega. Decorator 
                                     bhi process hoga.

================================================================================

3. Phase 2 — @my_decorator actually kya karta hai?
--------------------------------------------------

Tumhara code:
-------------
@my_decorator
def add(a, b):
    return a + b

Python ise conceptually aise samajhta hai:
------------------------------------------
def add(a, b):
    return a + b

add = my_decorator(add)

- Ab ise ek-ek line mein dekho.

--------------------------------------------------------------------------------

Step 1: Original add function banta hai
---------------------------------------
def add(a, b):
    return a + b

- Ab add naam original function ko refer karta hai.

--------------------------------------------------------------------------------

Step 2: Ye line execute hoti hai
--------------------------------

=> add = my_decorator(add)   // Yahan right side pehle execute hoti hai:

=> my_decorator(add)         // Matlab Python original add function ko
                                my_decorator ke andar bhej raha hai.

Ab:
---
=> def my_decorator(func):   // func ke andar original add function ka 
                                reference aa jaata hai.

Conceptually:
-------------
=> func = original_add

--------------------------------------------------------------------------------

Step 3: Ab wrapper define hota hai:
-----------------------------------
def wrapper(*args, **kwargs):
    print("Function start")

    result = func(*args, **kwargs)

    print("Function end")
    return result

- Python wrapper function ko define karta hai.
- Lekin abhi wrapper ke andar ka code execute nahi hota.

Yaani abhi ye print nahi hoga:
------------------------------
=> print("Function start")

. Kyunki humne wrapper() ko call hi nahi kiya.

--------------------------------------------------------------------------------

Step 4: Ye line execute hoti hai
--------------------------------
=> return wrapper

Iska matlab hai:
----------------
- my_decorator function apna kaam khatam karke wrapper function ko 
  caller ke paas return kar do.

Ab tumhara sabse important sawaal:
----------------------------------
- return wrapper ke baad control kahan jaata hai?

- Control wapas us jagah jaata hai jahan se my_decorator(add) call
  hua tha, yaani yahan:

=> add = my_decorator(add)   // Ab right side ki value mil chuki hai
                                — woh value wrapper function hai.

Isliye assignment effectively aisa ho jaata hai:
------------------------------------------------
add = wrapper

--------------------------------------------------------------------------------

* Ab add naam original function ko nahi, balki wrapper function ko 
  refer karta hai.

# Ab tak ka flow:
-----------------
my_decorator(add) call hua
        |
        |
wrapper function define hua
        |
        |
return wrapper
        |
        |
add = wrapper

================================================================================

4. Ab tumhara main sawaal — next line par control kaise jaata hai ?
-------------------------------------------------------------------

* Decorator ka kaam complete ho gaya. Python ab program ki agli 
  statement execute karta hai:

=> answer = add(10, 20)

- Python ko ye nahi dekhna hota ki wrapper return hua hai, isliye 
  program ruk jaaye. return sirf my_decorator function ko khatam 
  karta hai, poore program ko nahi.

* Ab kyunki add = wrapper ho chuka hai, isliye:
-----------------------------------------------
=> answer = add(10, 20)

ka matlab effectively hai:
--------------------------
=> answer = wrapper(10, 20)

- Yahi woh point hai jahan wrapper pehli baar execute hota hai!

--------------------------------------------------------------------------------

Ab wrapper ke andar chalte hain:
--------------------------------
=> def wrapper(*args, **kwargs):

Yahan values aati hain:
-----------------------
args = (10, 20)
kwargs = {}

- *args positional arguments ko collect karta hai, aur **kwargs 
   keyword arguments ko.

Ab execution line-by-line hoga:

--------------------------------------------------------------------------------

Step 1
------
=> print("Function start")

Output:
-------
Function start

<--------------------------------------------------------->

Step 2
------
=> result = func(*args, **kwargs)

- Yaad karo: func original add function ko refer karta hai.

Isliye ye effectively hai:
--------------------------
=> result = original_add(10, 20)

Original function chalta hai:
-----------------------------
def add(a, b):
    return a + b

Yahan:
------
a = 10
b = 20

Toh:
----
return a + b   // 30 return karta hai.

Ab wrapper mein wapas aakar:
----------------------------
=> result = 30   // ho jaata hai.

<--------------------------------------------------------->

Step 3
------
=> print("Function end")

Output:
-------
Function end

<--------------------------------------------------------->

Step 4
------
=> return result

Yaani:
------
return 30

--------------------------------------------------------------------------------

* Ab wrapper bhi khatam ho jaata hai aur 30 us jagah return 
  hota hai jahan se wrapper(10, 20) call hua tha.

Woh jagah thi:
--------------
=> answer = add(10, 20)

Isliye:
-------
answer = 30

Ab agli line execute hogi:
--------------------------
=> print(answer)

Output:
-------
30

================================================================================

5. Poore program ka execution flow ek saath:
--------------------------------------------

1. Original add define hota hai
- Do numbers add karne wala function banta hai.

2. my_decorator(add) call hota hai
- Original function func mein milta hai. wrapper define 
  hota hai.

3. return wrapper
- Decorator khatam hota hai aur add naam ab wrapper ko 
  refer karta hai.

4. answer = add(10, 20)
- Ab wrapper(10, 20) call hota hai.

5. wrapper original function ko call karta hai
- Start print hota hai, original add 30 return karta hai, 
  phir end print hota hai.

answer = 30

* Aakhir mein print(answer) se 30 print hota hai.

Final output:
-------------
Function start
Function end
30

================================================================================

6. Ab ek chhota sa test karo:
-----------------------------
* Dekhte hain ki return wrapper aur wrapper() ke beech ka 
  difference clear hua ya nahi.

Question: Jab Python return wrapper execute karta hai, tab 
          kya print("Function start") bhi execute hota hai ?

Answer  : Nahi, kyunki wrapper abhi sirf return hua hai, 
          call nahi hua.  

Bilkul sahi! 🎉
------------
- Function ko return karna aur function ko call karna alag 
  cheezein hain. Start tab print hota hai jab add(10, 20), 
  yaani wrapper(10, 20), call hota hai.

- Bas ye ek difference pakad lo: return wrapper function ko wapas 
                                 deta hai, jabki wrapper(10, 20) 
                                 us function ko chalata hai. Yahi 
                                 tumhare execution flow ka main 
                                 concept hai.