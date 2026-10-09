* Bilkul. Isko 3 steps mein samjho:

1. List Comprehension kya hai
2. Filtering kya hai
3. List Comprehension + Filtering kaise karte hain

=================================================================================

# 1. List Comprehension kya hota hai?

* Normally agar hume 1 se 5 tak numbers ki list banani ho:

CODE:
-----
numbers = []

for i in range(1, 6):
    numbers.append(i)

print(numbers)

Output:
-------
[1, 2, 3, 4, 5]

* Ye normal approach hai.

<------------------------------------------------------>

Ab isi ka short version:
------------------------
numbers = [i for i in range(1, 6)]
print(numbers)

Output:
-------
[1, 2, 3, 4, 5]

* Isko List Comprehension kehte hain.

Simple definition:
------------------
List comprehension ek short way hai list banane ka, 
usually loop ka use karke.

=================================================================================

2. Basic Syntax
---------------

List comprehension ka basic syntax:
-----------------------------------
[expression for item in iterable]

Example:
--------
squares = [x * x for x in range(1, 6)]

Isko tod ke samjho:
-------------------
[x * x     for     x      in      range(1, 6)]
   ↓                 ↓              ↓
 kya banana hai    variable       kahan se lena hai

Yani:
-----
x = 1 → 1 * 1 → 1
x = 2 → 2 * 2 → 4
x = 3 → 3 * 3 → 9
x = 4 → 4 * 4 → 16
x = 5 → 5 * 5 → 25

Result:
-------
[1, 4, 9, 16, 25]

=================================================================================

3. Normal for loop vs List Comprehension:
-----------------------------------------

Normal:
-------
numbers = []

for i in range(1, 6):
    numbers.append(i * 2)

<--------------------------------------------------->

List comprehension:
-------------------
numbers = [i * 2 for i in range(1, 6)]

Dono ka result:
---------------
[2, 4, 6, 8, 10]

* Bas comprehension mein code short ho gaya.

=================================================================================

4. Existing List se List Comprehension
--------------------------------------

Maan lo:
--------
numbers = [1, 2, 3, 4, 5]   // Har number ka square chahiye:
squares = [x * x for x in numbers]
print(squares)

Output:
-------
[1, 4, 9, 16, 25]

=================================================================================
---------------------------------------------------------------------------------
=================================================================================

🔥 Ab Filtering samjho
----------------------
Filtering ka matlab hai kisi collection mein se sirf wahi elements 
select karna jo kisi condition ko satisfy karte hain.

Example:
--------
numbers = [1, 2, 3, 4, 5, 6]  // Hume sirf even numbers chahiye.

Normal for loop:
----------------
even = []

for x in numbers:
    if x % 2 == 0:
        even.append(x)

print(even)

Output:
-------
[2, 4, 6]

* Yahan humne filtering ki.

* Kyun? Kyuki humne condition lagayi: x % 2 == 0

* Jo numbers condition satisfy karte hain, sirf unko list mein liya.

=================================================================================
---------------------------------------------------------------------------------
=================================================================================

5. List Comprehension + Filtering 🔥
------------------------------------

* Ab wahi kaam list comprehension se:

CODE:
-----
numbers = [1, 2, 3, 4, 5, 6]
even    = [x for x in numbers if x % 2 == 0]
print(even)

Output:
-------
[2, 4, 6]

Yahi hai: List Comprehension + Filtering

=================================================================================

6. Isko tod kar samjho
----------------------

Code:
-----
[x for x in numbers if x % 2 == 0]

Ismein:
-------
[x        for x in numbers        if x % 2 == 0]
 ↑              ↑                        ↑
 kya lena hai   kahan se lena hai       condition

<----------------------------------------------------->

Process:
--------
numbers = [1, 2, 3, 4, 5, 6]

1 → odd  → ❌
2 → even → ✅
3 → odd  → ❌
4 → even → ✅
5 → odd  → ❌
6 → even → ✅

Result → [2, 4, 6]

=================================================================================

7. Filtering mein if ka position:
---------------------------------

# Dhyan dena:

Sirf normal list comprehension:
-------------------------------
=> [x for x in numbers]

Filtering:
----------
=> [x for x in numbers if condition]  // if end mein aata hai.

