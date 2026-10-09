Sabse pehle ek line mein:
-------------------------

*args    → function mein kitne bhi positional arguments lene ke liye.
**kwargs → function mein kitne bhi keyword arguments lene ke liye.

* Ab ekdum zero se samjhte hain.

=============================================================================

1. Normal function mein problem kya hai?

Maan lo:
--------
def add(a, b):
    return a + b

add(10, 20)      // Ab tum ye kar sakte ho.
add(10, 20, 30)  // Lekin agar tum ye karoge, error aayega.

* Kyunki function sirf 2 parameters expect kar raha hai:

a
b

* Lekin tumne 3 values de di:

10
20
30

* Toh question: Agar mujhe pata hi nahi ki function ko 
                kitne arguments milenge, toh kya karun ?

--> Yahin *args ka use hota hai.

=============================================================================

2. *args kya hai?

Example:
--------
def add(*args):
    print(args)

Ab:
---
add(10, 20)     
Output: (10, 20)

<------------------------------------------------------------>

Aur:
----
add(10, 20, 30)
Output: (10, 20, 30)

<------------------------------------------------------------>

Aur:
----
add(1, 2, 3, 4, 5)
Output: (1, 2, 3, 4, 5)

* Yaani *args function ko variable number of positional 
  arguments accept karne deta hai.

=============================================================================

3. args actually kya hota hai?

**Ye bahut important hai.**

CODE:
-----
def test(*args):
    print(args)

Agar:
-----
test(10, 20, 30)

toh internally:
---------------
args = (10, 20, 30)  // args ek tuple hota hai.

<------------------------------------------------------------>

Matlab:
-------
def test(*args):
    print(type(args))

Output:
-------
<class 'tuple'>

Isliye yaad rakho: *args → multiple positional arguments → tuple 
                   ke form mein collect hote hain.

=============================================================================

4. *args ka naam args hi hona zaroori hai ? Nahi.

Ye:
---
def test(*args):
    print(args)

aur:
----

def test(*numbers):
    print(numbers)

--> dono valid hain.

<----------------------------------------------->

Example:
--------
def add(*numbers):
    print(numbers)

add(10, 20, 30)

Output:
-------
(10, 20, 30)

<----------------------------------------------->

--> Actually * important hai.

--> Naam tum kuch bhi rakh sakte ho:

*args
*numbers
*values
*items

--> Lekin convention ke according hum usually: *args likhte hain.

=============================================================================

5. *args ka practical example

Ab ek useful function banao:
----------------------------
def add(*args):
    total = 0

    for number in args:
        total = total + number

    return total

Ab:
---
print(add(10, 20))

Output:
-------
30

<--------------------------------------->

print(add(10, 20, 30))

Output:
-------
60

<--------------------------------------->

print(add(1, 2, 3, 4, 5))

Output:
-------
15

--> Dekho function ko pata hi nahi tha kitne 
    numbers aayenge.

=============================================================================

6. *args ko mentally kaise samjho?

Ye:
---
add(10, 20, 30, 40)

function ke andar roughly:
--------------------------
args
 ↓
(10, 20, 30, 40)   // ban gaya.

Phir:
-----
for number in args: se hum ek-ek value nikal sakte hain.

=============================================================================

7. Normal parameter + *args

* Tum normal parameters ke saath bhi *args use kar sakte ho.

CODE:
-----
def test(name, *args):
    print("Name:", name)
    print("Other values:", args)

Call:
-----
test("Rahul", 10, 20, 30)

Output:
-------
Name: Rahul
Other values: (10, 20, 30)

Yahan:
------
name → "Rahul"
args → (10, 20, 30)

=============================================================================
-----------------------------------------------------------------------------
=============================================================================

8. Ab aata hai **kwargs

* Ab maan lo tum function ko values name ke saath dena chahte ho.

Example:
--------
def student(name, age):
    print(name)
    print(age)

Call:
-----
student(name="Rahul", age=20)

Yahan:
------
name = "Rahul"
age  = 20

--> Ye keyword arguments hain.

<------------------------------------------------------------->

* Lekin agar tumhe pata hi nahi kitne keyword arguments aayenge?

Example:
--------
student(
    name="Rahul",
    age=20,
    city="Indore",
    course="Python"
)

* Aise arbitrary number of keyword arguments accept karne ke liye:

**kwargs, use hota hai.

=============================================================================

9. Basic **kwargs

CODE:
-----
def student(**kwargs):
    print(kwargs)

Ab:
---
student(name="Rahul", age=20)

Output:
-------
{'name': 'Rahul', 'age': 20}

<-------------------------------------------------->

Aur:
----
student(
    name="Rahul",
    age=20,
    city="Indore"
)

