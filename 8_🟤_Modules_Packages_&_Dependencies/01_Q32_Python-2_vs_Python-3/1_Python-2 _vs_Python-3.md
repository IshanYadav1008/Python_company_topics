1. Python 2 vs Python 3
-----------------------

* Python 2 aur Python 3, Python programming language ke do major versions 
  hain.

- Python 2: Purana version, jiska official support 1 January 2020 ko end 
            ho gaya.

- Python 3: Modern version, jo actively maintained hai aur new projects 
            mein use hota hai.

* Developer ke liye important : Aaj tujhe Python 3 seekhna hai. Python 2 ke 
                                differences isliye samajhne hain taaki tu 
                                legacy code ko samajh sake aur interviews 
                                mein version differences explain kar sake.

==============================================================================

2. Important differences at a glance:
-------------------------------------

Feature	             Python 2	                Python 3
-------------------------------------------------------------------------
Print	             print "Hello"	            print("Hello")
Normal division      5 / 2 → 2	                5 / 2 → 2.5
Floor division    	 5 / 2 → 2	                5 // 2 → 2
User input	         raw_input() for strings	input() returns a string
Strings 	         ASCII by default	        Unicode by default
Exception syntax	 except E, e:	            except E as e:
Range	             range() and xrange()	    range()
Current status	     End of life	            Actively maintained
-------------------------------------------------------------------------

* Ab har important difference ko practical examples se samajhte hain.

==============================================================================

3. Difference 1: Print statement vs function:
--------------------------------------------

* print ka use screen par output dikhane ke liye hota hai.

Python 2:
---------
print "Hello World"

Python 3:
---------
print("Hello World")

Output:
-------
Hello World

* Concept: Python 3 mein print() ek function hai, isliye parentheses 
           () use karna zaroori hai.

------------------------------------------------------------------------------

# Real-world example:

username = "Rahul"
print("Welcome", username)

Output:
-------
Welcome Rahul

- Ye user ko welcome message, application status ya debugging information 
  dikhane mein kaam aata hai.

==============================================================================

4. Difference 2: Division / vs //
---------------------------------

* Ye concept humne pehle practice kiya tha.

/ — True division
-----------------
print(7 / 2)

Output:
-------
3.5     // Python 3 mein / division ka result decimal mein bhi deta hai.

------------------------------------------------------------------------------

