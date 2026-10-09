1. Mutable kya hota hai?

Mutable = jise banane ke baad change/modify kar sakte ho.

Example: List
-------------
numbers = [10, 20, 30]
numbers[0] = 100
print(numbers)

Output: [100, 20, 30]

* Yaani same list ko humne modify kar diya.

Mutable types ke examples:
--------------------------  
list
set
dictionary

================================================================================

2. Immutable kya hota hai?

Immutable = jise banane ke baad directly change nahi kar sakte.

Example: Tuple
--------------
numbers = (10, 20, 30)
numbers[0] = 100       // Ye error dega:

TypeError: 'tuple' object does not support item assignment

* Kyunki Tuple immutable hai.

Immutable types ke common examples:
-----------------------------------
int
float
bool
str
tuple
frozenset

================================================================================

3. Simple real-life example 🧠

* Socho tumhare paas ek whiteboard hai.

Uspar likha:
------------
10 20 30

* Tum 20 ko erase karke 50 likh sakte ho ➡️ Mutable

--------------------------------------------------------------------------------

* Ab socho tumhare paas ek printed certificate hai:

Name: Rahul
Age : 20

* Printed hai, directly change nahi kar sakte ➡️ Immutable

--------------------------------------------------------------------------------

* Python me bhi roughly isi idea se samjho:

Mutable   → change kar sakte ho
Immutable → change nahi kar sakte

================================================================================

String bhi Immutable hai
------------------------

* Ye beginners ko thoda surprising lagta hai.

name    = "Rahul"
name[0] = "M"       // ❌ Error.

* String ko directly modify nahi kar sakte.

. Lekin tum new string bana sakte ho:

CODE:
-----
name = "Rahul"
name = "Mahul"
print(name)

Output: Mahul

* Yahan purani string modify nahi hui. name ko ek new string assign hui.

================================================================================

Integer bhi Immutable hai:
--------------------------

x = 10
x = 20

* Tumhe lag sakta hai ki 10 change hokar 20 ho gaya.

* Actually Python me 10 ko modify nahi kiya gaya.

. x ab 20 object ko refer kar raha hai.

Simple level par:
-----------------
x → 10
x = 20
x → 20

================================================================================

Set Mutable hai:
----------------
numbers = {10, 20, 30}
numbers.add(40)
print(numbers)

Output:
-------
{10, 20, 30, 40}

* Set ko modify kar diya.

➡️ Set = Mutable

================================================================================

Dictionary Mutable hai:
-----------------------
student = {
    "name": "Rahul",
    "age": 20
}
student["age"] = 21
print(student)

Output:
-------
{'name': 'Rahul', 'age': 21}

* Dictionary modify ho gayi ➡️ Dictionary = Mutable

================================================================================
--------------------------------------------------------------------------------
================================================================================

9. Frozenset Immutable hai
--------------------------

Normal Set:
-----------
a = {10, 20, 30}
a.add(40)                   ✅ Allowed.

Frozenset:
----------
a = frozenset([10, 20, 30])
a.add(40)                   ❌ Allowed nahi hai.

So:
---
set       → Mutable
frozenset → Immutable

================================================================================

Normal Set
----------
* Set ko directly curly braces se bana sakte ho:

a = {10, 20, 30}

<----------------------------------------------------------->

Frozenset
---------
* frozenset ko function/constructor ki tarah use karte hain:

CODE:
-----
a = frozenset([10, 20, 30])
print(a)

. Yahan [10, 20, 30] input iterable hai, jiske elements se 
  frozenset ban raha hai.

Output:
-------
frozenset({10, 20, 30})

================================================================================

Tum ye bhi kar sakte ho:
------------------------
a = frozenset({10, 20, 30})   // Ye bhi valid hai.

Aur:
----
a = frozenset((10, 20, 30))   // Ye bhi valid hai.

* Actually frozenset() kisi iterable se frozenset bana sakta hai:

list       → frozenset([10,20,30])
tuple      → frozenset((10,20,30))
set        → frozenset({10,20,30})
string     → frozenset("hello")

================================================================================

# Lekin {} kyun nahi?

Ye:
---
a = {10, 20, 30}

* Python me specifically set literal ka syntax hai.

* Frozenset ka koi special literal syntax nahi hai. 
  Isliye constructor use karna padta hai:

a = frozenset([10, 20, 30])

Simple yaad rakho 🧠
--------------------
Set:
a = {10, 20, 30}