Output:
-------
{'name': 'Rahul', 'age': 20, 'city': 'Indore'}

* Notice karo: kwargs ke andar data dictionary ban gaya.

=============================================================================

10. kwargs ka type kya hota hai?

CODE:
-----
def test(**kwargs):
    print(type(kwargs))

Call:
-----
test(name="Rahul", age=20)

Output:
-------
<class 'dict'>

<-------------------------------------------------->

So:
---
*args    → tuple
**kwargs → dictionary

* Ye line pakki yaad kar lo:

*args    → tuple
**kwargs → dictionary

=============================================================================

11. kwargs naam bhi compulsory nahi hai, Bilkul nahi.

Ye:
---
def student(**kwargs):
    print(kwargs)

aur ye:
-------

def student(**details):
    print(details)          // dono valid hain.

<-------------------------------------------------->

Example:
--------
def student(**details):
    print(details)

student(name="Rahul", age=20)

Output:
-------
{'name': 'Rahul', 'age': 20}

* Lekin convention ke according: **kwargs, use karte hain.

=============================================================================

12. args vs kwargs

* Ab main difference:

*args
-----
Values normally : add(10, 20, 30)

Collect         : args = (10, 20, 30)

→ tuple

-----------------------------------------------------------------------------

**kwargs
--------

Values names ke saath: student(name="Rahul", age=20)

Collect:
--------
kwargs = {
    "name": "Rahul",
    "age": 20
}

→ dictionary

=============================================================================

13. Ek table mein
-----------------

|                | `*args`                       | `**kwargs`                 |
| -------------- | ----------------------------- | -------------------------- |
| Full idea      | Variable positional arguments | Variable keyword arguments |
| Data structure | Tuple                         | Dictionary                 |
| Input          | `10, 20, 30`                  | `name="Rahul", age=20`     |
| Example        | `func(10,20)`                 | `func(name="Rahul")`       |
| Inside         | `(10, 20)`                    | `{"name": "Rahul"}`        |

=============================================================================

14. Dono ko ek saath use karna

**Ye bahut important hai.**

CODE:
-----
def student(*args, **kwargs):
    print("Args:", args)
    print("Kwargs:", kwargs)

Call:
-----
student(
    "Rahul",
    20,
    "Python",
    city="Indore",
    course="Programming"
)

Output:
-------
Args: ('Rahul', 20, 'Python')

Kwargs: {
    'city': 'Indore',
    'course': 'Programming'
}

<----------------------------------------------------->

Yaani:
------
"Rahul"      → args
20           → args
"Python"     → args

city="Indore"       → kwargs
course="Programming" → kwargs

=============================================================================

15. Ek bahut simple real-life example:

Socho ek shopping function hai:
-------------------------------
def order(*items, **details):
    print("Items:", items)
    print("Details:", details)

Ab:
---
order(
    "Laptop",
    "Mouse",
    "Keyboard",
    customer="Rahul",
    city="Indore"
)

Function ke andar:
------------------
items
↓
("Laptop", "Mouse", "Keyboard")

Aur:
----
details
↓
{
    "customer": "Rahul",
    "city": "Indore"
}

--> Ye *args aur **kwargs ka ek real use case hai.

=============================================================================

16. * aur ** ka ek aur important use

Ab thoda interesting part.
--------------------------
* sirf function definition mein hi nahi, function call karte 
  waqt bhi use hota hai.

-----------------------------------------------------------------------------

Maan lo:
--------
numbers = [10, 20, 30]

Aur function:
-------------
def add(a, b, c):
    return a + b + c

Normally:
---------
add(10, 20, 30)

<---------------------- ------------------------->

Lekin list already hai:
-----------------------
numbers = [10, 20, 30]

Toh:
----
add(*numbers)   // kar sakte ho.

* Python list ko unpack kar dega:

numbers
   ↓
[10, 20, 30]
   ↓ *
10, 20, 30

=============================================================================

17. ** se dictionary unpack karna

Maan lo:
--------
def student(name, age):
    print(name, age)

Aur:
----
details = {
    "name": "Rahul",
    "age": 20
}

Ab:
---
student(**details)

<---------------------------------------------------->

--> Python internally roughly:

student(name="Rahul", age=20)  // jaisa treat karega.

So:
---
*  → iterable unpacking
** → dictionary/keyword unpacking

=============================================================================

18. *args ko unpacking se confuse mat karna:

* Ye dono related hain, lekin direction opposite hai.

Function definition:
--------------------
def test(*args):

Yahan *args ka matlab: "Jo bhi extra positional arguments aayenge, 
                        unhe collect kar lo."

