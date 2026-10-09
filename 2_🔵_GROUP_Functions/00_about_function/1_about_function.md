1. Function hota kya hai?

* Function ek reusable block of code hota hai jo kisi particular 
  kaam ko karne ke liye banaya jata hai.

Simple example:
---------------
Socho tumhe baar-baar 2 numbers add karne hain.

Function ke bina:
-----------------
a = 10
b = 20
print(a + b)

x = 50
y = 30
print(x + y)

p = 100
q = 200
print(p + q)

Same kaam baar-baar likhna pad raha hai.

<------------------------------------------------------>

Function bana do:
-----------------
def add(a, b):
    return a + b

Ab:

print(add(10, 20))
print(add(50, 30))
print(add(100, 200))

Output:
-------
30
80
300

* Yaani function ka main idea hai: Code ek baar likho → baar-baar use karo.

==============================================================================

2. Function ko real life example se samjho

* Function ko ek machine samjho.

Input
  ↓
[ FUNCTION ]
  ↓
Output

Example:
--------
10 + 20
   ↓
[ add() ]
   ↓
30

* Function ko input diya → function ne kaam kiya → result diya.

<--------------------------------------------------------------->

Jaise calculator mein:
----------------------
2 numbers → calculator → answer

Python mein:
------------
2 numbers → function → answer

==============================================================================

3. Function banate kaise hain?

* Python mein function banane ke liye def keyword use hota hai.

Basic syntax:
-------------
def function_name():
    # code

Example:
--------
def hello():
    print("Hello World")

* Lekin sirf function define karne se woh execute nahi hota.

Usko call karna padta hai:
--------------------------
hello()

Output:
-------
Hello World

==============================================================================

4. Function ke 2 important parts

* Ye bahut important hai:

def hello():
    print("Hello")

Yahan:
------
def    → Python ko bata raha hai ki hum function bana rahe hain.

hello  → Function ka naam.

()     → Parameters yahan aa sakte hain.

:      → Function ka body start.

Aur neeche indentation wala code:
---------------------------------
print("Hello")  → Function ke andar ka kaam.

==============================================================================

5. Function ko call karna

Function banana:
----------------
def hello():
    print("Hello")

Function chalana:
-----------------
hello()

* Isko function calling kehte hain.

<------------------------------------------------->

Example:
--------
def greet():
    print("Good Morning")

greet()
greet()
greet()

Output:
-------
Good Morning
Good Morning
Good Morning

* Ek baar function likha, 3 baar use kar liya.

==============================================================================

6. Function mein input kaise dete hain?

* Yahan aata hai parameter.

Example:
--------
def greet(name):
    print("Hello", name)

Ab:
---
greet("Rahul")

Output:
-------
Hello Rahul

<-------------------------------------------->

Aur:
----
greet("Aman")

Output:
-------
Hello Aman

<-------------------------------------------->

* Yahan name ek parameter hai.

* Aur "Rahul" ek argument hai.

Parameter vs Argument
---------------------
def greet(name):    // name → parameter

greet("Rahul")      // "Rahul" → argument

Simple language mein:
---------------------
Parameter = function banate waqt jo input variable likhte ho.
Argument  = function call karte waqt jo actual value dete ho.

==============================================================================

7. Multiple parameters

* Ek function mein multiple parameters ho sakte hain.

def add(a, b):
    print(a + b)

Call:
-----
add(10, 20)

Output:
-------
30

<-------------------------------------------->

Ek aur:
-------
add(100, 50)

Output:
-------
150

==============================================================================

8. return kya hota hai?

* Ye functions ka bahut important concept hai.

Example:
--------
def add(a, b):
    return a + b

Ab:
---
result = add(10, 20)
print(result)

Output: 30

------------------------------------------------------------------------------

* return ka matlab roughly: Function ka result bahar bhejna.

Difference dekho:
-----------------
# print

def add(a, b):
    print(a + b)

* Ye result ko screen par display karega.

------------------------------------------------------------------------------

# return

def add(a, b):
    return a + b

* Ye result ko function ke bahar available karwa dega.

Isliye:
-------
result = add(10, 20)   // possible hai.

==============================================================================

9. return ko aur clearly samjho

def square(number):
    return number * number

Ab:
---
x = square(5)

Function ne:
------------
5 × 5
↓
25     // return kiya.

* Ab x ke andar: 25 hai.

Isliye:
-------
print(x)

Output: 25

<-------------------------------------------->

Aur directly bhi:
-----------------
print(square(10))

Output: 100

==============================================================================
------------------------------------------------------------------------------
==============================================================================

0. Function ke kitne types hote hain?

**Yahan ek important baat hai:**

* Python mein functions ko alag-alag basis par classify kiya ja 
  sakta hai. Beginner level par commonly tum ye 4 types padhoge:

------------------------------------------------------------------------------

# Type 1 — No parameter, no return

