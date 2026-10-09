1. List kya hoti hai?
---------------------

List ek collection data structure hai jisme hum multiple values 
ko ek hi variable mein store kar sakte hain.

Example:
--------
fruits = ["apple", "banana", "mango"]

* Yahan ek variable fruits mein 3 values store hain.

Agar list na hoti, to humein:
-----------------------------
fruit1 = "apple"
fruit2 = "banana"
fruit3 = "mango"    // aise likhna padta.

List ki wajah se:
-----------------
fruits = ["apple", "banana", "mango"]

kaafi easy ho gaya.

===========================================================================

# List mein different data types ho sakte hain

* Python list mein ek hi type ka data hona zaroori nahi hai.

data = [10, "Rahul", 5.5, True]

Is list mein:
-------------
10      → int
"Rahul" → str
5.5     → float
True    → bool

. sab ek saath hain.

List ke andar list bhi ho sakti hai:
------------------------------------
data = [10, 20, [30, 40]]           // Isko nested list bolte hain.

===========================================================================

# List Ordered hoti hai

* List mein elements ek specific order mein store hote hain.

fruits = ["apple", "banana", "mango"]

Order hai:  apple → banana → mango

Agar print karoge:
------------------
print(fruits)

to same order milega:
---------------------
['apple', 'banana', 'mango']

===========================================================================

# List mein Indexing

* List ka har element ek index number rakhta hai.

Important:
----------
Python mein indexing 0 se start hoti hai.

Example:
--------
fruits = ["apple", "banana", "mango"]

=> print(fruits[0])
Output: apple

=> print(fruits[1])
Output: banana

=> print(fruits[2])
Output: mango

===========================================================================

# Negative Indexing

* Python list mein negative indexing bhi hoti hai.

fruits = ["apple", "banana", "mango"]

| Element | Positive Index | Negative Index |
| ------- | -------------: | -------------: |
| apple   |       0        |       -3       |
| banana  |       1        |       -2       |
| mango   |       2        |       -1       |

Example:
--------
print(fruits[-1])

Output:
-------
mango

===========================================================================

# List Mutable hoti hai

* Ye bahut important concept hai.

* Mutable ka matlab: list banne ke baad uske elements ko change kar sakte ho.

Example:
--------
fruits    = ["apple", "banana", "mango"]
fruits[1] = "orange"
print(fruits)

Output:
-------
['apple', 'orange', 'mango']

. Humne banana ko orange se replace kar diya.

===========================================================================

# List mein Duplicate Values allowed hain

* List mein same value multiple times aa sakti hai.

numbers = [10, 20, 20, 30, 20]  // Ye completely valid hai.
print(numbers)

Output:
-------
[10, 20, 20, 30, 20]

* Ye Set se important difference hai, kyunki set duplicate 
  values ko store nahi karta.

===========================================================================

# List ki length — len()

* List mein kitne elements hain, ye jaanne ke liye len() use karte hain.

fruits = ["apple", "banana", "mango"]
print(len(fruits))

Output: 3

<----------------------------------------->

Example:
--------
numbers = [10, 20, 30, 40, 50]
print(len(numbers))

Output: 5

===========================================================================

# List mein element check karna

* "in" operator se check kar sakte ho ki koi element list 
  mein hai ya nahi.

fruits = ["apple", "banana", "mango"]
print("apple" in fruits)

Output:
-------
True

<---------------------------------------------------->

print("orange" in fruits)

Output:
-------
False

<---------------------------------------------------->

Similarly:
----------
print("apple" not in fruits)

Output: 
-------
False

===========================================================================

# List mein element add karna

* Iske liye mainly append() aur insert() use hote hain.

append()
--------
* append() list ke end mein element add karta hai.

CODE:
-----
fruits = ["apple", "banana"]
fruits.append("mango")
print(fruits)

Output:
-------
['apple', 'banana', 'mango']

<------------------------------------------------->

Ek aur example:
---------------
numbers = [10, 20, 30]
numbers.append(40)
print(numbers)

Output:
-------
[10, 20, 30, 40]

---------------------------------------------------------------------------

insert()
--------
* Agar kisi specific position par element add karna hai, to 
  insert() use karo.

Syntax:
-------
list.insert(index, value)

Example:
--------
fruits = ["apple", "mango"]
fruits.insert(1, "banana")
print(fruits)

Output:
-------
['apple', 'banana', 'mango']

. Yahan banana index 1 par insert hua.

===========================================================================

extend()
--------
* Agar ek list ke multiple elements doosri list mein add karne 
  hain, to extend() useful hai.