Frozenset:
a = frozenset([10, 20, 30])

Set       = mutable
Frozenset = immutable

* Aur ek interesting point: empty set bhi {} se nahi banta:

a = {}  // Ye empty dictionary hai.

Empty set ke liye:
------------------
a = set()

Aur empty frozenset:
--------------------
a = frozenset()

So Python me {} dekhkar hamesha set mat samajhna — {} actually 
empty dictionary hota hai.

================================================================================

* frozenset ka set se direct relation hai — actually ye immutable 
                                            set hi hai.

* Lekin ye kisi bhi iterable ko simply immutable nahi banata.

Example:
--------
a = [10, 20, 30]
b = frozenset(a)
print(b)

Output:
-------
frozenset({10, 20, 30})

<------------------------------------------------>

Yahan kya hua?

List
----
[10, 20, 30]
      ↓
frozenset()
      ↓
frozenset({10, 20, 30})

* List immutable nahi bani, Usse ek naya frozenset object create hua.

================================================================================

* Ye difference bahut important hai:

❌ Ye mat sochna : frozenset() kisi bhi iterable ko immutable bana deta hai.

✅ Actually      : frozenset() kisi iterable ke elements se ek immutable set 
                   create karta hai.

--------------------------------------------------------------------------------

Example
-------
numbers = [10, 20, 30]
f       = frozenset(numbers)
numbers.append(40)
print(numbers)
print(f)

Output:
-------
[10, 20, 30, 40]
frozenset({10, 20, 30})

* Dekho original list abhi bhi mutable hai. frozenset alag object hai.

================================================================================

To final concept:
-----------------
set
 ↓
Mutable set

frozenset
 ↓
Immutable set

* Aur frozenset() ko input me list, tuple, set, string etc. 
  de sakte ho, but result hamesha frozenset hota hai.

Isliye frozenset ko best way me yaad karo:
------------------------------------------
"Frozenset = set ka immutable version."

================================================================================
--------------------------------------------------------------------------------
================================================================================

10. Ek important table 🔥
-------------------------

| Data Type   | Mutable?     |
| ----------- | -----------  |
| `int`       | ❌ Immutable |
| `float`     | ❌ Immutable |
| `bool`      | ❌ Immutable |
| `str`       | ❌ Immutable |
| `tuple`     | ❌ Immutable |
| `frozenset` | ❌ Immutable |
| `list`      | ✅ Mutable   |
| `set`       | ✅ Mutable   |
| `dict`      | ✅ Mutable   |

================================================================================

11. Mutable vs Immutable ka actual fayda kya hai?

* Ye sirf definition nahi hai. Iska practical effect hota hai.

For example:
------------
a = [10, 20, 30]
b = a
b.append(40)
print(a)
print(b)

Output:
-------
[10, 20, 30, 40]
[10, 20, 30, 40]

😮 a bhi change ho gaya!

Kyun? Because a aur b same list object ko refer kar rahe hain.

--------------------------------------------------------------------------------

Immutable example:
------------------
a = (10, 20, 30)
b = a

* Tuple ko directly modify hi nahi kar sakte.

* Isliye immutable objects ka behavior different hota hai.

================================================================================

12. Ek aur important distinction

* Immutable ka matlab ye nahi hai ki variable ko kabhi 
  change nahi kar sakte.

Example:
--------
x = 10
x = 20   // Ye bilkul allowed hai.

* x variable ko new value assign kar sakte ho.

--------------------------------------------------------------------------------

Immutable ka matlab hai:
------------------------
* Object ko khud modify nahi kar sakte.

Isi tarah:
----------
name = "Rahul"
name = "Aman"     // Allowed hai.

Lekin:
------
name[0] = "M"    // ❌ Allowed nahi hai.

================================================================================

🧠 Final shortcut
-----------------
Bas ye line yaad rakho:

* Mutable   → object ke andar change kar sakte ho.

* Immutable → object banne ke baad uske andar direct 
              change nahi kar sakte.


Mutable
├── List
├── Set
└── Dictionary

Immutable
├── int
├── float
├── bool
├── string
├── tuple
└── frozenset

--------------------------------------------------------------------------------

* Aur tumhare ab tak ke concepts ko connect karo:

List       → Mutable
Tuple      → Immutable
Set        → Mutable
FrozenSet  → Immutable
Dictionary → Mutable
String     → Immutable