🔹 Set kya hota hai?
--------------------

* Set ek collection data type hai jisme unique values store hoti hain.

Set ko {} curly brackets mein likhte hain.
------------------------------------------
numbers = {10, 20, 30, 40}
print(numbers)

Output: {10, 20, 30, 40}

<------------------------------------------------------------>

# Sabse important baat

* Set mein duplicate values automatically remove ho jaati hain.

numbers = {10, 20, 10, 30, 20}
print(numbers)

Output: {10, 20, 30}

Isliye: Set = Unique elements ka collection

=============================================================================

🔹 Set ki properties
--------------------

1. Duplicate allowed nahi hain:

CODE:
-----
a = {1, 2, 2, 3, 3, 3}
print(a)

Output: {1, 2, 3}

-----------------------------------------------------------------------------

2. Set unordered hota hai

* Set mein elements ka fixed index/order nahi hota.

Isliye ye nahi kar sakte:
------------------------
a = {10, 20, 30}
print(a[0])   # Error

-----------------------------------------------------------------------------

3. Set mutable hota hai

* Set banne ke baad usme elements add/remove kar sakte ho.

a = {10, 20, 30}
a.add(40)
print(a)

O/P: {40, 10, 20, 30}

-----------------------------------------------------------------------------

4. Set mein indexing nahi hoti

a = {10, 20, 30}
# a[0] ❌

=============================================================================

# 🔥 Set ke Methods

* Set ke kaafi methods hain. Inko categories mein samjho.

1. add()
--------
* Set mein ek element add karta hai.

a = {10, 20, 30}
a.add(40)
print(a)

Output:
-------
{40, 20, 30, 10}

<------------------------------------------------------------->

# Set unordered collection hai.

Isliye output aisa bhi aa skta hai:

Output:
-------
a = {10, 20, 30, 40}

Toh iska ka matlab ye nahi hai ki Python hamesha 10 → 20 → 30 → 40 
ke order mein print karega.

* Set ka main purpose hai unique values rakhna, order maintain karna 
  nahi.

-----------------------------------------------------------------------------

2. update()
-----------
* Set mein multiple elements add karta hai.

a = {10, 20}
a.update([30, 40, 50])
print(a)

Output:
-------
{10, 20, 30, 40, 50}

=============================================================================

🔴 Elements Remove Karne Wale Methods:
--------------------------------------

3. remove()
-----------
* Set se particular element remove karta hai.

a = {10, 20, 30}
a.remove(20)
print(a)

Output: {10, 30}

* ⚠️ Agar element set mein nahi hai, to remove() KeyError deta hai.

a.remove(50)  // Error
    
-----------------------------------------------------------------------------

4. discard()
------------
* Ye bhi element remove karta hai.

* Difference ye hai ki element nahi mila to error nahi deta.

a = {10, 20, 30}
a.discard(50)
print(a)

Output: {10, 20, 30}

remove() vs discard()
---------------------
remove()   → element nahi mila → Error ❌
discard()  → element nahi mila → No Error ✅

-----------------------------------------------------------------------------

5. pop()
--------
* Set se ek random/arbitrary element remove karke return karta hai.

a = {10, 20, 30}
x = a.pop()
print(x)
print(a)

* Kaunsa element remove hoga, is par depend nahi karna chahiye, 
  kyunki set unordered hai.

-----------------------------------------------------------------------------

6. clear()
----------
* Set ke saare elements remove kar deta hai.

a = {10, 20, 30}
a.clear()
print(a)

Output:
-------
set()

=============================================================================

🟢 Set Operations

* Ye Set ka sabse important part hai.

Maan lo:
--------
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}

-----------------------------------------------------------------------------

7. union()
----------
* Dono sets ke saare unique elements deta hai.

A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
print(A.union(B))

Output: {1, 2, 3, 4, 5, 6}

Short syntax:
-------------
print(A | B)

-----------------------------------------------------------------------------