Example:
--------
[x for x in numbers if x > 5]

=================================================================================

8. Example: Sirf bade numbers:
------------------------------

CODE:
-----
numbers = [2, 8, 3, 10, 5, 15]
result  = [x for x in numbers if x > 5]
print(result)

Output:
-------
[8, 10, 15]

<--------------------------------------------------->

CODE:
-----
numbers = [10, 15, 20, 25, 30]
result  = [x for x in numbers if x == 20 or x == 30]
print(result)

Output:
-------
[20, 30]

=================================================================================

9. Example: Sirf odd numbers:
-----------------------------

numbers = [1, 2, 3, 4, 5, 6, 7]
odd     = [x for x in numbers if x % 2 != 0]
print(odd)

Output:
-------
[1, 3, 5, 7]

=================================================================================

10. Example: Strings ko filter karna

CODE:
-----
names  = ["Amit", "Rahul", "Ankit", "Rohit", "Raj"]
result = [name for name in names if name.startswith("A")]
print(result)

Output:
-------
['Amit', 'Ankit']

* Yahan numbers nahi, strings ko filter kar rahe hain.

=================================================================================

11. List Comprehension mein filtering + transformation

Ye bahut important hai.

Maan lo:
--------
numbers = [1, 2, 3, 4, 5, 6]

Hume:
-----
sirf even numbers chahiye
aur unka square chahiye

CODE:
-----
numbers = [1, 2, 3, 4, 5, 6]
result  = [x * x for x in numbers if x % 2 == 0]
print(result)

Output:
-------
[4, 16, 36]

<------------------------------------------------->

* Yahan do kaam hue:

Filtering:
----------
if x % 2 == 0  → sirf even numbers

Transformation:
---------------
x * x          → unka square

=================================================================================
---------------------------------------------------------------------------------
=================================================================================

🔥 Iska formula yaad rakho

Simple List Comprehension:
--------------------------
[expression for item in iterable]

<----------------------------------------------->

Filtering:
----------
[expression for item in iterable if condition]

Example:
--------
[x for x in numbers if x > 10]

<----------------------------------------------->

Filtering + Transformation:
---------------------------
[expression for item in iterable if condition]

Example:
--------
[x * 2 for x in numbers if x % 2 == 0]

=================================================================================

# ⚠️ Ek important difference

Ye:
---
[x for x in numbers if x > 5]     // filtering hai.

Lekin ye:
---------
[x * 2 for x in numbers]          // transformation hai.
 
Aur ye:
-------
[x * 2 for x in numbers if x > 5] // filtering + transformation dono hai.

=================================================================================

🧠 Real-world example
---------------------

* Maan lo students ke marks hain:

marks = [45, 78, 32, 90, 66, 25, 88]

<-------------------------------------------------->

* Sirf 60 se zyada marks wale students ke marks:

passed = [mark for mark in marks if mark >= 60]
print(passed)

Output:
-------
[78, 90, 66, 88]

<-------------------------------------------------->

* Ab in marks ko 10 bonus marks dene hain:

bonus = [mark + 10 for mark in marks if mark >= 60]
print(bonus)

Output:
-------
[88, 100, 76, 98]

<-------------------------------------------------->

Yahan:
------
marks
  ↓
condition check
  ↓
>= 60 wale select
  ↓
+10
  ↓
final list

=================================================================================

⭐ Sabse important baat
-----------------------

* List comprehension ko dekhte hi pehle ye identify karo:

[WHAT       for       FROM       if CONDITION]

<--------------------------------------------------------->

Example:
--------
[x * 2 for x in numbers if x > 5]

Isko padho: x × 2 banao, numbers mein se x lekar, lekin 
            sirf tab jab x > 5 ho.

* Bas ye thought process aa gaya to List Comprehension + Filtering 
  easily samajh aa jayega.

<--------------------------------------------------------->

Quick revision
--------------

# Normal
result = []

for x in numbers:
    if x > 5:
        result.append(x * 2)

# List comprehension
result = [x * 2 for x in numbers if x > 5]

Dono ka result same hai.

* List comprehension basically isi type ke code ko compact aur 
  readable banane ka tareeka hai.