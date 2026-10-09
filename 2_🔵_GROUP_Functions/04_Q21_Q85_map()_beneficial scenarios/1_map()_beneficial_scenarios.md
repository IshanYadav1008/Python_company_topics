1. map() hota kya hai?

* Python ka map() ek built-in function hai jo kisi function ko 
  collection ke har element par apply karta hai.

* Simple language mein: "Collection ke har item par ye kaam karo."

Example:
--------
numbers = [1, 2, 3, 4, 5]  // Agar har number ka square chahiye:

Normal for loop
---------------
squares = []

for number in numbers:
    squares.append(number * number)

print(squares)

Output:
-------
[1, 4, 9, 16, 25]

--> map() basically isi type ke repetitive transformation ko compact 
    way mein likhne deta hai.

==============================================================================

2. map() ka syntax

Basic syntax:
-------------
map(function, iterable)

Isko yaad rakho:
----------------
map(
    KYA KARNA HAI,
    KISKE HAR ELEMENT PAR KARNA HAI
)

Example:
--------
map(lambda x: x * x, numbers)

Yahan:
------
lambda x: x * x   // = kya karna hai

aur

numbers           // = kis collection ke elements par karna hai

==============================================================================

3. Pehla example — proper dry run

Code:
-----
numbers = [1, 2, 3, 4]
result = map(lambda x: x * 2, numbers)
print(list(result))

--> Ab isko line-by-line dry run karte hain.

------------------------------------------------------------------------------

Step 1
------
numbers = [1, 2, 3, 4]

Memory mein:
------------
numbers
   ↓
[1, 2, 3, 4]

------------------------------------------------------------------------------

Step 2
------
map(lambda x: x * 2, numbers)

Python dekhta hai:
------------------
--> Function:
lambda x: x * 2

--> Collection:
[1, 2, 3, 4]

<---------------------------------------------------->

* Ab map() function ko har element par apply karega.

Conceptually:
-------------
1 → lambda x: x * 2 → 2

2 → lambda x: x * 2 → 4

3 → lambda x: x * 2 → 6

4 → lambda x: x * 2 → 8

So results conceptually hain:
-----------------------------
2, 4, 6, 8

**IMP**
Lekin ek important baat: map() normally turant ek list nahi banata.

result = map(...)   // mein result ek map object hota hai.

==============================================================================

4. Phir list(result) kyun?

Humne likha:
------------
print(list(result))

* list() map object ke results ko lekar ek list bana deta hai.

So:
----
map object
    ↓
    2
    4
    6
    8
    ↓
list()
    ↓
[2, 4, 6, 8]

Output:
-------
[2, 4, 6, 8]

==============================================================================

5. Ek aur important dry run

Ab ye dekho:
------------
numbers = [10, 20, 30]
result  = map(lambda x: x + 5, numbers)
print(list(result))

numbers
-------
[10, 20, 30]

Lambda
------
lambda x: x + 5

Matlab:
-------
Jo bhi x mile, usme 5 add karo.

<--------------------------------------------->

* map() ek-ek karke:

First:
------
x = 10

10 + 5
  ↓
15

Second:
-------
x = 20

20 + 5
  ↓
25

Third:
------
x = 30

30 + 5
  ↓
35

So:
---
10 → 15
20 → 25
30 → 35

Final:
------
[15, 25, 35]

==============================================================================


6. map() ko loop ke saath compare karo

Ye:
---
numbers = [10, 20, 30]
result  = []

for x in numbers:
    result.append(x + 5)

<----------------------------------------------->

aur ye:
-------
numbers = [10, 20, 30]
result  = list(map(lambda x: x + 5, numbers))

<----------------------------------------------->

Dono ka result:
---------------
[15, 25, 35]

* Yaani map() ka main idea hai: "Har element ko 
                                 transform karo."

==============================================================================
------------------------------------------------------------------------------
==============================================================================

7. Real benefit scenario #1 — prices par discount:

* Suppose products ki prices hain:

=> prices = [100, 200, 500, 1000]

--> Ab Har product par 10% discount lagana hai.

<--------------------------------------------------->

Normal loop:
------------
discounted = []

for price in prices:
    discounted.append(price * 0.9)

<--------------------------------------------------->

map():
------
discounted = list(map(lambda price: price * 0.9, prices))

<--------------------------------------------------->

Dry run:
--------
100  → 100  × 0.9 → 90
200  → 200  × 0.9 → 180
500  → 500  × 0.9 → 450
1000 → 1000 × 0.9 → 900

Result:
-------
[90.0, 180.0, 450.0, 900.0]

Benefit
-------
* Jab same operation har element par repeatedly karna ho, 
  map() convenient hota hai.

==============================================================================

8. Real benefit scenario #2 — strings ko uppercase karna

Suppose:
--------
names = ["rahul", "aman", "rohit"]

* Sabko uppercase banana hai.

=> result = list(map(str.upper, names))

Dry run:
--------
"rahul" → str.upper → "RAHUL"

"aman"  → str.upper → "AMAN"

"rohit" → str.upper → "ROHIT"

Result:
-------
["RAHUL", "AMAN", "ROHIT"]

* Yahan lambda ki zarurat bhi nahi padi.

==============================================================================

9. Real benefit scenario #3 — strings ko numbers mein convert karna

