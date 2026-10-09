**Doubt**
tmne bola ki args mai value hum tuple mai as argument pass krte hai 
lekin hum normally bhi toh as tuple hi value pass krte hai function 
call krte time, yaa or bhi tarike hai value as argument pass krne ke 
toh muje batao ??

Answer:
-------
Haan — yahin ek important misunderstanding hai, aur tumne bilkul sahi 
point pakda. 👍

Maine jab bola tha:
-------------------
*args mein values tuple ke form mein collect hoti hain.

--> iska matlab ye nahi tha ki function call karte waqt hume tuple hi 
    pass karna padta hai.

Actually:
---------
def test(*args):
    print(args)

--> mein tum normally individual values pass karte ho:

test(10, 20, 30)

--> Aur Python un values ko andar automatically tuple mein collect kar 
    leta hai:

args = (10, 20, 30)

* Ab isko detail mein samjho.

===============================================================================

1. Normal function mein arguments kaise pass hote hain?

Maan lo:
--------
def add(a, b):
    return a + b

Call:
-----
add(10, 20)

Yahan:
------
10 → a
20 → b

* Python ne tuple nahi banaya.

Conceptually:
-------------
a = 10
b = 20

===============================================================================

2. Hum tuple directly bhi pass kar sakte hain:

Maan lo:
--------
def add(numbers):
    return numbers[0] + numbers[1]

Ab:
---
add((10, 20))

<------------------------------------------------->

* Yahan ek argument pass hua hai:

=> (10, 20)

* Aur numbers ke andar poora tuple aa gaya:

numbers
   ↓
(10, 20)

<------------------------------------------------->

**Important:**

=> add(10, 20)

aur

=> add((10, 20))

same cheez nahi hain.

Pehle wale mein:
----------------
2 arguments
10
20

Dusre wale mein:
----------------
1 argument
(10, 20)

===============================================================================

3. Ab *args ko dekho

CODE:
-----
def test(*args):
    print(args)

Call:
-----
test(10, 20, 30)

<------------------------------------------------------->

* Yahan humne kya pass kiya? 3 individual arguments:

10
20
30

<------------------------------------------------------->

Python kehta hai: "Is function mein *args hai, toh jitne 
                   bhi positional arguments aaye hain, 
                   sabko ek tuple mein collect kar do."

Result:
-------
args = (10, 20, 30)

So:
---
CALL:

test(10, 20, 30)
       ↓
       ↓
Python collects them
       ↓
args = (10, 20, 30)

===============================================================================

4. Ye difference bahut important hai:

Normal parameter:
-----------------
def test(x):
    print(x)

Call:
-----
test((10, 20, 30))

Yahan:
------
x
↓
(10, 20, 30)

* Ek argument diya, jo tuple hai.

-------------------------------------------------------------------------------

*args:
------
def test(*args):
    print(args)

Call:
-----
test(10, 20, 30)

Yahan:
------
args
↓
(10, 20, 30)

* Teen arguments diye aur Python ne automatically tuple bana 
  diya.

* Dono ka output dekhne mein same lag sakta hai, lekin process 
  different hai.

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

5. Ab tumhara main question: aur kaun-kaun se tarike hain?

* Python mein function ko arguments dene ke multiple ways hain.

* Main tumhe important ones ek sequence mein batata hoon.

===============================================================================

Type 1: Positional arguments

Sabse basic.
------------
def student(name, age):
    print(name)
    print(age)

Call:
-----
student("Rahul", 20)

* Yahan position decide karti hai:

"Rahul" → name
20      → age

* Isliye ise positional argument bolte hain.

===============================================================================

6. Keyword arguments

* Yahan hum parameter ka naam explicitly dete hain:

=> student(name="Rahul", age=20) // Ab position matter nahi karti.

Tum:
----
=> student(age=20, name="Rahul") // Ye bhi kar sakte ho.

Result same hoga.
-----------------
name → Rahul
age  → 20

* Isko keyword argument kehte hain.

===============================================================================

7. Default arguments

* Function banate waqt default value de sakte ho:

def student(name, age=18):
    print(name, age)

Ab:
---
student("Rahul")

Output: Rahul 18 // Kyunki age nahi diya, toh Python ne 
                    default 18 use kiya.

Lekin:
------
student("Rahul", 20)

Output: Rahul 20

===============================================================================

8. Multiple positional arguments using *args

Ab:
---
def test(*args):
    print(args)

Call:
-----
test(10, 20, 30, 40)

Arguments:
----------
10
20
30
40

Function ke andar:
------------------
args = (10, 20, 30, 40)

* Yahan *args ka main benefit hai ki arguments ki number 
  fixed nahi hai.

===============================================================================

9. Multiple keyword arguments using **kwargs:

def test(**kwargs):
    print(kwargs)

Call:
-----
test(name="Rahul", age=20, city="Indore")

Function ke andar:
------------------
kwargs = {
    "name": "Rahul",
    "age": 20,
    "city": "Indore"
}

