Bilkul. filter() ko samajhne ka easiest way hai map() se 
compare karke samajhna.

map()    = har item ko transform/change karo
filter() = condition ke basis par kuch items ko rakh lo, 
           baaki hata do.

==============================================================================

1. filter() kya hota hai?

* Python ka filter() ek built-in function hai jo kisi collection 
  ke elements mein se sirf un elements ko select karta hai jo 
  given condition ko satisfy karte hain.

Simple language:
----------------
"Har item ko check karo. Jo condition pass kare, usko rakh lo."

Example:
--------
numbers = [1, 2, 3, 4, 5, 6]

* Hume sirf even numbers chahiye: [2, 4, 6]

* Yahan filter() useful hai.

==============================================================================

2. Basic syntax
---------------
=> filter(function, iterable)

Isko map() ki tarah read karo:
------------------------------
filter(
    KYA CONDITION CHECK KARNI HAI,
    KIS COLLECTION KE ELEMENTS KO CHECK KARNA HAI
)

Example:
--------
filter(lambda x: x % 2 == 0, numbers)

Yahan:
------
lambda x: x % 2 == 0  // condition hai.

* Matlab: "x even hai ya nahi?"

==============================================================================

3. Sabse pehla example — proper dry run

Code:
-----
numbers = [1, 2, 3, 4, 5, 6]
result  = filter(lambda x: x % 2 == 0, numbers)
print(list(result))

* Ab ekdum step-by-step.

------------------------------------------------------------------------------

Step 1
------
numbers = [1, 2, 3, 4, 5, 6]

Collection:
-----------
[1, 2, 3, 4, 5, 6]

------------------------------------------------------------------------------

Step 2
------
lambda x: x % 2 == 0  // Ye kya kar raha hai?

Har x ke liye check:

x % 2 == 0

Agar result:
------------
True          → item rakhna hai

Agar:

False         → item remove/ignore karna hai.

==============================================================================

4. Ab actual dry run:

First element:
--------------
x = 1

1 % 2 == 0
1     == 0

False

So:
---
1 → ❌ reject

<------------------------------------------------------>

Second:
-------
x = 2

2 % 2 == 0
0     == 0
True

So:
---
2 → ✅ keep

<------------------------------------------------------>

Third:
------
x = 3

3 % 2 == 0
1     == 0
False

3 → ❌ reject

<------------------------------------------------------>

Fourth:
-------
x = 4

4 % 2 == 0
0     == 0
True

4 → ✅ keep

<------------------------------------------------------>

Fifth:
------
x = 5

5 % 2 == 0
1     == 0
False

5 → ❌ reject

<------------------------------------------------------>

Sixth:
------
x = 6

6 % 2 == 0
0 == 0
True

6 → ✅ keep

<------------------------------------------------------>

So internally:
--------------
1 → False → ❌
2 → True  → ✅
3 → False → ❌
4 → True  → ✅
5 → False → ❌
6 → True  → ✅

Bach gaye:
----------
2, 4, 6

Aur:
----
list(result)

karne ke baad:
--------------
[2, 4, 6]

==============================================================================

5. filter() mein True aur False ka kya role hai?

**Ye bahut important hai.**

* filter() basically poochta hai: "Is element ko rakhna hai?"

Function ka answer:
-------------------
True  → YES, rakho
False → NO, hata do

Example:
--------
filter(lambda x: x > 10, numbers)

Agar:
-----
x = 15

toh: 15 > 10 --> True → 15 rakho.

Agar: 
-----
x = 5

toh: 5 > 10 --> False → 5 mat rakho.

==============================================================================

6. map() vs filter() — sabse important difference

* Ye distinction achhe se samajh lo.

map()
-----
numbers = [1, 2, 3, 4]
list(map(lambda x: x * 10, numbers))

Dry run:
--------
1 → 10
2 → 20
3 → 30
4 → 40

Result:
-------
[10, 20, 30, 40]  // Har item transform hua.

------------------------------------------------------------------------------

filter()
--------
numbers = [1, 2, 3, 4]
list(filter(lambda x: x > 2, numbers))

Dry run:
--------
1 → False → ❌
2 → False → ❌
3 → True  → ✅
4 → True  → ✅

Result:
-------
[3, 4]

* Items transform nahi hue; sirf select hue.

==============================================================================

7. Ek simple mental model

map()
-----

INPUT        ACTION        OUTPUT
-----       --------       ------
  1    →      ×10     →     10
  2    →      ×10     →     20
  3    →      ×10     →     30

* Har item ka new version ban raha hai.