8. intersection()
-----------------
* Dono sets mein jo elements common hain, woh deta hai.

A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
print(A.intersection(B))

Output: {3, 4}

Short syntax:
-------------
print(A & B)

-----------------------------------------------------------------------------

9. difference()
---------------
* Jo elements A mein hain lekin B mein nahi hain, woh deta hai.

A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
print(A.difference(B))

Output: {1, 2}

Short syntax:
-------------
print(A - B)

<----------------------------------------------->

⚠️ Direction important hai:
--------------------------

--> A - B

aur

--> B - A

same nahi hote.

A - B = {1, 2}
B - A = {5, 6}

-----------------------------------------------------------------------------

10. symmetric_difference()
--------------------------
* Jo elements sirf A ya sirf B mein hain, common elements nahi.

A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
print(A.symmetric_difference(B))

Output:
-------
{1, 2, 5, 6}

Short syntax:
-------------
print(A ^ B)

=============================================================================

🟡 Set Relationship Methods:
----------------------------

11. issubset()

* Check karta hai ki kya ek set ke saare elements doosre set mein hain.

A = {1, 2}
B = {1, 2, 3, 4}
print(A.issubset(B))

Output: True

* Matlab: A, B ke andar completely present hai.

-----------------------------------------------------------------------------

12. issuperset()

* Check karta hai ki kya ek set mein doosre set ke saare 
  elements present hain.

A = {1, 2, 3, 4}
B = {1, 2}
print(A.issuperset(B))

Output:
-------
True

-----------------------------------------------------------------------------

13. isdisjoint()
----------------
* Check karta hai ki dono sets mein koi common element hai ya nahi.

A = {1, 2, 3}
B = {4, 5, 6}
print(A.isdisjoint(B))

Output:
-------
True

. Kyunki koi common element nahi hai.

<----------------------------------------------->

Agar:
-----
A = {1, 2, 3}
B = {3, 4, 5}
print(A.isdisjoint(B))

Output:
-------
False

* Kyunki 3 common hai.

=============================================================================

🔵 intersection_update()
------------------------
* Intersection nikalta hai aur original set ko update bhi kar deta hai.

A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
A.intersection_update(B)
print(A)

Output:
-------
{3, 4}

=============================================================================

🔵 difference_update()
----------------------
* Difference nikal kar original set ko update karta hai.

A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
A.difference_update(B)
print(A)

Output:
-------
{1, 2}

=============================================================================

🔵 symmetric_difference_update()
--------------------------------
* Symmetric difference nikal kar original set ko update karta hai.

A = {1, 2, 3, 4}
B = {3, 4, 5, 6}
A.symmetric_difference_update(B)
print(A)

Output:
-------
{1, 2, 5, 6}

=============================================================================

📌 Saare important Set methods ek jagah
---------------------------------------

| Method                          | Kaam                               |
| ------------------------------- | ---------------------------------- |
| `add()`                         | Ek element add                     |
| `update()`                      | Multiple elements add              |
| `remove()`                      | Element remove, nahi mila to error |
| `discard()`                     | Element remove, error nahi         |
| `pop()`                         | Ek arbitrary element remove        |
| `clear()`                       | Saare elements remove              |
| `union()`                       | Dono sets ke unique elements       |
| `intersection()`                | Common elements                    |
| `difference()`                  | Sirf first set ke elements         |
| `symmetric_difference()`        | Common ko chhodkar elements        |
| `issubset()`                    | Check subset                       |
| `issuperset()`                  | Check superset                     |
| `isdisjoint()`                  | Check no common elements           |
| `intersection_update()`         | Intersection + update              |
| `difference_update()`           | Difference + update                |
| `symmetric_difference_update()` | Symmetric difference + update      |


🧠 Easy trick
-------------
* Set ke operations ko aise yaad karo:

UNION          → A + B
INTERSECTION   → A aur B mein COMMON
DIFFERENCE     → A mein hai, B mein nahi
SYMMETRIC      → A ya B, but COMMON nahi