Yaani:
------
*args
↓
multiple positional arguments
↓
tuple


**kwargs
↓
multiple keyword arguments
↓
dictionary

===============================================================================

10. Tuple/list ko argument ke roop mein pass karna

* Ab ek aur important distinction.

Maan lo:
--------
def add(a, b, c):
    return a + b + c

Tumhare paas list hai:
----------------------
numbers = [10, 20, 30]

Agar tum:
---------
add(numbers)  // karoge, ❌ error aayega.

* Kyunki function 3 arguments chahta hai:

a
b
c

* aur tumne sirf 1 argument diya:

numbers

===============================================================================

11. * se list/tuple unpack kar sakte ho:

CODE:
-----
numbers = [10, 20, 30]
add(*numbers)

Python ise approximately:
-------------------------
add(10, 20, 30)           // samjhega.

--> Yahan * ka meaning hai: Collection ko unpack karke individual 
                            positional arguments bana do.

* Ye bahut important hai.

===============================================================================

12. Tuple ke saath bhi:

CODE:
-----
numbers = (10, 20, 30)
add(*numbers)

Ye bhi:
-------
add(10, 20, 30)  // jaisa hai.

--> So * sirf args ke saath nahi hota.

--> Ye function call mein unpacking ke liye bhi use hota hai.

===============================================================================

13. Dictionary ke saath **

Maan lo:
--------
def student(name, age, city):
    print(name, age, city)

Aur:
----
details = {
    "name": "Rahul",
    "age": 20,
    "city": "Indore"
}

Tum:
----
student(**details)  // kar sakte ho.

Python approximately ise:
-------------------------
student(
    name="Rahul",
    age=20,
    city="Indore"
)

--> mein convert karega.

Yahan:
------
**details, dictionary ko keyword arguments mein unpack kar raha hai.

===============================================================================

14. Ab saare types ek jagah

Function:
---------
def demo(a, b=10, *args, **kwargs):
    print(a)
    print(b)
    print(args)
    print(kwargs)

Call:
-----
demo(
    1,
    2,
    3,
    4,
    5,
    name="Rahul",
    city="Indore"
)

-------------------------------------------------------------------------------

Breakdown:
----------
a
↓
1

b
↓
2

args
↓
(3, 4, 5)

kwargs
↓
{
    "name": "Rahul",
    "city": "Indore"
}

* Ye example tumhe positional + default + *args + keyword + **kwargs 
  sab ek saath dikha raha hai.

===============================================================================

15. Lekin ek subtle point

Tumne bola: "hum normally bhi toh as tuple hi value pass karte 
             hai function call karte time"

* Actually normally tuple automatically nahi banta.

Example:
--------
def test(a, b):
    print(a)
    print(b)

Call:
-----
test(10, 20)

<----------------------------------------------------->

Python ke paas:

a = 10
b = 20

hai.

* (10, 20), Tuple nahi bana.

-------------------------------------------------------------------------------

Lekin:
------
def test(*args):
    print(args)

* mein Python explicitly multiple positional arguments ko collect karke:
  (10, 20) banata hai.

--> Yahi *args ka main concept hai.

===============================================================================

16. Ek simple analogy

* Socho tumhare paas ek bag hai.

Normal function:
----------------
def test(a, b):

Tum do cheezein directly do:
----------------------------
🍎 → a
🍊 → b

<---------------------------------------------------------->

*args:
------
def test(*args):

* Tum jitni cheezein do: 🍎 🍊 🍌 🍇 🍉

* Python bolta hai: Sabko ek bag mein collect kar deta hoon."

args
 ↓
(🍎, 🍊, 🍌, 🍇, 🍉)

--> So *args ka matlab "tuple pass karna" nahi hai.

Balki: "Multiple positional arguments ko receive/collect karke 
        tuple bana lena."

===============================================================================

17. Final cheat sheet

| Tarika                | Example            | Function mein kya milta hai? |
| --------------------- | ------------------ | ---------------------------- |
| Positional            | `fun(10, 20)`      | `a=10, b=20`                 |
| Keyword               | `fun(a=10, b=20)`  | `a=10, b=20`                 |
| Default               | `fun(10)`          | Missing value default se     |
| `*args`               | `fun(10,20,30)`    | `args=(10,20,30)`            |
| Tuple as one argument | `fun((10,20,30))`  | One tuple argument           |
| `*` unpacking         | `fun(*(10,20,30))` | `10,20,30` as separate args  |
| `**kwargs`            | `fun(a=10,b=20)`   | `kwargs={"a":10,"b":20}`     |
| `**` unpacking        | `fun(**data)`      | Dict → keyword arguments     |

-------------------------------------------------------------------------------

* Sabse important distinction:

# Tuple as ONE argument
fun((10, 20, 30))

vs

# THREE arguments
fun(10, 20, 30)

vs

# Tuple/list ko todkar THREE arguments
numbers = (10, 20, 30)
fun(*numbers)