------------------------------------------------------------------------------

filter()
--------

INPUT       CONDITION       OUTPUT
-----       ---------       ------
  1    →     > 2       →      ❌
  2    →     > 2       →      ❌
  3    →     > 2       →      ✅
  4    →     > 2       →      ✅

* Yahan items ko select/reject kiya ja raha hai.

==============================================================================

8. Real-world example — age

Suppose:
--------
ages = [12, 18, 25, 15, 30, 10]

* Hume sirf adults chahiye:

adults = list(filter(lambda age: age >= 18, ages))

Dry run:
--------
12 → 12 >= 18 → False → ❌
18 → 18 >= 18 → True  → ✅
25 → 25 >= 18 → True  → ✅
15 → 15 >= 18 → False → ❌
30 → 30 >= 18 → True  → ✅
10 → 10 >= 18 → False → ❌

Result:
-------
[18, 25, 30]

* Ye filter() ka perfect use case hai.

==============================================================================

9. Real-world example — prices

Suppose:
--------
prices = [50, 200, 1500, 80, 3000, 120]

* Hume sirf expensive products chahiye, maan lo 1000 se upar:

expensive = list(filter(lambda price: price > 1000, prices))

Dry run:
--------
50   → False ❌
200  → False ❌
1500 → True  ✅
80   → False ❌
3000 → True  ✅
120  → False ❌

Result:
-------
[1500, 3000]

==============================================================================

10. Strings ke saath

Suppose:
--------
names = ["Rahul", "Aman", "Rohit", "Ankit", "Raj"]

* Hume sirf names chahiye jinki length 4 se zyada hai:

result = list(filter(lambda name: len(name) > 4, names))

Dry run:
--------
"Rahul" → len = 5 → 5 > 4 → True  → ✅
"Aman"  → len = 4 → 4 > 4 → False → ❌
"Rohit" → len = 5 → 5 > 4 → True  → ✅
"Ankit" → len = 5 → 5 > 4 → True  → ✅
"Raj"   → len = 3 → 3 > 4 → False → ❌

Result:
-------
["Rahul", "Rohit", "Ankit"]

==============================================================================

11. filter() ke saath normal function bhi use kar sakte ho
    Lambda compulsory nahi hai.

Example:
--------
def is_even(x):
    return x % 2 == 0

Then:
-----
numbers = [1, 2, 3, 4, 5, 6]
result = list(filter(is_even, numbers))

Output:
-------
[2, 4, 6]

Dry run:
--------
1 → is_even(1) → False → ❌
2 → is_even(2) → True  → ✅
3 → is_even(3) → False → ❌
4 → is_even(4) → True  → ✅
5 → is_even(5) → False → ❌
6 → is_even(6) → True  → ✅

* Yahan filter() ko                 : is_even, function diya, is_even() 
                                      nahi.

* Exactly waise hi jaise map() mein : map(int, numbers) , likhte hain, 
                                      int() nahi.

==============================================================================

12. filter() ka output direct list nahi hota

* Ye bhi map() jaisa hi important point hai.

=> result = filter(lambda x: x > 10, numbers)

* result ek filter object hota hai.

<-------------------------------------------------->

Agar tum list chahte ho:
------------------------
result = list(filter(lambda x: x > 10, numbers))

Then list milegi.

Mental model:
-------------
filter(...)
   ↓
filter object
   ↓
list(...)
   ↓
[matching elements]

==============================================================================
------------------------------------------------------------------------------
==============================================================================

13. filter() kab appropriate hai?

* Ab tumhara main question: "When appropriate?"

✅ filter() use karo jab:

------------------------------------------------------------------------------

1. Sirf kuch elements select karne hain:

numbers = [1, 2, 3, 4, 5, 6]
even = list(filter(lambda x: x % 2 == 0, numbers))

------------------------------------------------------------------------------

2. Condition based selection karni hai

students = [...]

Suppose marks:
--------------
marks = [35, 80, 42, 90, 25, 70]

Passing students ke marks:
--------------------------
passed = list(filter(lambda mark: mark >= 40, marks))

Result:
-------
[80, 42, 90, 70]

------------------------------------------------------------------------------

3. Data mein unwanted values remove karni hain

Example:
--------
numbers = [10, 0, 20, 0, 30]

Zero remove:
------------
result = list(filter(lambda x: x != 0, numbers))

Result:
-------
[10, 20, 30]

------------------------------------------------------------------------------

4. Search/selection type operation hai

Suppose:
--------
products = [
    {"name": "Laptop", "price": 50000},
    {"name": "Phone", "price": 20000},
    {"name": "TV", "price": 40000}
]

