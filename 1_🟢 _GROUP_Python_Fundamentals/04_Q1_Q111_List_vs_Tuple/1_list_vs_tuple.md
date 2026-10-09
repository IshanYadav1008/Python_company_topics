* List vs Tuple Python ka bahut important concept hai. Dono collection 
  hain, lekin sabse bada difference hai: List ko change kar sakte ho, 
  Tuple ko nahi.

1. Basic difference
-------------------

# List

List ko [] se banate hain:
--------------------------
numbers = [10, 20, 30, 40]

* Isme tum elements ko change, add aur remove kar sakte ho.

CODE:
-----
numbers[0] = 100
print(numbers)

Output:
-------
[100, 20, 30, 40]

============================================================================

# Tuple

Tuple ko () se banate hain:
---------------------------
numbers = (10, 20, 30, 40)

* Tuple ko banane ke baad uske elements change nahi kar sakte.

=> numbers[0] = 100 

Ye error dega:
--------------
TypeError: 'tuple' object does not support item assignment

============================================================================
----------------------------------------------------------------------------
============================================================================

2. Main difference
------------------

| Feature           | List          | Tuple      |
| ----------------- | ------------- | ---------- |
| Syntax            | `[]`          | `()`       |
| Change kar sakte? | ✅ Yes        | ❌ No      |
| Mutable?          | ✅ Yes        | ❌ No      |
| Ordered?          | ✅ Yes        | ✅ Yes     |
| Duplicate values? | ✅ Yes        | ✅ Yes     |
| Indexing?         | ✅ Yes        | ✅ Yes     | 
| `append()`        | ✅ Yes        | ❌ No      |
| `remove()`        | ✅ Yes        | ❌ No      |
| `count()`         | ✅ Yes        | ✅ Yes     | 
| `index()`         | ✅ Yes        | ✅ Yes     |
| Generally         | More flexible | More fixed |

============================================================================
----------------------------------------------------------------------------
============================================================================

3. List ko kab use karein?

* Jab tumhare data ko future me change karna ho, List use karo.

Example:
--------
students = ["Rahul", "Aman", "Priya"]
students.append("Rohit")              // Baad me student add karna hai:
print(students)

Output:
-------
['Rahul', 'Aman', 'Priya', 'Rohit']

<------------------------------------------------>

* Ya student remove karna hai:

students.remove("Aman")

<------------------------------------------------>

Real-life examples
------------------

List use karo jab:
------------------
. Shopping cart ke items change hote hain
. Students ki list me students add/remove hote hain
. Todo list update hoti hai
. Scores/marks update ho sakte hain
. User data dynamically add/remove ho raha hai

Example:
--------
cart = ["Apple", "Milk", "Bread"]
cart.append("Eggs")
cart.remove("Milk")

* Yahan List perfect hai, kyunki data change ho raha hai.

============================================================================

4. Tuple ko kab use karein?

* Jab tumhara data fixed rehna chahiye, Tuple use karo.

Example:
--------
coordinates = (10, 20)  // Ye kisi point ke coordinates hain:

x = 10
y = 20

Usually tum nahi chahte ki accidentally:
----------------------------------------
coordinates[0] = 50  // ho jaye.

Isliye Tuple useful hai.

<------------------------------------------------>

Real-life examples
------------------
rgb    = (255, 0, 0)
days   = ("Monday", "Tuesday", "Wednesday", "Thursday", "Friday")
person = ("Rahul", 21, "Indore")

* Agar ye values ek fixed group ko represent kar rahi hain, 
  tuple useful ho sakta hai.

============================================================================

5. Ek important example

* Suppose tumhare paas shopping cart hai:

CODE:
-----
cart = ["Apple", "Milk", "Bread"]

cart.append("Eggs")  // User baad me item add kar sakta hai:

List → suitable ✅

----------------------------------------------------------------------------

* Lekin agar tumhare paas ek location hai:

=> location = (22.7196, 75.8577)

* Coordinates ko tum generally ek fixed pair ki tarah 
  treat karna chahoge.

Tuple → suitable ✅

============================================================================
----------------------------------------------------------------------------
============================================================================

6. List ke important methods

* List mutable hai, isliye iske kaafi methods hain:

=> numbers = [10, 20, 30]

Add
---
numbers.append(40)

Remove
------
numbers.remove(20)

Insert
------
numbers.insert(1, 15)

Sort
----
numbers.sort()

Reverse
-------
numbers.reverse()

============================================================================

7. Tuple ke methods

* Tuple immutable hai, isliye methods bahut kam hain.

Mainly:
-------

count()
-------
numbers = (10, 20, 20, 30)
print(numbers.count(20))

Output: 2

<------------------------------------------->

index()
-------
print(numbers.index(30))

Output: 3

* Tuple me append(), remove(), sort() jaise 
  methods nahi hote.

============================================================================
----------------------------------------------------------------------------
============================================================================

8. Ek bahut important concept 🧠

Tum ye yaad rakho:
------------------
List  = Changeable data
Tuple = Fixed data

Example:
--------
# Change hone wala data
marks = [80, 75, 90, 85]

* Agar marks update ho sakte hain → List

<---------------------------------------------------->

# Fixed data
point = (10, 20)

* Agar values ka fixed group hai → Tuple

============================================================================

9. Performance ka bhi difference hai
-------------------------------------

* Generally Tuple List se thoda lightweight/faster hota hai 
  because Tuple immutable hai.

* Lekin beginner level par speed ke liye Tuple choose karne 
  ki zarurat nahi.

Pehle ye rule follow karo:
--------------------------
Data change hoga?    → List
Data fixed hai?      → Tuple

============================================================================

10. Ek interesting example

Maan lo:
--------
student    = ["Rahul", 20, "Python"]  // Tum isme change kar sakte ho:
student[1] = 21

Result:
-------
["Rahul", 21, "Python"]

<----------------------------------------------------->

Agar:
-----
student = ("Rahul", 20, "Python")
student[1] = 21

❌ Error, Kyuki Tuple immutable hai.

============================================================================

🔥 Final shortcut

# LIST
------
[]
Mutable
Change/Add/Remove possible
Dynamic data ke liye

<------------------------------------------>

# TUPLE
-------
()
Immutable
Change/Add/Remove directly possible nahi
Fixed data ke liye

<------------------------------------------->

Ek line me:
-----------
* Agar tum soch rahe ho "future me is data ko modify karunga" → List.

* Agar tum soch rahe ho "ye values ek fixed group hain, change 
  nahi honi chahiye" → Tuple.