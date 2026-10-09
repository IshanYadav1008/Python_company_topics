1. Merge Dictionaries
---------------------

* Merge ka matlab: do ya zyada dictionaries ko combine karke 
                   ek dictionary banana.

Maan lo:
--------
student1 = {
    "name": "Rahul",
    "age": 20
}

student2 = {
    "city": "Indore",
    "course": "Python"
}                         // Hume dono ko combine karna hai.

Method 1: update()
------------------
student1.update(student2)
print(student1)

Output:
-------
{
    'name': 'Rahul',
    'age': 20,
    'city': 'Indore',
    'course': 'Python'
}

<------------------------------------------------------->

Important
---------
* update() original dictionary ko modify karta hai.

=> student1.update(student2)   // Matlab student1 ke andar 
                                  student2 ke key-value 
                                  pairs add ho gaye.

===========================================================================

2. | operator se merge
----------------------

* Python 3.9+ me dictionaries ko | se merge kar sakte ho:

CODE:
-----
student1 = {
    "name": "Rahul",
    "age": 20
}

student2 = {
    "city": "Indore",
    "course": "Python"
}

result = student1 | student2
print(result)

Output:
-------
{
    'name': 'Rahul',
    'age': 20,
    'city': 'Indore',
    'course': 'Python'
}

-----------------------------------------------------------------------------

# Difference

student1.update(student2)     ➡️ student1 modify hota hai.

result = student1 | student2  ➡️ result me new merged dictionary milti hai; 
                                original dictionaries ko directly modify 
                                nahi karta.

===========================================================================

3. Agar same key ho toh?
------------------------

* Ye bahut important hai.

CODE:
-----
student1 = {
    "name": "Rahul",
    "age": 20
}

student2 = {
    "age": 25,
    "city": "Indore"
}

Ab:
---
result = student1 | student2
print(result)

Output:
-------
{
    'name': 'Rahul',
    'age': 25,
    'city': 'Indore'
}

* age dono dictionaries me tha.

* Second dictionary ki value win karti hai.

student1 → age = 20
student2 → age = 25

Merge → age = 25

* Same rule update() me bhi hai:

=> student1.update(student2)  // student2 ki value existing key 
                                 ko overwrite karegi.

===========================================================================
---------------------------------------------------------------------------
===========================================================================

4. Ab Dictionary ko values ke according sort karna
--------------------------------------------------

Maan lo:
--------
marks = {
    "Rahul": 80,
    "Aman": 95,
    "Priya": 70,
    "Neha": 90
}

* Hume marks ke according sort karna hai.

Ascending order
---------------
sorted_marks = dict(sorted(marks.items(), key=lambda x: x[1]))
print(sorted_marks)

Output:
-------
{
    'Priya': 70,
    'Rahul': 80,
    'Neha': 90,
    'Aman': 95
}

===========================================================================

5. Ye code actually kar kya raha hai?

* Ye line thodi complicated lag sakti hai:

=> sorted(marks.items(), key=lambda x: x[1])

Isko todte hain.
----------------

Step 1: marks.items()
---------------------
marks.items()

* Hume key-value pairs deta hai:

('Rahul', 80)
('Aman', 95)
('Priya', 70)
('Neha', 90)

Har item basically: (key, value) hai.

---------------------------------------------------------------------------

Step 2: key=lambda x: x[1]

* Ye Python ko bata raha hai: "Sorting kis cheez ke according karni hai?"

Har pair:
---------
("Rahul", 80)

me:
---
x[0] → "Rahul"
x[1] → 80

. Hume value ke according sort karna hai.

Isliye:
-------
key=lambda x: x[1]

===========================================================================

6. Descending order me sort karna
---------------------------------

* Agar highest marks pehle chahiye:

sorted_marks = dict(
    sorted(marks.items(), key=lambda x: x[1], reverse=True)
)
print(sorted_marks)

Output:
-------
{
    'Aman': 95,
    'Neha': 90,
    'Rahul': 80,
    'Priya': 70
}

<------------------------------------------------------->

Difference:
-----------
reverse=False

ya default:
-----------
70 → 80 → 90 → 95

Ascending.
----------
reverse=True
95 → 90 → 80 → 70   // Descending.

===========================================================================

7. Dictionary ko keys ke according sort karna
---------------------------------------------

* Ye bhi samajh lo.

Agar:
-----
marks = {
    "Rahul": 80,
    "Aman": 95,
    "Priya": 70,
    "Neha": 90
}

Keys ke according sort:
-----------------------
sorted_marks = dict(sorted(marks.items()))

Output:
-------
{
    'Aman': 95,
    'Neha': 90,
    'Priya': 70,
    'Rahul': 80
}

* Yahan alphabetical order me keys sort hui hain.

===========================================================================

8. Values ke according vs Keys ke according:
--------------------------------------------

* Ye difference yaad rakho:

Keys ke according
-----------------
sorted(marks.items())  // Python default me tuple ka first 
                          element yani key dekhega.

Values ke according
-------------------
sorted(marks.items(), key=lambda x: x[1])

* x[1] value ko represent kar raha hai.

===========================================================================

9. Real-world example
---------------------

* Suppose products ke prices hain:

CODE:
-----
products = {
    "Laptop": 50000,
    "Mouse": 500,
    "Keyboard": 1500,
    "Monitor": 12000
}

Cheapest → expensive
--------------------
sorted_products = dict(
    sorted(products.items(), key=lambda x: x[1])
)
print(sorted_products)

Output:
-------
{
    'Mouse': 500,
    'Keyboard': 1500,
    'Monitor': 12000,
    'Laptop': 50000
}

---------------------------------------------------------------------------

Expensive → cheapest
--------------------
sorted_products = dict(
    sorted(products.items(), key=lambda x: x[1], reverse=True)
)

Output:
-------
{
    'Laptop': 50000,
    'Monitor': 12000,
    'Keyboard': 1500,
    'Mouse': 500
}

===========================================================================

🧠 Sabse important cheez
------------------------
* Dictionary sorting ka ye pattern yaad kar lo:

=> dict(sorted(dictionary.items(), key=lambda x: x[1]))

Iska meaning:
-------------
dictionary.items()
       ↓
(key, value) pairs
       ↓
lambda x: x[1]
       ↓
value ko sorting key banao
       ↓
sorted()
       ↓
dict()
       ↓
sorted dictionary

Aur descending:
---------------
=> dict(sorted(dictionary.items(), key=lambda x: x[1], reverse=True))

===========================================================================

Quick cheat sheet
-----------------
# Merge
a.update(b)

# Merge without modifying originals
result = a | b

# Sort by keys
result = dict(sorted(d.items()))

# Sort by values - ascending
result = dict(sorted(d.items(), key=lambda x: x[1]))

# Sort by values - descending
result = dict(sorted(d.items(), key=lambda x: x[1], reverse=True))

Ek important concept: sorted() khud dictionary return nahi karta; 
wo sorted items ki list return karta hai. Isliye hum bahar dict(...) 
lagate hain taaki wapas dictionary mil jaye.