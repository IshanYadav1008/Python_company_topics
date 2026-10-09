Tuple kya hota hai?
-------------------
Tuple ek collection/data type hai, jisme hum multiple values 
ko ek hi variable mein store kar sakte hain.

Tuple ko round brackets () mein likhte hain.
--------------------------------------------
numbers = (10, 20, 30, 40)
print(numbers)

Output:
-------
(10, 20, 30, 40)

================================================================================

# List aur Tuple mein main difference

List:
-----
my_list = [10, 20, 30]

Tuple:
------
my_tuple = (10, 20, 30)

--------------------------------------------------------------------------------

* List mutable hoti hai → values change kar sakte ho.

=> my_list[0] = 100

* Tuple immutable hota hai → banne ke baad values change nahi kar sakte.

=> my_tuple[0] = 100   # Error

================================================================================

# Tuple ki important properties

1. Ordered
----------
* Tuple mein values ka order maintain rehta hai.

t = ("A", "B", "C")
print(t[0])

Output:
-------
A

--------------------------------------------------------------------------------

2. Duplicate values allowed:
----------------------------

t = (10, 20, 10, 30)

. Yahan 10 do baar aa sakta hai.

--------------------------------------------------------------------------------

3. Different data types rakh sakte hain:
----------------------------------------

student = ("Rahul", 20, 85.5, True)

--------------------------------------------------------------------------------

4. Immutable
------------
Tuple ki existing value ko directly change nahi kar sakte.

================================================================================
--------------------------------------------------------------------------------
================================================================================

# Tuple ke Methods

* Tuple ke sirf 2 main built-in methods hote hain:

1. count()
----------
* Ye batata hai ki koi value tuple mein kitni baar present hai.

CODE:
-----
numbers = (10, 20, 10, 30, 10)
print(numbers.count(10))

Output: 3

. Matlab 10 tuple mein 3 baar hai.

--------------------------------------------------------------------------------

2. index()

* Ye kisi value ka first index/position batata hai.

CODE:
-----
numbers = (10, 20, 30, 40)
print(numbers.index(30))

Output: 2

. Kyunki indexing 0 se start hoti hai:

10   20   30   40
 ↓    ↓    ↓    ↓
 0    1    2    3

<--------------------------------------------------->

Agar duplicate ho:
------------------
numbers = (10, 20, 30, 20, 40)
print(numbers.index(20))

Output: 1

. index() pehli occurrence ka index return karta hai.

================================================================================

# Tuple ke saath commonly used functions

* Methods ke alawa kuch Python functions bhi bahut useful hain:

len()
-----
Tuple mein kitne elements hain:

t = (10, 20, 30, 40)
print(len(t))

Output: 4

<----------------------------------------------------------->

max()
-----
Sabse badi value:

t = (10, 50, 20, 30)
print(max(t))

Output: 50

<----------------------------------------------------------->

min()
-----
Sabse chhoti value:

t = (10, 50, 20, 30)
print(min(t))

Output: 10

<----------------------------------------------------------->

sum()
-----
Sabhi numbers ka total:

t = (10, 20, 30)
print(sum(t))

Output: 60

================================================================================

⭐ Ek important point
---------------------
* Agar tuple mein sirf ek element hai, to comma lagana zaroori hai:

t = (10,)     # Tuple

Lekin:
------
t = (10)      # Ye integer hai

Check kar sakte ho:
-------------------
print(type((10,)))
print(type((10)))

Output:
-------
<class 'tuple'>
<class 'int'>

================================================================================

Short mein yaad rakho:
----------------------

| Feature                | Tuple                |
| ---------------------- | -------------------- |
| Brackets               | ()                   |
| Ordered                | ✅                   |
| Duplicate              | ✅                   |
| Different data types   | ✅                   |
| Change kar sakte hain? | ❌                   |
| Main methods           | count(), index()     |

* Tuple = ordered + immutable collection.