* Ye teen lines alag concepts hain. Agar ye samajh aa gaya, 
  toh *args, **kwargs, aur unpacking ka confusion almost 
  khatam ho jata hai.


===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Doubt-2
-------
numbers = [10, 20, 30]
add(*numbers)

tmne bola ki isme Collection ko unpack karke individual positional 
arguments bana do. toh jo individual arguments bane vo list mai 
honge yaa tuple mai ?

or dusra tmne bola ki...
def test(*args):
    print(args)

* mein Python explicitly multiple positional arguments ko collect karke:
  (10, 20) banata hai.

  toh ye (10, 20) usne tuple banaya naa

-------------------------------------------------------------------------------

Answer:
-------

1. add(*numbers) mein kya hota hai?

CODE:
-----
numbers = [10, 20, 30]
add(*numbers)          // Yahan numbers ek list hai: [10, 20, 30]

*numbers ka matlab hai: List ke andar ke elements ko unpack karke 
                        alag-alag positional arguments bana do.

So conceptually:
----------------
add(*numbers)

becomes:
--------
add(10, 20, 30)

<---------------------------------------------------------------->

* Ab important question: 10, 20, 30 list hain ya tuple?

--> Na list, na tuple.

Call ke waqt:
-------------
add(10, 20, 30)  // mein 10, 20, aur 30. Ye 3 separate positional 
                    arguments hain.

* Python ne yahan koi tuple nahi banaya.

So:
---
numbers = [10, 20, 30]
          ↓
       * unpack
          ↓
add(10, 20, 30)
          ↓
   3 individual arguments

===============================================================================

2. Ab def test(*args) dekho

CODE:
-----
def test(*args):
    print(args)

test(10, 20)

* Yahan situation ulta direction mein hai.

Call ke waqt:
-------------
test(10, 20)

* Python ko 2 individual positional arguments mile:

10
20

<---------------------------------------------------------------->

* Ab function ke andar *args bolta hai:

"Jo bhi multiple positional arguments aaye hain, 
 unko collect karke ek tuple bana do."

Therefore:
----------
args = (10, 20)

Aur:
----
print(args)

output:
-------
(10, 20)

* Haan! Yahan Python tuple banata hai. ✅

===============================================================================

# Sabse important difference

--> Dono jagah * hai, lekin direction opposite hai:

* function definition mein → COLLECT

def test(*args):

Meaning:
--------
10, 20, 30
   ↓
COLLECT
   ↓
(10, 20, 30)

* Python multiple positional arguments ko tuple mein 
  collect karta hai.

-------------------------------------------------------------------------------

* function call mein → UNPACK

numbers = [10, 20, 30]
test(*numbers)

Meaning:
--------
[10, 20, 30]
      ↓
   UNPACK
      ↓
10, 20, 30

* Yahan list ke elements individual arguments ban jaate hain.

===============================================================================

Ek complete example
-------------------
def test(*args):
    print(args)

numbers = [10, 20, 30]
test(*numbers)

-------------------------------------------------------------------------------

Ab step-by-step:

Step 1
------
numbers = [10, 20, 30]

--> numbers ek list hai.

-------------------------------------------------------------------------------

Step 2
------
test(*numbers)     // *numbers list ko unpack karega:

test(10, 20, 30)   // Toh aisa ban jayega lekin ye tuple nhi hai.

-------------------------------------------------------------------------------

Step 3
------
* Ab function receive karta hai:

10
20
30

--> Ye abhi 3 separate positional arguments hain.

-------------------------------------------------------------------------------

Step 4
------
Function mein:

=> def test(*args):

*args in 3 arguments ko collect karta hai or 
Tuble mai convert kr deta hai.

args = (10, 20, 30)

-------------------------------------------------------------------------------

Step 5
------
=> print(args)
 
Output: (10, 20, 30)  // Ye Tuple hai.

===============================================================================

Ekdum visual yaad rakho 🧠

CALL TIME
─────────
numbers = [10, 20, 30]

       *
       ↓
[10, 20, 30]
       ↓
10   20   30
└────┬────┘
  separate
  arguments

<--------------------------------------------------------->

FUNCTION TIME
─────────────
10   20   30
└────┬────┘
     ↓
   *args
     ↓
(10, 20, 30)
     ↑
   TUPLE
Isliye golden rule:

<--------------------------------------------------------->

* call ke time       → UNPACK karta hai
* definition ke time → COLLECT karta hai

===============================================================================

# Aur tumhara second observation 100% correct hai:

CODE:
-----
def test(*args):
    print(args)

test(10, 20)

--> mein Python internally multiple positional arguments ko 
    tuple (10, 20) mein collect karta hai.

Lekin:
------
numbers = [10, 20]
test(*numbers)

--> mein pehle list unpack hoti hai → 10, 20 arguments bante 
    hain → phir *args unko dobara tuple (10, 20) mein collect 
    kar leta hai.

--> Yaani ek hi example mein unpack → collect dono ho sakte hain.