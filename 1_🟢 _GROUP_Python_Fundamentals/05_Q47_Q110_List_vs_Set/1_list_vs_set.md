1. List vs Set
--------------

Sabse pehle basic idea:
-----------------------
List → order important hota hai aur duplicates allowed hote hain.
Set  → unique values chahiye aur duplicates nahi chahiye.

Example
-------
numbers_list = [10, 20, 20, 30, 40]
numbers_set = {10, 20, 20, 30, 40}
print(numbers_list)
print(numbers_set)

Output:
-------
[10, 20, 20, 30, 40]
{10, 20, 30, 40}

* Set ne duplicate 20 hata diya.

==========================================================================

Main differences
----------------

| Feature            | List               | Set   
--------------------------------------------------------------------------
| Syntax             | `[]`               | `{}`
| Ordered collection | ✅ Yes             | ❌ Sequence/order par depend 
                                               nahi karna chahiye 

| Duplicates         | ✅ Allowed         | ❌ Not allowed
| Indexing           | ✅ Yes             | ❌ No
| Mutable            | ✅ Yes             | ✅ Yes  
| `append()`         | ✅                 | ❌   
| `add()`            | ❌                 | ✅  
| `remove()`         | ✅                 | ✅  
| `union()`          | ❌                 | ✅     
| `intersection()`   | ❌                 | ✅         
| Main purpose       | Ordered collection |  Unique collection 

==========================================================================

List me indexing:
-----------------
numbers = [10, 20, 30]
print(numbers[1])

Output: 20

<------------------------------------------->

Set me:
-------
numbers = {10, 20, 30}
print(numbers[1])

❌ Error aayega, kyunki set indexing support 
   nahi karta.

==========================================================================

2. Set ko kab use karein?
-------------------------

Case 1: Duplicate remove karne hain

CODE:
-----
numbers = [10, 20, 20, 30, 30, 40]
unique_numbers = set(numbers)
print(unique_numbers)

Output:
-------
{10, 20, 30, 40}

* Ye Set ka ek bahut common use hai.

--------------------------------------------------------------------------

Case 2: Membership check karna
------------------------------

students = {"Rahul", "Aman", "Priya"}
print("Rahul" in students)

Output:
-------
True

* Set me membership testing generally efficient hoti hai.

==========================================================================
--------------------------------------------------------------------------
==========================================================================

3. Set Types
------------
* Yahan ek important clarification hai: Python me Set ke 2 main built-in 
                                        types samajhne layak hain:

1. set
2. frozenset

--------------------------------------------------------------------------

# 3.1 set

* Normal set mutable hota hai.

CODE:
-----
numbers = {10, 20, 30}  // Tum isme value add kar sakte ho:
numbers.add(40)
print(numbers)

Output me 40 aa jayega.

<---------------------------------------------------------->

* Tum remove bhi kar sakte ho:

=> numbers.remove(20)

So: set = mutable

==========================================================================

4. frozenset

* frozenset basically immutable set hai.

numbers = frozenset([10, 20, 30])

Ab:
---
numbers.add(40)  // ❌ Nahi kar sakte.

Because:
--------
frozenset = immutable

<---------------------------------------------------->

Comparison
----------
set        → mutable
frozenset  → immutable

<---------------------------------------------------->

Normal set:
-----------
a = {10, 20, 30}
a.add(40)

<---------------------------------------------------->

Frozenset:
----------
a = frozenset([10, 20, 30])

* Isko directly modify nahi kar sakte.

==========================================================================

5. Ab Set Operations 🔥
-----------------------

* Set operations bahut important hain.

Maan lo:
--------
A = {1, 2, 3, 4, 5}
B = {4, 5, 6, 7, 8}

* Ab hum in dono ke saath operations karenge.

==========================================================================

6. Union

Meaning: A aur B ke saare unique elements

CODE:
-----
A = {1, 2, 3, 4, 5}
B = {4, 5, 6, 7, 8}
print(A.union(B))

Output:
-------
{1, 2, 3, 4, 5, 6, 7, 8}

<--------------------------------------------->

Operator:
---------
print(A | B)

Same result.

Yaad rakho: UNION = dono ke elements

==========================================================================

7. Intersection

Meaning: Jo elements A aur B dono me common hain

CODE:
-----
print(A.intersection(B))

