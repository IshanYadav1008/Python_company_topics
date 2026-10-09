* Lambda Function kya hota hai?

--> Python mein lambda ek chhota, anonymous (naam-rahit) 
    function hota hai.

Normal function:
----------------
def add(a, b):
    return a + b

Same kaam lambda se:
--------------------
add = lambda a, b: a + b

Ab:
---
print(add(10, 20))

Output: 30

--> Yaani lambda bhi function hi hai, bas usko likhne ka 
    short syntax hai.

================================================================================

1. Normal function vs Lambda

Normal function
---------------
def square(x):
    return x * x

Call:
-----
print(square(5))

Output: 25

--------------------------------------------------------------------------------

Lambda
------
square = lambda x: x * x

Call:
-----
print(square(5))

Output: 25

--> Dono ka result same hai.

================================================================================

2. Lambda ka syntax

Basic syntax:
-------------
lambda arguments: expression

Example:
--------
lambda x: x * 2

Isko tod ke dekho:
------------------
lambda     x       :       x * 2
  ↓        ↓       ↓          ↓
keyword  argument  :       result

For example:
------------
double = lambda x: x * 2

Yahan:
------
. lambda → batata hai lambda function bana rahe hain
. x      → parameter
. :      → parameter aur expression ko separate karta hai
. x * 2  → expression/result

================================================================================

3. Lambda mein return kahan hai ? Ye bahut important hai.

Normal function:
----------------
def add(a, b):
    return a + b

Lambda:
-------
add = lambda a, b: a + b

--> Lambda mein alag se return nahi likhte.

--> lambda a, b: a + b     // mein a + b ka result automatically 
                              return hota hai.

So:
---
add(10, 20)  → 30

================================================================================

4. Lambda ka naam kahan hai?

* Actually lambda function anonymous hota hai, matlab normally 
  iska apna naam nahi hota.

Jab hum:
--------
add = lambda a, b: a + b

* likhte hain, toh add lambda ka naam technically nahi hai; add 
  variable hai jo us function ko refer kar raha hai.

Conceptually:
-------------
add
 ↓
lambda function

--> Isliye lambda ko aksar directly bhi use kar sakte ho.

================================================================================

5. Direct lambda

Example:
--------
print((lambda x: x * 2)(5))

Output:
-------
10

<--------------------------------------------->

Isko step-by-step dekho:
------------------------

(lambda x: x * 2)(5)

<--------------------------------------------->

Pehle function bana:

lambda x: x * 2

<--------------------------------------------->

Phir usko 5 diya:

(5 * 2)

Result: 10

================================================================================

6. Lambda mein multiple parameters bhi ho sakte hain

Jaise normal function:
----------------------
def add(a, b):
    return a + b

Lambda:
-------
add = lambda a, b: a + b

<-------------------------------------------------->

Aur 3 parameters:
-----------------
add = lambda a, b, c: a + b + c
print(add(10, 20, 30))

Output: 60

================================================================================

7. Lambda ki sabse important use — map(), filter(), sorted()

* Lambda ko mostly tab dekhoge jab kisi function ko chhota sa 
  operation/instruction dena ho.

For example:
------------
numbers = [1, 2, 3, 4, 5]  // Har number ka square chahiye.

Lambda:
-------
squares = list(map(lambda x: x * x, numbers))

Result:
-------
[1, 4, 9, 16, 25]

Yahan:
------
lambda x: x * x  // ka matlab: "Jo bhi x mile, uska square kar do."

================================================================================

8. filter() ke saath

Suppose:
--------
numbers = [1, 2, 3, 4, 5, 6]

Sirf even numbers chahiye:
--------------------------
even = list(filter(lambda x: x % 2 == 0, numbers))

Output: [2, 4, 6]

<--------------------------------------------------->

Lambda:
-------
lambda x: x % 2 == 0

* har number ke liye check karta hai:

1 → False
2 → True
3 → False
4 → True
5 → False
6 → True

* Aur filter() True wale elements rakhta hai.

================================================================================

9. sorted() ke saath

* Suppose students hain:

students = [
    ("Rahul", 80),
    ("Aman", 95),
    ("Rohit", 70)
]

* Marks ke basis par sort karna hai:

students.sort(key=lambda x: x[1])

Result:
-------
[
    ("Rohit", 70),
    ("Rahul", 80),
    ("Aman", 95)
]

Yahan:
------
lambda x: x[1]   // ka matlab: Har student tuple mein second 
                               value (marks) ko sorting ke 
                               liye use karo.

================================================================================

10. Lambda ki limitation

* Lambda simple expression ke liye designed hai.

Achha:
------
square = lambda x: x * x

<------------------------------------------------->

Achha:
------
add = lambda a, b: a + b

<------------------------------------------------->

Lekin agar logic bada ho:
-------------------------
def calculate(x):
    if x > 10:
        return x * 2
    else:
        return x + 5

* Toh normal def use karna better hai.

* Lambda ka purpose ye nahi hai ki har 
  function ko one-line bana do.

================================================================================

# Ek important comparison

| Normal Function                   | Lambda                                    |
| --------------------------------- | ----------------------------------------- |
| `def` use hota hai                | `lambda` use hota hai                     |
| Usually naam hota hai             | Anonymous/naam-rahit function             |
| Multiple statements likh sakte ho | Single expression                         |
| `return` explicitly likh sakte ho | Expression automatically return hota hai  |
| Badi logic ke liye better         | Chhoti logic ke liye better               |
| Reusable functions ke liye useful | Short temporary operations ke liye useful |

================================================================================

* Sabse simple definition yaad rakho:

Lambda = ek chhota, one-expression function jisme return alag 
         se nahi likhna padta.

Example:
--------
square = lambda x: x * x

Isko mentally normal function ki tarah dekho:
---------------------------------------------
def square(x):
    return x * x

* Dono ka basic kaam same hai; lambda bas short form hai.