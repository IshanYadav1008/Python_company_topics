1. Generator kya hota hai ?
---------------------------

* Python mein Generator ek aisa function hota hai jo ek baar mein saari 
  values dene ke bajay, ek-ek karke value deta hai.

* Generator banane ke liye hum yield keyword ka use karte hain.

Ek simple example dekho:
------------------------
def my_generator():       //  Ye ek generator function hai.
    yield 1
    yield 2
    yield 3

* Lekin dhyan do: jab hum my_generator() likhte hain, to function ki saari 
                  values turant nahi milti. Ye ek generator object banata 
                  hai.

g = my_generator()

print(next(g))  # 1
print(next(g))  # 2
print(next(g))  # 3

Output:
-------
1
2
3

- Har baar next(g) call karne par generator agli value deta hai.

===============================================================================

2. Pehle ek basic problem samjho:
---------------------------------

* Maan lo tumhe 5 numbers print karne hain.

Normal function:
----------------
def numbers():
    return [1, 2, 3, 4, 5]

print(numbers())

Output:
-------
[1, 2, 3, 4, 5]

- Ismein function ek poori list return kar raha hai.

-------------------------------------------------------------------------------

* Ab wahi kaam generator se:
----------------------------
def numbers():
    yield 1
    yield 2
    yield 3
    yield 4
    yield 5

for n in numbers():
    print(n)

Output:
-------
1
2
3
4
5

* Output same numbers hain, lekin values dene ka tareeka alag hai.

-------------------------------------------------------------------------------

# Normal function vs Generator:

Normal function
---------------
- return se result deta hai aur function call khatam ho jata hai.

Generator
---------
- yield se ek value deta hai, pause hota hai aur baad mein resume 
  ho sakta hai.

===============================================================================

3. yield kya hota hai ?
-----------------------

* Generator samajhne ke liye yield sabse important hai.

yield ka matlab hai:
--------------------
1. Ek value produce karo.
2. Function ko wahi pause kar do.
3. Jab agli value maangi jaye, wahin se dobara continue karo.

Example:
--------
def demo():
    print("Start")
    yield 10

    print("Middle")
    yield 20

    print("End")

<--------------------------------------------------->

Ab ise run karte hain:
----------------------
g = demo()

print(next(g))
print(next(g))

<--------------------------------------------------->

Output:
-------
Start
10
Middle
20

Dhyan do, "End" print nahi hua.

Kyun? Kyunki humne abhi generator se teesri baar 
value nahi maangi.

<--------------------------------------------------->

Agar ye likho:
--------------
=> print(next(g))

To output hoga:
---------------
End

Traceback (most recent call last):
    ...
StopIteration

* Aisa isliye kyunki function khatam ho gaya aur koi agli value 
  available nahi hai. next() call karne par generator ke khatam 
  hone ka signal StopIteration hota hai.

===============================================================================

4. Generator ka execution kaise chalta hai?

Isko ek-ek step mein dekho.

Step 1: g = demo()
------------------
- Generator object banta hai. Function body abhi execute nahi hoti.

Step 2: Pehla next(g)
---------------------
- Execution start hota hai, Start print hota hai aur yield 10 par 
  pause ho jata hai.

Step 3: Doosra next(g)
----------------------
- Wahin se resume hota hai, Middle print hota hai aur yield 20 par 
  pause ho jata hai.

Step 4: Teesra next(g)
----------------------
- End print hota hai. Function complete ho jata hai aur StopIteration 
  raise hota hai.

* Deep point: Generator apni execution state yaad rakhta hai. Ismein 
  ye bhi shamil hai ki execution kahan ruka tha aur local variables 
  ki current values kya thi.

===============================================================================

5. Generator memory kaise bachata hai?
--------------------------------------

* Maan lo tumhe 10 lakh numbers process karne hain.

List se:
--------
numbers = [x for x in range(1_000_001)]

- Ye list saare numbers ek saath store karti hai.

<--------------------------------------------------->

Generator se:
-------------
def numbers():
    for x in range(1_000_001):
        yield x

Ab:
---
for n in numbers():
    print(n)

- Generator values ko zaroorat ke hisaab se produce karta hai; saari 
  values ki list pehle nahi banata.

- Isliye ye aksar memory bachata hai, khaaskar jab bahut saari values 
  ko ek-ek karke process karna ho.

