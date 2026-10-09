# Python list ke 11 methods hote hain:

1. append()
2. extend()
3. insert()
4. remove()
5. pop()
6. clear()
7. index()
8. count()
9. sort()
10. reverse()
11. copy()

===============================================================================

1. append()
-----------

* List ke end mein ek element add karta hai.

Syntax
------
list.append(value)

<-------------------------------------------------->

Example
-------
fruits = ["apple", "banana"]
fruits.append("mango")
print(fruits)

Output:
-------
['apple', 'banana', 'mango']

<-------------------------------------------------->

Important
---------
* append() sirf ek object add karta hai.

numbers = [1, 2]
numbers.append([3, 4])
print(numbers)

Output:
-------
[1, 2, [3, 4]]

* Yaani [3, 4] ek single element ban gaya.

Result:
-------
[10, 30, 20, 40]

<-------------------------------------------------->

"Pehli baar" ka matlab: List ke beginning se search karte 
                        hue jo matching value sabse pehle 
                        milegi, wahi remove hogi.

* Ye first occurrence kehlata hai.

===============================================================================

2. extend()
-----------

* Ek iterable ke saare elements list mein add karta hai.

Example
-------
numbers = [1, 2]
numbers.extend([3, 4, 5])
print(numbers)

Output:
-------
[1, 2, 3, 4, 5]

<---------------------------------------------->

append() vs extend()
--------------------

a = [1, 2]
a.append([3, 4])
print(a)

Output:
-------
[1, 2, [3, 4]]

<---------------------------------------------->

Lekin:
------
a = [1, 2]
a.extend([3, 4])
print(a)

Output:
-------
[1, 2, 3, 4]

Yaad rakho:
-----------
append() → ek item
extend() → multiple items

===============================================================================

3. insert()
-----------

* List ke specific index par element insert karta hai.

Syntax
------
list.insert(index, value)

Example
-------
fruits = ["apple", "mango"]
fruits.insert(1, "banana")
print(fruits)

Output:
-------
['apple', 'banana', 'mango']

* Yahan "banana" index 1 par insert hua.

<---------------------------------------------->

Beginning mein insert:
----------------------
fruits = ["banana", "mango"]
fruits.insert(0, "apple")
print(fruits)

Output:
-------
['apple', 'banana', 'mango']

===============================================================================

4. remove()
-----------
* List mein jo value pehli baar milti hai, usko remove karta hai.

Example
-------
fruits = ["apple", "banana", "mango"]
fruits.remove("banana")
print(fruits)

Output:
-------
['apple', 'mango']

<----------------------------------------------->

# Python list ko left se right check karega:

Index:     0    1    2    3    4
Value:    10   20   30   20   40
                ↑         ↑
              20         20

Python sabse pehle index 1 par 20 dekhta hai.

Isliye index 1 wala 20 remove hoga.

------------------------------------------------------------------------------

Duplicate values
----------------
numbers = [10, 20, 20, 30]
numbers.remove(20)
print(numbers)

Output:
-------
[10, 20, 30]

* Sirf first matching 20 remove hua.

<----------------------------------------------->

⚠️ Agar value list mein nahi hai:
--------------------------------

=> numbers.remove(50)  // to ValueError aayega.

===============================================================================

5. pop()
--------
* List se element remove karta hai aur removed element return bhi karta hai.

Index ke saath
--------------
fruits = ["apple", "banana", "mango"]
x      = fruits.pop(1)
print(x)
print(fruits)

Output:
-------
banana
['apple', 'mango']

<----------------------------------------------->

Index na do
-----------
fruits = ["apple", "banana", "mango"]
fruits.pop()
print(fruits)

Output:
-------
['apple', 'banana']

. Default mein last element remove hota hai.

<----------------------------------------------->

remove() vs pop()
-----------------
remove(value) → value ke basis par remove
pop(index)    → index ke basis par remove
remove(value) → first element remove
pop()         → last element remove

===============================================================================

6. clear()
----------
* List ke saare elements remove kar deta hai.

Example
-------
numbers = [10, 20, 30]
numbers.clear()
print(numbers)

Output:
-------
[]

* List exist karti hai, bas empty ho gayi.

===============================================================================

7. index()
----------
* Kisi value ka first matching index return karta hai.

Example
-------
fruits = ["apple", "banana", "mango"]
print(fruits.index("banana"))

Output:
-------
1

-------------------------------------------------------------------------------

Duplicate values
----------------
numbers = [10, 20, 30, 20, 40]
print(numbers.index(20))

Output:
-------
1

* First 20 ka index return hoga.

<----------------------------------------------->

Range bhi de sakte ho
---------------------
numbers = [10, 20, 30, 20, 40]
print(numbers.index(20, 2))

Output:
3

* Yahan search index 2 se start hua.

<----------------------------------------------->

Isko samjho:
------------
             ↓    ↓
numbers.index(20, 2)
                  ↑
                  search yahan se

index() ka basic syntax hai:
----------------------------
=> list.index(value, start)

Toh:
----
numbers.index(20, 2)

ka matlab:
----------
20 ko search karo, lekin index 2 se search start karo.

-------------------------------------------------------------------------------

index(20, 2)
------------
Ab Python ko bol rahe ho:

* "20 ko dhundo, but index 0 aur 1 ko ignore karo. 
   Index 2 se search start karo."

To:
---
Index:     0    1    2    3    4
Value:    10   20   30   20   40
                     ↓    ↑
                   start  20

Search:
-------
index 2 → 30 ❌
index 3 → 20 ✅