def hello():
    print("Hello")

Call:

hello()

==============================================================================

# Type 2 — Parameter, no return

def greet(name):
    print("Hello", name)

Call:
-----
greet("Rahul")

==============================================================================

# Type 3 — No parameter, return

def get_number():
    return 10

Call:
-----
x = get_number()
print(x)

Output: 10

==============================================================================

# Type 4 — Parameter + return

def add(a, b):
    return a + b

Call:
-----
result = add(10, 20)
print(result)

Output: 30

* Ye 4 classification beginner ke liye sabse useful hai.

==============================================================================
------------------------------------------------------------------------------
==============================================================================

11. Python mein built-in functions bhi hote hain

* Ab ek aur important concept. Abhi tak hum apne functions bana rahe the:

def add(a, b):
    return a + b

. Inhe user-defined functions bolte hain.

==============================================================================

* Lekin Python mein bahut saare functions pehle se available hote hain.
  Inhe built-in functions bolte hain.

Example:
--------
print()
len()
type()
input()
sum()
max()
min()

Example:
--------
name = "Rahul"
print(len(name))

Output: 5

* Yahan len() Python ka built-in function hai.

==============================================================================

12. User-defined function

* Jo function hum khud banate hain:

def multiply(a, b):
    return a * b

--> Ye user-defined function hai.

==============================================================================

13. Built-in function

* Jo Python already provide karta hai:

=> print("Hello")
=> len("Python")
=> type(10)
=> max(10, 20, 30)

--> Ye built-in functions hain.

==============================================================================

14. Default parameter

* Function mein default value bhi de sakte ho.

CODE:
-----
def greet(name="User"):
    print("Hello", name)

greet()  // Agar argument nahi diya:

Output: Hello User

<----------------------------------------------->

* Agar argument diya:

greet("Rahul")

Output: Hello Rahul

<----------------------------------------------->

**IMP**
-------
Matlab: name="User" default value hai.

==============================================================================
------------------------------------------------------------------------------
==============================================================================

15. Keyword arguments

Normally:
---------
def student(name, age):
    print(name, age)

Call:
-----
student("Rahul", 20)

------------------------------------------------------------------------------

* Lekin naam ke saath bhi value de sakte ho:

student(age=20, name="Rahul")

Output:
-------
Rahul 20

--> Isko keyword argument kehte hain.

==============================================================================

16. *args

* Ye thoda advanced concept hai, lekin function ke context mein 
  important hai.

Normally:
---------
def add(a, b):
    return a + b   // Sirf 2 values.

<----------------------------------------------------->

* Lekin agar tumhe pata hi nahi kitni values aayengi?

def add(*numbers):
    return sum(numbers)

Ab:
---
print(add(10, 20))

O/P: 30

<----------------------------------------------------->

Aur:
----
print(add(10, 20, 30, 40))

O/P: 100

<----------------------------------------------------->

Aur:
----
print(add(1, 2, 3, 4, 5))
15

*args ka use variable number of positional arguments ke 
 liye hota hai.

==============================================================================

17. **kwargs
------------

* Ye keyword arguments ke variable number ke liye hota hai.

Example:
--------
def student(**details):
    print(details)

Call:
-----
student(name="Rahul", age=20, city="Indore")

Output kuch aisa:
-----------------
{'name': 'Rahul', 'age': 20, 'city': 'Indore'}

**kwargs generally dictionary-like data provide karta hai.

==============================================================================

18. Lambda function

* Python mein ek chhota anonymous function bhi bana sakte ho:

CODE:
-----
square = lambda x: x * x

Ab:
---
print(square(5))

Output: 25

<---------------------------------------------->

Normal function:
----------------
def square(x):
    return x * x

Lambda:
-------
square = lambda x: x * x

* Lambda ka use generally small/simple functions ke 
  liye hota hai.

==============================================================================

19. Function kaha use hota hai?

* Almost har serious Python program mein functions use hote hain.

* Suppose tum ek banking application bana rahe ho.

Tumhare paas functions ho sakte hain:
-------------------------------------
def check_balance():
    pass

def deposit_money():
    pass

def withdraw_money():
    pass

def transfer_money():
    pass

<------------------------------------------------>

Ya calculator:
--------------
def add():
    pass

def subtract():
    pass

def multiply():
    pass

def divide():
    pass

<------------------------------------------------>

Ya website:
-----------
def login():
    pass

def register():
    pass

def logout():
    pass

<------------------------------------------------>

Ya data science:
----------------
def clean_data():
    pass

def calculate_average():
    pass

def generate_report():
    pass

==============================================================================

20. Functions use karne ka biggest benefit

* Suppose tumhare paas 500 lines ka program hai.

Agar saara code ek hi jagah likh diya:
--------------------------------------
500 lines
↓
samajhna mushkil
↓
debug karna mushkil
↓
reuse mushkil