Ye bahut practical example hai.
-------------------------------
* Maan lo user se numbers strings ke form mein aaye:

=> numbers = ["10", "20", "30", "40"]

* Hume actual integers chahiye.

=> numbers = list(map(int, numbers))

<--------------------------------------------------->

CODE:
-----
numbers = ["10", "20", "30", "40"]
numbers = list(map(int, numbers))
print(numbers)
print(type(numbers))

<--------------------------------------------------->

Dry run:
--------
"10" → int → 10

"20" → int → 20

"30" → int → 30

"40" → int → 40

Final:
------
[10, 20, 30, 40]

* Ye real-world Python mein kaafi common pattern hai.

==============================================================================

10. Yahan ek bahut important cheez samjho

* map() mein function dena hota hai, function ko call nahi karna.

Correct:
--------
map(int, numbers)

Correct:
--------
map(lambda x: x * 2, numbers)

Incorrect:
----------
map(int(), numbers)

<--------------------------------------------------->

* Kyun? Kyuki map() ko hum keh rahe hain:

"Ye function le jao aur har element par apply karo."

Isliye:
-------
int      // dena hai, na ki:

int()    // ye int() dena hai

Same:
-----
str.upper vs str.upper()

==============================================================================

11. map() ka mental model

Isko ek machine samjho:

             MAP MACHINE
                  │
       ┌──────────┴──────────┐
       │                     │
    FUNCTION             COLLECTION
       │                     │
  x → x * 2          [1, 2, 3, 4]
       │
       ↓
     APPLY
       │
       ↓
[2, 4, 6, 8]

<--------------------------------------------------->

Ya aur simple:
--------------

INPUT          FUNCTION         OUTPUT
-----          --------         ------
  1       →    × 2      →         2
  2       →    × 2      →         4
  3       →    × 2      →         6
  4       →    × 2      →         8

* Map ka core concept = one-to-one transformation.

==============================================================================

12. map() kab beneficial hai?

Scenario 1: Har element par same calculation
--------------------------------------------
numbers = [1, 2, 3, 4]
list(map(lambda x: x * 10, numbers))

------------------------------------------------------------------------------

Scenario 2: Data type conversion
--------------------------------
values = ["10", "20", "30"]
list(map(int, values))

------------------------------------------------------------------------------

Scenario 3: Text transformation
-------------------------------
names = ["rahul", "aman", "rohit"]
list(map(str.upper, names))

------------------------------------------------------------------------------

Scenario 4: Mathematical transformation
---------------------------------------
numbers = [2, 4, 6, 8]
list(map(lambda x: x ** 2, numbers))

------------------------------------------------------------------------------

Scenario 5: Data cleaning/transformation

Suppose:
--------
prices = ["100", "250", "500"]

Numbers mein convert:
---------------------
prices = list(map(int, prices))

Ab:
---
[100, 250, 500]

==============================================================================

13. map() kab use nahi karna chahiye?

* Agar operation complicated hai, normal for loop often zyada readable hota hai.

Example:
--------
def calculate(x):
    if x > 100:
        return x * 0.8
    else:
        return x * 0.9

Phir:
-----
result = list(map(calculate, prices))

--> Ye technically bilkul valid hai.

--> Lekin agar logic bahut complex ho jaye, simple for 
    loop zyada easy to understand ho sakta hai.

==============================================================================

14. Sabse important distinction: map() kya nahi karta?

* map() filter nahi karta.

Example:
--------
numbers = [1, 2, 3, 4, 5]

* Agar tumhe: sirf even numbers chahiye, toh ye filtering hai.

* Uske liye generally filter() use hota hai:

=> list(filter(lambda x: x % 2 == 0, numbers))

Output:
-------
[2, 4]

<-------------------------------------------------------------->

Whereas map():
--------------
list(map(lambda x: x * 2, numbers))

output:
-------
[2, 4, 6, 8, 10]

<-------------------------------------------------------------->

Ek line mein:
-------------
map()    → har item ko TRANSFORM karo
filter() → kuch items ko SELECT karo

==============================================================================

15. Ek final super-important example

CODE:
-----
numbers = [10, 20, 30]
result  = map(lambda x: x + 100, numbers)
print(list(result))

<-------------------------------------------------------->

* Isko exam/interview style dry run karo:

map() ko mila:
--------------
function = lambda x: x + 100
iterable = [10, 20, 30]

<-------------------------------------------------------->

First element:
--------------
x        = 10
10 + 100 = 110

<-------------------------------------------------------->

Second:
-------
x        = 20
20 + 100 = 120

<-------------------------------------------------------->

Third:
------
x        = 30
30 + 100 = 130

<-------------------------------------------------------->

Results:
--------
110, 120, 130

<-------------------------------------------------------->

list():
-------
[110, 120, 130]

<-------------------------------------------------------->

Final output:
-------------
[110, 120, 130]

<-------------------------------------------------------->

🧠 Bas ye 4 cheezein pakad lo

=> map(function, iterable)

1. function → har element ke saath kya karna hai
2. iterable → kin elements par karna hai
3. map()    → function ko har element par apply karta hai
4. list()   → map ke results ko list mein convert kar deta hai

Aur lambda ke context mein:
---------------------------
list(map(lambda x: x * 2, numbers))

ka literal mental translation:
------------------------------
"numbers ke har x ko lo, x * 2 karo, aur saare results ki list bana do."