- Ek important baat: Generator zero memory use nahi karta. Use apni 
                     current state aur zaroori data rakhna hota hai. 
                     Memory saving is baat par depend karti hai ki 
                     tum values ko kaise use karte ho.

===============================================================================

6. Generator function aur Generator object mein difference:

* Ye exam ke liye important hai.

def test():
    yield 100
    yield 200

Yahan:
------
- test ek generator function hai.
- test() call karne par jo object milta hai, woh generator object hai.
- next(test()) se 100 milega, lekin har baar test() dobara call karoge 
  to naya generator banega.

Sahi tareeka:
-------------
g = test()
print(next(g))  # 100
print(next(g))  # 200

- Agar generator exhaust ho gaya, to usi object se dobara values nahi 
  milengi.

===============================================================================

7. Generator ke main advantages:
--------------------------------
- Memory efficient     : Badi list ko ek saath store karne ki zaroorat nahi.
- Lazy evaluation      : Value tab generate hoti hai jab maangi jati hai.
- Better for streaming : Files, records aur data ko ek-ek karke process kar 
                         sakte ho.
- Simple code          : Kuch iterators ko manually implement karne ke mukable 
                         generator likhna aasaan hota hai.

===============================================================================

8. Exam mein likhne layak definition:
-------------------------------------
* A generator in Python is a special type of function that uses the yield 
  keyword to produce values one at a time. It pauses its execution after 
  yielding a value and resumes from the same point when the next value is 
  requested. Generators are memory-efficient because they generate values 
  lazily instead of storing all values at once.

===============================================================================

9. Ab apna concept test karo:
-----------------------------

Question: Is code ka output kya hoga?

CODE:
-----
def test():
    yield 5
    yield 10

g = test()
print(next(g))
print(next(g))

O/P: 5, phir 10   // Pehla next(g) value 5 deta hai. Doosra next(g) 
                     wahi se resume karke value 10 deta hai.

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Doubt:
------
muje ek baat batao tmne bola ki, Isliye ye aksar memory bachata hai, khaaskar 
jab bahut saari values ko ek-ek karke process karna ho. lekin ye memory 
bacchanta kaise hai 

saari values ki list pehle nahi banata, bhle pehle nhi banata lekin phir bhi 
values ko store karne ka tarika thodi alg ho jayega, values toh memory mai 
same tarah se hi jyengi naa ? Ye muje clear krke do simple way mai.

-------------------------------------------------------------------------------

* Bhai, tumhara doubt bilkul sahi hai. ❤️ Tum ye soch rahe ho ki list ho ya 
  generator, values ko aakhir RAM mein hi rehna hai, toh memory bachegi 
  kaise?

- Isko ekdum basic se samajhte hain.

===============================================================================

1. Pehle ek example imagine karo:
---------------------------------
- Maan lo tumhe 10 lakh numbers process karne hain, 1 se lekar 
  10,00,000 tak.

<------------------------------------------------------------->

Tumhare paas do tareeke hain:
-----------------------------

Tareeka 1: List

* Socho tumhe 10 lakh books padhni hain. Tum pehle saari books 
  apne kamre mein laakar rakh dete ho.

- Saari values ek saath memory mein.
- Jab zaroorat ho, koi bhi value access kar sakte ho.
- Bahut saari values ke liye kaafi memory lag sakti hai.

<------------------------------------------------------------->

Tareeka 2: Generator

* Socho library se ek-ek book laate ho, padhte ho aur aage badh 
  jaate ho. Saari books ek saath apne kamre mein nahi rakhte.

- Ek value tab banti hai jab uski zaroorat hoti hai.
- Pichhli value ko agar aage zaroorat nahi, toh use rakhna zaroori 
  nahi.
- Isliye saari values ko ek saath store karne ki zaroorat nahi.

* Ye example samajhne ke liye hai. Actual Python memory mein values 
  kaise store hoti hain, woh thoda aur samjho.

===============================================================================

2. Ab Python code se samjho:
----------------------------

- List wala tareeka

=> numbers = list(range(1, 1000001))

. Is line mein Python ek list banata hai jismein 10 lakh numbers ke 
  elements hote hain.

Conceptually:
-------------

RAM mein list