Sirf ₹30,000 se expensive products:
-----------------------------------
expensive = list(
    filter(lambda product: product["price"] > 30000, products)
)

Result:
-------
[
    {"name": "Laptop", "price": 50000},
    {"name": "TV", "price": 40000}
]

* Ye actual programming mein kaafi useful pattern hai.

==============================================================================

14. filter() kab use nahi karna?

* Agar tumhe har item ko modify/transform karna hai, toh map() better hai.

Example:
--------
numbers = [1, 2, 3, 4]
list(map(lambda x: x * 2, numbers)) // Har number ko double karna hai:

* filter() yahan wrong tool hai because tum kisi item ko select/reject 
  nahi kar rahe.

==============================================================================

15. Ek combined example — filter() + map()

Ab ek interesting example:
--------------------------
numbers = [1, 2, 3, 4, 5, 6]

Requirement:
------------
* Pehle even numbers nikalo, phir unko square karo.

<------------------------------------------------------->

* Yahan do operations hain:

Step 1 — Filter
---------------
Even numbers:

=> list(filter(lambda x: x % 2 == 0, numbers))

Result:
-------
[2, 4, 6]

<------------------------------------------------------->

Step 2 — Map
------------
Ab square:

=> list(map(lambda x: x * x, [2, 4, 6]))

Result:
-------
[4, 16, 36]

<------------------------------------------------------->

So conceptually:

Original:
[1, 2, 3, 4, 5, 6]

       FILTER
          ↓
[2, 4, 6]

        MAP
          ↓
[4, 16, 36]

<------------------------------------------------------->

Ye distinction bahut powerful hai:
----------------------------------
1. Filter decides "kaun rahega?"
2. Map decides "jo rahega uske saath kya karna hai?"

==============================================================================

🧠 Final cheat sheet
--------------------

| Tool       | Kaam                                          | Example             |
| ---------- | --------------------------------------------- | ------------------- |
| `map()`    | Har item ko transform karta hai               | `[1,2,3] → [2,4,6]` |
| `filter()` | Condition ke basis par items select karta hai | `[1,2,3,4] → [2,4]` |
| `map()`    | Output generally same number of items         | 4 → 4               |
| `filter()` | Output items kam ho sakte hain                | 4 → 2               |
| `map()`    | "Har item ko change karo"                     | `x * 2`             |
| `filter()` | "Check karke rakho/hatayo"                    | `x > 10`            |

==============================================================================

Ek line mein yaad rakho:
------------------------
MAP     → Transform
FILTER  → Select

Aur jab bhi code dekho:
-----------------------
filter(lambda x: CONDITION, collection)

mentally bolo:
--------------
"Collection ke har x ko condition mein check karo; 
 True wale rakh do, False wale hata do."

==============================================================================

**IMP CONCEPT**

* Isko ek diagram se lock kar lo

numbers = [1, 2, 3, 4, 5, 6]

             filter()
                │
                │
        function = is_even
                │
                ↓
             ┌─────┐
1 ──────────→│     │──→ is_even(1) → False → ❌
2 ──────────→│     │──→ is_even(2) → True  → ✅
3 ──────────→│FILTER──→ is_even(3) → False → ❌
4 ──────────→│     │──→ is_even(4) → True  → ✅
5 ──────────→│     │──→ is_even(5) → False → ❌
6 ──────────→│     │──→ is_even(6) → True  → ✅
             └─────┘
                │
                ↓
             [2, 4, 6]

------------------------------------------------------------------------------

🧠 Sabse important 3 lines:

is_even                  = function ka reference

is_even()                = function call

filter(is_even, numbers) = filter ko function ka reference de rahe ho; 
                           filter khud baad mein har element ko argument 
                           bana kar is_even() call karta hai.

==============================================================================

* There are indeed 2 return statements, but dono alag function 
  ke return hain.

def add(a, b):
    return a + b       # RETURN 1

and

def operate(function):
    return function(10, 20)   # RETURN 2

Flow:
-----
                    operate(add)
                         │
                         ▼
               function = add
                         │
                         ▼
                function(10,20)
                         │
                         ▼
                   add(10,20)
                         │
                  ┌──────┴──────┐
                  │             │
                a=10           b=20
                  │             │
                  └──────┬──────┘
                         ▼
                      a + b
                         │
                         ▼
                  add RETURN 30
                         │
                         ▼
               operate ka expression
               function(10,20)
                         │
                         ▼
                      return 30
                         │
                         ▼
                 operate RETURN 30