-----------------------------------------------------------------------------

Function call:
--------------
test(*numbers)

Yahan *numbers ka matlab: "Is collection ko todkar individual 
                           arguments bana do."

-----------------------------------------------------------------------------

So:
---
Definition:

10, 20, 30
   ↓
*args
   ↓
(10, 20, 30)


Call:
-----
(10, 20, 30)
   ↓
*numbers
   ↓
10, 20, 30

=============================================================================

19. **kwargs ke saath bhi same

Definition:
-----------
def student(**kwargs):
    print(kwargs)

* Meaning: Multiple keyword arguments ko dictionary mein collect karo.

-----------------------------------------------------------------------------

Call:
-----
details = {
    "name": "Rahul",
    "age": 20
}

student(**details)

* Meaning: Dictionary ko keyword arguments mein unpack karo.

=============================================================================

20. Ek important syntax rule

* Agar tum function mein sab kuch use kar rahe ho:

Syntax:
-------
def function(a, b, *args, **kwargs):
    pass

* Ye common structure hai:

normal parameters
       ↓
     *args
       ↓
   **kwargs

-----------------------------------------------------------------------------

Example:
--------
def test(name, age, *args, **kwargs):
    print(name)
    print(age)
    print(args)
    print(kwargs)

Call:
-----
test(
    "Rahul",
    20,
    "Python",
    "Coding",
    city="Indore",
    country="India"
)

Result conceptually:
--------------------
name  → Rahul
age   → 20

args  → ("Python", "Coding")

kwargs → {
    "city": "Indore",
    "country": "India"
}

=============================================================================

21. Ek common mistake

Ye:
---
def test(*args, **kwargs):
    print(args)
    print(kwargs)

call karna:
-----------
test(
    name="Rahul",
    age=20
)

mein:
-----
args = ()
kwargs = {
    "name": "Rahul",
    "age": 20
}

Hoga.

-----------------------------------------------------------------------------

Aur:
----
test(10, 20, 30)

mein:
-----
args = (10, 20, 30)
kwargs = {}

Hoga.

* Dono independent hain.

=============================================================================

22. Real-world mein *args aur **kwargs kahan use hote hain?

* Ye especially useful hote hain jab:

1. Function ko flexible banana ho

def add(*numbers):
    return sum(numbers)

-----------------------------------------------------------------------------

2. Wrapper functions

* Advanced Python mein functions ko wrap karte waqt:

def wrapper(*args, **kwargs):
    return original_function(*args, **kwargs)

Ye bahut common pattern hai.

-----------------------------------------------------------------------------

3. Libraries/frameworks

* Python ki libraries mein aise functions milenge jo unknown number 
  of arguments accept karte hain.

-----------------------------------------------------------------------------

4. Decorators

* Jab tum decorators padhoge, *args aur **kwargs bahut frequently 
  dikhenge.

=============================================================================

23. Sabse important example

Is code ko samajh lo:
---------------------
def introduce(name, *skills, **details):
    print("Name:", name)
    print("Skills:", skills)
    print("Details:", details)

Call:
-----
introduce(
    "Rahul",
    "Python",
    "SQL",
    "Git",
    age=20,
    city="Indore"
)

Ab breakdown:
-------------
name
 ↓
"Rahul"

<------------------------------------------------->

skills
 ↓
("Python", "SQL", "Git")

<------------------------------------------------->

details
 ↓
{
    "age": 20,
    "city": "Indore"
}

<------------------------------------------------->

So output:
----------
Name    : Rahul
Skills  : ('Python', 'SQL', 'Git')
Details : {'age': 20, 'city': 'Indore'}

=============================================================================

24. Ekdum short trick

* Bas ye diagram yaad rakho:

                 FUNCTION
                    │
        ┌───────────┴───────────┐
        │                       │
     *args                   **kwargs
        │                       │
   positional              keyword
   arguments               arguments
        │                       │
      tuple                  dict
        │                       │
 (10, 20, 30)       {"name": "Rahul", "age": 20}

-----------------------------------------------------------------------------

Example:
--------
def test(*args, **kwargs):
    print(args)
    print(kwargs)

Call:
-----
test(
    10,
    20,
    30,
    name="Rahul",
    age=20
)

Result:
-------
args
→ (10, 20, 30)

kwargs
→ {'name': 'Rahul', 'age': 20}

-----------------------------------------------------------------------------

Bas ye 4 points yaad rakho:
---------------------------

1. *args    = multiple positional arguments
2. **kwargs = multiple keyword arguments
3. args andar tuple hota hai
4. kwargs andar dictionary hota hai

Aur ek bonus:
-------------
*  → unpack/collect positional
** → unpack/collect keyword