1              2              3              4
5              6              7              8
... isi tarah 10 lakh elements ki jagah

Saare elements ko ek saath rakhne ke liye memory chahiye.

<------------------------------------------------------------->

Generator wala tareeka:
-----------------------
def numbers():
    for i in range(1, 1000001):
        yield i

g = numbers()

- Abhi g banane par 10 lakh numbers ki list nahi bani.

- Generator apni current execution state rakhta hai. 
  Jab tum next(g) karte ho, tab agla number produce 
  hota hai.

print(next(g))  # 1
print(next(g))  # 2
print(next(g))  # 3

<------------------------------------------------------------->

Generator ki memory
-------------------

i = 3                   -->          Agli value produce karo
Current state

- Conceptually, generator ko aage badhne ke liye current state 
  yaad rakhni hoti hai; poori 10 lakh numbers ki list nahi.

===============================================================================

3. Tumhare main doubt ka jawab:
-------------------------------

* Tumne kaha: Values toh memory mein same tarah se hi jayengi naa ?

* Nahi, zaroori nahi. Difference ye hai ki values kitni ek saath 
  memory mein rakhi ja rahi hain.

- List      : 10 lakh values ke liye list ka storage ek saath chahiye.

- Generator : Agar tum ek-ek value process kar rahe ho, toh generator 
              ko poori list rakhne ki zaroorat nahi.

-------------------------------------------------------------------------------

* Ek aur important baat: generator se nikli value bhi memory use karti hai. 
  Lekin agar tum use process karke aage badh jaate ho aur uska reference 
  kahin store nahi karte, toh purani value ko generally alag se sambhal 
  kar rakhne ki zaroorat nahi hoti.

- Agar tum generator ki saari values ko dobara list mein store kar do, toh 
  memory ka fayda khatam ho sakta hai:

=> all_numbers = list(numbers())

- Ab phir se saare numbers ek list mein store ho jayenge.

===============================================================================

4. Ek chhota sa memory experiment:
----------------------------------

* Is example mein hum dono tareekon se numbers ka sum nikal rahe hain:

# List
numbers_list = list(range(1, 1000001))
total1 = sum(numbers_list)

# Generator
numbers_gen = (x for x in range(1, 1000001))
total2 = sum(numbers_gen)

Dono ka sum same hoga. Lekin generator wale case mein 10 lakh elements 
ki list nahi banayi gayi.

Ek line mein yaad rakho:
------------------------
List saari values ko ek saath store karti hai, jabki generator values ko 
zaroorat ke hisaab se produce karta hai. Memory isliye bachti hai kyunki 
ek saath bahut saari values ko store karna avoid hota hai, na ki isliye 
ki har individual number memory use karna band kar deta hai.

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Doubt-2:
--------
pehli baat toh ye ki ye example generator ka kaise hai ? 
isme yield toh kahi use hi nhi hua ??

numbers_gen = (x for x in range(1, 1000001))
total2      = sum(numbers_gen)

-------------------------------------------------------------------------------

ANS) Bhai, bahut badhiya question! Tumne sahi notice kiya ki is code 
     mein yield likha hi nahi hai. Phir ye generator kaise hai ? 

numbers_gen = (x for x in range(1, 1000001))
total2      = sum(numbers_gen)

- Chalo, zero level se samajhte hain.

===============================================================================

1. Python mein generator banane ke 2 tareeke hain:
--------------------------------------------------

Tareeka 1: Generator function — yield use karke

def numbers():
    for x in range(1, 6):
        yield x

numbers_gen = numbers()

* Yahan yield ki wajah se numbers() ek generator function hai. Jab ise 
  call karte hain, toh generator object milta hai.

-------------------------------------------------------------------------------

Tareeka 2: Generator expression — bina yield likhe:

=> numbers_gen = (x for x in range(1, 6))

- Ye bhi generator banata hai! Ismein yield explicitly likhne ki 
  zaroorat nahi hoti.

===============================================================================

2. Generator expression ko pehchane ka shortcut:
------------------------------------------------

In dono codes ko dekho:

List comprehension
------------------
nums = [x for x in range(1, 6)]

Output: [1, 2, 3, 4, 5]

- Square brackets [] list banate hain, jo saare results store karti hai.

------------------------------------------------------------------------------

Generator expression
--------------------
=> nums = (x for x in range(1, 6))