CODE:
-----
fruits      = ["apple", "banana"]
more_fruits = ["mango", "orange"]
fruits.extend(more_fruits)

print(fruits)

Output:
-------
['apple', 'banana', 'mango', 'orange']

<----------------------------------------------------------->

# append() vs extend()

. Ye difference bahut important hai.

a = [1, 2]
a.append([3, 4])
print(a)

Output:
-------
[1, 2, [3, 4]]  // Puri list ek single element ban gayi.

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
append → ek item add
extend → multiple items add

===========================================================================

# List se element remove karna

Iske liye mainly:
-----------------
remove()
pop()
del
clear()

. use hote hain.

===========================================================================

# List Slicing

* Slicing ka matlab list ke ek part ko nikalna.

Syntax:
-------
list[start:end]

Example:
--------
numbers = [10, 20, 30, 40, 50]
print(numbers[1:4])

Output:
-------
[20, 30, 40]

Important: start included hota hai, end excluded hota hai.

So: [1:4]

1 → included
2 → included
3 → included
4 → excluded

---------------------------------------------------------------------------

Slicing examples
----------------
numbers = [10, 20, 30, 40, 50]

Starting se:
------------
numbers[:3]
Output: [10, 20, 30]

End tak:
--------
numbers[2:]
Output:[30, 40, 50]

Puri list:
----------
numbers[:]
Output: [10, 20, 30, 40, 50]

---------------------------------------------------------------------------

# Slicing with Step

Syntax:
-------
list[start:end:step]

Example:
--------
numbers = [10, 20, 30, 40, 50]
print(numbers[::2])

Output:
-------
[10, 30, 50]  // Har 2nd element liya.

* Reverse karne ka common method:
---------------------------------
numbers[::-1]

Output: [50, 40, 30, 20, 10]

===========================================================================

List mein Loop
--------------
* List ke elements ko one-by-one access karne ke liye for 
  loop use karte hain.

CODE:
-----
fruits = ["apple", "banana", "mango"]

for fruit in fruits:
    print(fruit)

Output:
-------
apple
banana
mango

* Ye list ke saath bahut common operation hai.

===========================================================================

List Methods
------------
* Python mein list ke bahut useful methods hain:

| Method      | Kaam                           |
| ----------- | ------------------------------ |
| `append()`  | End mein item add              |
| `insert()`  | Specific position par add      |
| `extend()`  | Multiple items add             |
| `remove()`  | Value remove                   |
| `pop()`     | Index/value position se remove |
| `clear()`   | Puri list empty                |
| `index()`   | Value ka index find            |
| `count()`   | Value kitni baar hai           |
| `sort()`    | List sort                      |
| `reverse()` | List reverse                   |
| `copy()`    | List ki copy                   |

---------------------------------------------------------------------------

# List Concatenation

* Do lists ko + se join kar sakte ho.

a = [1, 2, 3]
b = [4, 5, 6]
c = a + b
print(c)

Output:
-------
[1, 2, 3, 4, 5, 6]

---------------------------------------------------------------------------

# List Repetition

. * se list ko repeat kar sakte ho.

numbers = [1, 2]
print(numbers * 3)

Output:
-------
[1, 2, 1, 2, 1, 2]

---------------------------------------------------------------------------

# Nested List

* List ke andar list:

students = [
    ["Rahul", 20],
    ["Aman", 21],
    ["Rohit", 19]
]

Access:
-------
print(students[0])
Output: ['Rahul', 20]

Name:
-----
print(students[0][0])
Output: Rahul

Age:
----
print(students[0][1])
Output: 20

---------------------------------------------------------------------------

# List aur input()

* User se multiple values lene mein list kaafi useful hai.

For example:
------------
numbers = input("Enter numbers: ").split()
print(numbers)

Agar user enter kare:
---------------------
10 20 30 40

to result:
----------
['10', '20', '30', '40']

. Dhyan do: ye strings hain.

<--------------------------------------------------------->

Numbers chahiye to:
-------------------
numbers = list(map(int, input("Enter numbers: ").split()))

Agar input:
-----------
10 20 30 40

to:
---
[10, 20, 30, 40]

===========================================================================

# List ke important characteristics

* Exam/interview ke liye ye points yaad rakho:

Python List:
------------
. Collection data structure hai
. Ordered hoti hai
. Mutable hoti hai
. Duplicates allow karti hai
. Indexing support karti hai
. Negative indexing support karti hai
. Slicing support karti hai
. Different data types store kar sakti hai
. Nested lists ho sakti hain
. Dynamic size hoti hai