<------------------------------------------------->

Functions bana do:
------------------
login()
↓
get_data()
↓
clean_data()
↓
calculate()
↓
generate_report()

* Ab program organized ho jata hai, Isko modularity kehte hain.

==============================================================================

21. Ek real example

* Maan lo tum student ka result calculate karna chahte ho.

CODE:
-----
def calculate_total(math, science, english):
    return math + science + english

def calculate_percentage(total):
    return total / 3

total      = calculate_total(80, 90, 70)
percentage = calculate_percentage(total)

print("Total:", total)
print("Percentage:", percentage)

Output:
-------
Total: 240
Percentage: 80.0

------------------------------------------------------------------------------

* Dekha? Humne ek bada kaam ek function mein nahi ghusaya.

* Humne alag-alag responsibilities rakhi:

calculate_total()
        ↓
Total calculate karta hai

calculate_percentage()
        ↓
Percentage calculate karta hai

Yehi good programming practice hai.

==============================================================================

22. Function ke andar function call kar sakte ho ? Bilkul.

CODE:
-----
def square(x):
    return x * x

def calculate(x):
    result = square(x)
    return result + 10

Ab:
---
print(calculate(5))

<--------------------------------------------->

Process:
--------
calculate(5)
     ↓
square(5)
     ↓
25
     ↓
25 + 10
     ↓
35

Output: 35

==============================================================================

23. Function ke andar conditions bhi ho sakti hain:

CODE:
-----
def check_number(num):

    if num > 0:
        return "Positive"

    elif num < 0:
        return "Negative"

    else:
        return "Zero"

Ab:
---
print(check_number(10))

Output: Positive

==============================================================================

24. Function ke andar loop bhi ho sakta hai

CODE:
-----
def print_numbers():
    for i in range(1, 6):
        print(i)

Call:
-----
print_numbers()

<-------------------------------------------------->

Output:
-------
1
2
3
4
5

<-------------------------------------------------->

* Matlab function ke andar tum normal Python code 
  likh sakte ho:

. variables
. if/else
. loops
. lists
. dictionaries
. other functions

etc.

==============================================================================

25. Function ka scope

* Ye bhi important concept hai.

def test():
    x = 10
    print(x)  // Yahan x function ke andar bana hai, Ye local variable hai.

              // test() ke andar x accessible hai.

Lekin:
------
print(x)     // bahar normally x nahi milega, Kyunki x function ke local 
                scope mein hai.

==============================================================================

26. Function ka complete structure

* Ek function ko is tarah imagine karo:

def function_name(parameter1, parameter2):
    
    # function ka kaam
    
    result = parameter1 + parameter2
    
    return result

Call:
-----
answer = function_name(10, 20)

print(answer)

<------------------------------------------------>

Flow:
-----

             FUNCTION
                 ↓
       ┌──────────────────┐
Input →│ parameter1        │
Input →│ parameter2        │
       │                  │
       │ calculation      │
       │                  │
       │ return result    │
       └────────┬─────────┘
                ↓
             Output

==============================================================================

27. Sabse important keywords

* Functions padhte waqt ye terms yaad rakho:

| Term                  | Meaning                              |
| --------------------- | ------------------------------------ |
| `def`                 | Function define karne ke liye        |
| Function name         | Function ka naam                     |
| Parameter             | Function ka input variable           |
| Argument              | Function ko di gayi actual value     |
| `return`              | Result function se bahar bhejna      |
| Call                  | Function ko execute karna            |
| `*args`               | Multiple positional arguments        |
| `**kwargs`            | Multiple keyword arguments           |
| Local variable        | Function ke andar ka variable        |
| Built-in function     | Python ka already available function |
| User-defined function | Jo function hum khud banate hain     |
| Lambda                | Chhota anonymous function            |

==============================================================================

28. Beginner ke liye tumhe kis order mein functions padhne chahiye?

* Main recommend karunga ki abhi lambda, decorators, generators etc.
  mein mat ghuso.

Pehle ye sequence follow karo:
------------------------------
1. Function kya hai
        ↓
2. def
        ↓
3. Function call
        ↓
4. Parameters
        ↓
5. Arguments
        ↓
6. return
        ↓
7. print vs return
        ↓
8. Multiple parameters
        ↓
9. Default parameters
        ↓
10. Keyword arguments
        ↓
11. Local & global scope
        ↓
12. *args
        ↓
13. **kwargs
        ↓
14. Lambda
        ↓
15. Recursion
        ↓
16. Advanced functions

<------------------------------------------------------>

Ek line mein pura concept:
--------------------------
Function Python mein code ka reusable block hai, jo input 
le sakta hai, us input par kaam kar sakta hai aur return 
ke through result de sakta hai.

Sabse basic function:
---------------------
def add(a, b):
    return a + b

Use:
----
result = add(10, 20)
print(result)

Output: 30