- Output ko print karne par generator object dikhega, 
  jaise <generator object ...>.

- Round brackets () ke andar comprehension likhne se 
  generator expression banta hai, jo values ko zaroorat 
  ke hisaab se produce karta hai.

===============================================================================

3. Ab tumhare code ko samjho:
-----------------------------

numbers_gen = (x for x in range(1, 1000001))
total2 = sum(numbers_gen)

Ismein:
-------
1. (x for x in range(1, 1000001)) ek generator expression hai.
2. numbers_gen us generator object ko refer karta hai.
3. sum(numbers_gen) generator se ek-ek value leta hai aur unka 
   sum nikalta hai.
4. Is process mein saare 10 lakh numbers ki list pehle nahi banti.

===============================================================================

4. Ek important difference yaad rakhna:
---------------------------------------

-----------------------------------------------------------
Code	                                Kya banta hai?
-----------------------------------------------------------
[x for x in range(5)]	                List
(x for x in range(5))	                Generator object
yield x wala function	                Generator function
numbers() — jab numbers mein yield ho	Generator object
-----------------------------------------------------------

Exam trick: Generator banane ke liye har baar yield likhna compulsory 
            nahi hai. Generator function mein yield hota hai, jabki 
            generator expression mein parentheses () aur comprehension 
            ka syntax hota hai.

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Doubt-3:
--------
ek cheez or ki ye code execute kaise hoga ?
def numbers():
    for x in range(1, 6):
        yield x

numbers_gen = numbers()

kyuki numbers() se object ban gaya eb next kaise or kaha likhenge ?

-------------------------------------------------------------------------------

ANS) Bhai, tumhara doubt ye hai ki numbers() se generator object ban gaya, 
     lekin ab us object ko execute kaise karna hai, aur next() kahan likhna 
     hai ?

Chalo, ek-ek step samajhte hain.

===============================================================================

1. Pehle ye code dekho:
-----------------------
def numbers():
    for x in range(1, 6):
        yield x

numbers_gen = numbers()

* Jab tum numbers_gen = numbers() likhte ho, tab generator object banta 
  hai, slekin function ke andar ka code abhi execute nahi hota.

===============================================================================

2. Ab next() kahan likhna hai?
------------------------------
* numbers_gen variable mein generator object store hai. Isi variable ko 
  next() ke andar pass karna hai.

CODE:
-----
def numbers():
    for x in range(1, 6):
        yield x

numbers_gen = numbers()

print(next(numbers_gen))
print(next(numbers_gen))
print(next(numbers_gen))
print(next(numbers_gen))
print(next(numbers_gen))

Output:
-------
1
2
3
4
5

--> Bas! Ab samjho ki andar kya hua.

===============================================================================

3. Step-by-step execution:
--------------------------

Step 1
------
=> numbers_gen = numbers()

. Generator object bana. Abhi for loop execute nahi hua.

------------------------------------------------------------------------------

Step 2
------
=> next(numbers_gen)

. Function execute hona shuru hua. x = 1 hua, phir yield 
  x ne 1 de diya aur execution pause ho gaya.

------------------------------------------------------------------------------

Step 3
------
=> next(numbers_gen)

. Jahan execution ruka tha, wahin se resume hua. Ab x = 2 
  aur yield x ne 2 de diya.

------------------------------------------------------------------------------

Step 4
------
. Har agla next(numbers_gen) agli value deta hai: 3, 4, phir 5.

===============================================================================

4. Kya har baar next() hi likhna zaroori hai?

* Nahi! Tum for loop bhi use kar sakte ho. Python automatically next() 
  call karta hai aur generator khatam hone par loop rok deta hai.

CODE:
-----
def numbers():
    for x in range(1, 6):
        yield x

numbers_gen = numbers()

for num in numbers_gen:
    print(num)

Output:
-------
1
2
3
4
5

------------------------------------------------------------------------------

Yaad rakhne ka rule:
--------------------
- numbers()              → generator object banata hai.
- next(numbers_gen)      → agli value nikalta hai.
- for num in numbers_gen → saari available values ek-ek karke nikalta hai.

* Ek baat aur: jab generator ki saari values nikal chuki hoti hain, 
               toh usi generator par dobara next() call karne se 
               StopIteration exception aata hai.