Isliye:
-------
print(numbers.index(20, 2))

Output:
-------
3

<----------------------------------------------->

(20, 2) ko simple language mein yaad rakho:
-------------------------------------------
numbers.index(20, 2)
        ↑   ↑
        |   |
      kya  kahan se search

20 → kya search karna hai
2  → kahan se search start karna hai

**Important:**
--------------
start ka matlab index number hai, value nahi.

===============================================================================

8. count()
----------
* Kisi value ki list mein kitni occurrences hain, ye batata hai.

Example
-------
numbers = [10, 20, 20, 30, 20]
print(numbers.count(20))

Output:
-------
3

<----------------------------------------------->

Another example
---------------
fruits = ["apple", "banana", "apple", "mango"]
print(fruits.count("apple"))

Output:
-------
2

===============================================================================

9. sort()
---------

* List ko sort karta hai.

Ascending order
---------------
numbers = [50, 10, 40, 20, 30]
numbers.sort()
print(numbers)

Output:
-------
[10, 20, 30, 40, 50]

<----------------------------------------------->

Descending order
----------------
numbers = [50, 10, 40, 20, 30]
numbers.sort(reverse=True)
print(numbers)

Output:
-------
[50, 40, 30, 20, 10]

<----------------------------------------------->

Strings
-------
names = ["Rohit", "Aman", "Rahul", "Karan"]
names.sort()
print(names)

Output:
-------
['Aman', 'Karan', 'Rahul', 'Rohit']

<----------------------------------------------->

Important
---------
* sort() original list ko modify karta hai.

numbers = [3, 1, 2]
result = numbers.sort()
print(result)

Output:
-------
None

* Lekin numbers change ho chuki hai:

=> print(numbers)

Output:
-------
[1, 2, 3]

===============================================================================

10. reverse()
-------------
* List ke elements ka current order reverse karta hai.

Example
-------
numbers = [1, 2, 3, 4, 5]
numbers.reverse()
print(numbers)

Output:
-------
[5, 4, 3, 2, 1]

<----------------------------------------------->

Important difference
--------------------
reverse() sorting nahi karta.

Example:
--------
numbers = [30, 10, 20]
numbers.reverse()
print(numbers)

Output:
-------
[20, 10, 30]

* Sirf existing order ulta hua.

===============================================================================

11. copy()
----------
* List ki shallow copy banata hai.

Example
-------
numbers = [10, 20, 30]
new_numbers = numbers.copy()
print(new_numbers)

Output:
-------
[10, 20, 30]

<----------------------------------------------->

Ab dono separate lists hain:
----------------------------
numbers     = [10, 20, 30]
new_numbers = numbers.copy()
new_numbers.append(40)
print(numbers)
print(new_numbers)

Output:
-------
[10, 20, 30]
[10, 20, 30, 40]

* Original list change nahi hui.

--------------------------------------------------------------------------------

🔥 copy() kyun important hai?
-----------------------------
Ye dekho:

a = [1, 2, 3]
b = a

* Yahan b independent copy nahi hai. Dono same list object 
  ko refer karte hain.

b.append(4)
print(a)

Output:
-------
[1, 2, 3, 4]

--------------------------------------------------------------------------------

Lekin:
------
a = [1, 2, 3]
b = a.copy()
b.append(4)
print(a)
print(b)

Output:
-------
[1, 2, 3]
[1, 2, 3, 4]

* Isliye jab actual copy chahiye, copy() useful hai.

===============================================================================

📌 Saare List Methods — Quick Revision
--------------------------------------

| Method      | Kaam                   | Example            |
| ----------- | ---------------------- | ------------------ |
| `append()`  | End mein 1 item add    | `a.append(5)`      |
| `extend()`  | Multiple items add     | `a.extend([5, 6])` |
| `insert()`  | Specific index par add | `a.insert(1, 5)`   |
| `remove()`  | Value remove           | `a.remove(5)`      |
| `pop()`     | Index se remove        | `a.pop(1)`         |
| `clear()`   | Sab remove             | `a.clear()`        |
| `index()`   | Value ka index         | `a.index(5)`       |
| `count()`   | Occurrences count      | `a.count(5)`       |
| `sort()`    | Sort                   | `a.sort()`         |
| `reverse()` | Order reverse          | `a.reverse()`      |
| `copy()`    | Copy create            | `b = a.copy()`     |

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

# Ek important distinction: Methods vs Functions

Ye bhi clear rakho.

List methods
------------
numbers.append(10)
numbers.remove(10)
numbers.sort()

. Ye list ke methods hain.

--------------------------------------------------------------------------------

Built-in functions
------------------
len(numbers)
max(numbers)
min(numbers)
sum(numbers)
sorted(numbers)

. Ye Python built-in functions hain, list methods nahi.

===============================================================================

* Method basically ek function hi hota hai, lekin jo kisi object/class
  se associated hota hai.

Beginner level par tum ise aise samjho:
---------------------------------------
Function → independently call ho sakta hai
Method   → kisi object ke through call hota hai

--------------------------------------------------------------------------------

# Function

Example:
--------
len(numbers)   // Yahan len() ek built-in function hai.

. Ye independently call ho raha hai: len(numbers)

<------------------------------------------------------->

# Method

Example:
--------
numbers.append(50)

Yahan:
------
numbers → object
append  → method

* append() specifically list object ke saath associated hai.

Isliye hum:
-----------
numbers.append(50)  // likhte hain.

Na ki:
------
append(numbers, 50)