// — Floor division
-------------------
print(7 // 2)

Output:
-------
3

// result ko neeche ke integer ki taraf floor karta hai. Positive numbers 
   mein ye decimal part hatane jaisa dikhta hai.

------------------------------------------------------------------------------

Ek important example:
---------------------
print(-7 // 2)

Output:
-------
-4

* Ye -3 nahi hai, kyunki floor division negative infinity ki taraf 
  round down karta hai.

------------------------------------------------------------------------------

Real-world example: Shopping app:
---------------------------------
* Maan le customer ke 17 products hain aur ek box mein maximum 5 
  products aa sakte hain. Kitne boxes lagenge?

items = 17
capacity = 5

print(items // capacity)

Output:
-------
3

- Lekin 3 boxes mein sirf 15 products aayenge. Do products bach jayenge, 
  jinhe pack karne ke liye ek aur box chahiye.

------------------------------------------------------------------------------

# Sahi solution: Ceiling division

CODE:
-----
items    = 17
capacity = 5

boxes = (items + capacity - 1) // capacity
print(boxes)

Output:
-------
4

Formula ka logic:
-----------------
1. 17 + 5 - 1 = 21
2. 21 // 5    = 4

------------------------------------------------------------------------------

Ek aur readable option:
-----------------------
import math

items = 17
capacity = 5

boxes = math.ceil(items / capacity)
print(boxes)  # 4

* math.ceil() decimal result ko agle integer tak round up karta hai.

------------------------------------------------------------------------------

* Agar items exactly divide ho jayein?

import math

print(math.ceil(20 / 5))  # 4
print(math.ceil(17 / 5))  # 4

- Dono cases mein sahi number of boxes milta hai.

------------------------------------------------------------------------------

# Production code mein validation bhi karo:

if capacity <= 0:
    raise ValueError("Capacity must be greater than zero")

- Kyunki box ki capacity zero ya negative nahi ho sakti.

Yaad rakh:
----------
- /           → division, decimal result possible.
- //          → floor division.
- math.ceil() → next integer tak round up.
- Real-world logic mein sirf operator nahi, problem ki 
  requirement bhi samajhni hoti hai.

==============================================================================

5. Difference 3: User input
Python mein user se data lene ke liye input function use hota hai.

Python 2:
---------
name = raw_input("Enter your name: ")

Python 3:
---------
name = input("Enter your name: ")

- Dono examples mein user se text liya ja raha hai.

------------------------------------------------------------------------------

# Python 3 mein input() hamesha string return karta hai.

Example:
--------
age = input("Enter your age: ")
print(type(age))

* Agar user 25 enter kare, toh output hoga:
<class 'str'>

------------------------------------------------------------------------------

* Agar number ki tarah calculation karni hai, toh convert karo:

age = int(input("Enter your age: "))
print(age + 1)

- User 25 enter kare toh output 26 hoga.

------------------------------------------------------------------------------

* Developer insight: Input validation zaroori hai, kyunki user abc enter 
                     karega toh int() conversion error dega.

CODE:
-----
try:
    age = int(input("Enter your age: "))
    print(age + 1)
except ValueError:
    print("Please enter a valid integer.")

- Ye real applications mein invalid input handle karne ka basic example 
  hai.

==============================================================================

6. Difference 4: Strings aur Unicode
------------------------------------

* String ka matlab text hota hai.

* Python 2 mein normal strings default roop se ASCII-oriented hoti thi. 
  Unicode text ke liye aksar u"..." syntax use hota tha.

Python 2:
---------
message = u"Namaste"

Python 3:
---------
message = "नमस्ते 👋"print(message)

Output:
-------
नमस्ते 👋

* Python 3 mein str Unicode text represent karta hai. Isse Hindi, emojis 
  aur different languages ke text ke saath kaam karna easy hota hai.

------------------------------------------------------------------------------

* Ek important distinction: Python 3 mein text (str) aur raw binary data 
                            (bytes) alag types hain.

CODE:
-----
text = "Hello"
data = text.encode("utf-8")

print(type(text))
print(type(data))

Output:
-------
<class 'str'>
<class 'bytes'>

* Real-world use : APIs, files, multilingual websites aur user messages 
                   ke saath kaam karte waqt ye difference useful hai

==============================================================================

7. Difference 5: Exception handling
-----------------------------------

* Program run karte waqt error aa sakta hai. Python mein exceptions 
  ko handle karne ke liye try aur except use hote hain.

Python 2:
---------
try:
    result = 10 / 0
except ZeroDivisionError, e:
    print(e)

Python 3:
---------
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(e)

* Output ka message interpreter version ke hisaab se vary kar sakta 
  hai, lekin exception zero se division ke baare mein hoga.

------------------------------------------------------------------------------

* Concept: Python 3 mein as e likhkar exception object ko variable e 
           mein capture karte hain.

Real-world example — invalid input:
-----------------------------------
try:
    number = int("hello")
except ValueError as e:
    print("Invalid number:", e)

* Yahan program ValueError ko handle karta hai, taaki error ko controlled 
  tareeke se deal kiya ja sake.

* Developer tip: Sirf errors ko chhupane ke liye har jagah except Exception 
                 mat likhna. Jis error ko handle karna hai, use specifically 
                 catch karna better hota hai.

==============================================================================

8. Difference 6: range() aur xrange():
--------------------------------------

* Python 2 mein range() aur xrange() dono available the.

- Python 2 ka range() list banata tha.

- Python 2 ka xrange() values ko lazily generate karta tha.

- Python 3 mein range() ek range object deta hai, jo values 
  ko zaroorat par generate karta hai.

Python 3 example:
-----------------
for i in range(5):
    print(i)

Output:
-------
0
1
2
3
4

- Python 3 mein range() poori list pehle se create nahi karta. 
  Ye bade numeric ranges par memory bachane mein helpful hota 
  hai.

------------------------------------------------------------------------------

Agar actual list chahiye:
-------------------------

numbers = list(range(5))
print(numbers)

Output:
-------
[0, 1, 2, 3, 4]

* Real-world use: Repeated operations, loops, indexing aur records 
                  process karne mein range() kaafi common hai.

==============================================================================

9. Python 2 vs Python 3 — aur kya yaad rakhein ?
------------------------------------------------

* Kuch aur differences jo legacy code samajhne mein useful hain:

- Dictionary iteration: Python 2 mein dict.iteritems() available tha. 
                        Python 3 mein aam taur par dict.items() use 
                        hota hai.

- Integer division    : Python 2 mein do integers ka / integer result 
                        deta tha. Python 3 mein / true division karta 
                        hai.

- Compatibility       : Python 2 ke liye likha hua code Python 3 mein 
                        bina changes ke zaroori nahi ki chale.

- Support             : Python 2 end-of-life hai. Python 3 ko use karna 
                        aur supported version par rehna modern development 
                        ke liye important hai.

* Har purane project ko migrate karna simple syntax changes se possible 
  nahi hota; dependencies aur tests bhi check karne padte hain.

==============================================================================

10. Developer ke liye final mental model:
-----------------------------------------

Output
------
- print() screen par information show karta hai.

Calculations
------------
- / normal division, // floor division, aur math.ceil() round up.

Input
-----
- input() text deta hai; calculation ke liye zaroorat par int() 
  ya float() use karo.

Text
----
- Python 3 ka str Unicode text represent karta hai; bytes binary 
  data ke liye hai.

Errors
------
- try/except se expected errors ko properly handle karo.

==============================================================================

Client interview mein kaise explain karna hai ?
-----------------------------------------------

* Agar client ya interviewer poochhe, “What is the difference between 
  Python 2 and Python 3?”, toh apne words mein kuch aise explain kar:

- Python 3 is the modern and actively maintained version of Python. 
  Compared with Python 2, it provides more consistent syntax and 
  improved Unicode handling. For example, Python 3 uses print() as 
  a function, / performs true division, and input() returns a string. 
  Python 2 reached end of life in 2020, so I use Python 3 for new 
  development.

- Is answer ko ratne ki jagah examples ka logic samajh. Follow-up mein 
  interviewer division, strings ya legacy code migration ke baare mein 
  pooch sakta hai.

------------------------------------------------------------------------------

# Quick self-check:
-------------------

* Notes padhne ke baad apni understanding check kar.

1. Python 3 mein 7 / 2 ka result ?            

o/p: 3.5  // Normal division fractional result deta hai.

2. 17 items, 5 per box: minimum boxes ?      
 
o/p: 4    

Correct! — 3 boxes mein 15 items aayenge; bache 2 items ke 
           liye ek aur box chahiye.

3. Python 3 ka input() kya return karta hai ? 

o/p: String

Correct! — Numeric calculations ke liye int() ya float() se 
           convert karna padta hai.

4. Python 3 mein Unicode text ka example ?    

o/p: message = 'नमस्ते'

Correct! — Python 3 ki str type Unicode text support karti hai.