Output:
-------
{4, 5}

<--------------------------------------------->

Operator:
---------
print(A & B)

Same result.

Yaad rakho: INTERSECTION = common elements

==========================================================================

8. Difference

Meaning: A me hain, lekin B me nahi hain

=> print(A.difference(B))

Output:
-------
{1, 2, 3}

<--------------------------------------------->

Operator:
---------
print(A - B)  // Same result.

<--------------------------------------------->

Lekin dhyan:
------------
print(B - A)

Output:
-------
{6, 7, 8}

<--------------------------------------------->

* Because difference directional hai.

A - B → A me hain, B me nahi
B - A → B me hain, A me nahi

==========================================================================

9. Symmetric Difference
-----------------------

* Ye thoda interesting hai.

Meaning: Jo A ya B me hain, lekin dono me common nahi hain.

=> print(A.symmetric_difference(B))

Output:
-------
{1, 2, 3, 6, 7, 8}  // 4 aur 5 nahi aaye kyunki wo dono 
                       sets me common hain.

Operator:
---------
print(A ^ B)

Same result.

==========================================================================

10. Ek table se samjho
----------------------

Agar:
-----
A = {1, 2, 3, 4, 5}
B = {4, 5, 6, 7, 8}

| Operation | Result              | Meaning                |
| --------- | ------------------- | ---------------------- |
|  A \| B   |  {1,2,3,4,5,6,7,8}  | Sab unique             |
|  A & B    |  {4,5}              | Common                 |
|  A - B    |  {1,2,3}            | A only                 |
|  B - A    |  {6,7,8}            | B only                 |
|  A ^ B    |  {1,2,3,6,7,8}      | Common ko chhodkar sab |

==========================================================================

11. Real-life example
---------------------

* Maan lo 2 classes hain:

python_students = {"Rahul", "Aman", "Priya", "Neha"}
java_students   = {"Aman", "Neha", "Rohit", "Karan"}

Dono courses karne wale students
--------------------------------
python_students & java_students

Output:
-------
{"Aman", "Neha"} // Ye intersection hai.

<------------------------------------------------------>

Python ya Java me enrolled students
-----------------------------------
python_students | java_students

Ye union hai.

--------------------------------------------------------------------------

Sirf Python wale students
-------------------------
python_students - java_students

Output:
-------
{"Rahul", "Priya"}

--------------------------------------------------------------------------

Sirf ek course wale students
----------------------------
python_students ^ java_students

* Ye symmetric difference hai.

==========================================================================

12. Set relationship operations

* Set operations me kuch aur important methods bhi hain.

=> issubset()

* Check karta hai ki ek set ke saare elements doosre set me hain ya nahi.

CODE:
-----
A = {1, 2}
B = {1, 2, 3, 4}
print(A.issubset(B))

Output:
-------
True     // Because A ke 1, 2 dono B me hain.

--------------------------------------------------------------------------

=> issuperset()

* Check karta hai ki doosre set ke saare elements current set me 
  hain ya nahi.

print(B.issuperset(A))

Output:
-------
True

--------------------------------------------------------------------------

=> isdisjoint()

* Check karta hai ki dono sets me koi common element nahi hai.

CODE:
-----
A = {1, 2, 3}
B = {4, 5, 6}
print(A.isdisjoint(B))

Output:
-------
True

* Kyuki koi common element nahi hai.

==========================================================================
--------------------------------------------------------------------------
==========================================================================

13. Set ke important methods

Ab ek jagah important methods dekh lo:
--------------------------------------
add()
update()

remove()
discard()
pop()
clear()

union()
intersection()
difference()
symmetric_difference()

issubset()
issuperset()
isdisjoint()

<------------------------------------------------------>

Aur operators:
--------------
|  → union
&  → intersection
-  → difference
^  → symmetric difference

==========================================================================

🧠 Sabse important memory trick
-------------------------------

* Set operations ko bas is tarah yaad rakho:

A | B   → DONO ke saare unique
A & B   → COMMON
A - B   → A ONLY
B - A   → B ONLY
A ^ B   → COMMON ko hata do

Aur:
----
List → order + duplicates
Set  → unique values

* Ek practical rule: agar tumhe "duplicates nahi chahiye", 
  Set ke baare me socho. Agar tumhe "order/indexing chahiye", 
  List ke baare me socho.