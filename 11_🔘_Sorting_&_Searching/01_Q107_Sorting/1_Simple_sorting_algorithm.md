1. Sorting kya hoti hai ?
-------------------------

* Sorting ka matlab hai data ko ek particular order mein 
  arrange karna.

Maan lo tumhare paas numbers ki ek list hai:
--------------------------------------------
numbers = [5, 2, 8, 1, 3]

- Abhi numbers kisi particular order mein nahi hain.

----------------------------------------------------------------------------------

Sorting karne ke baad:
----------------------

# Before sorting
5      2      8      1      3

Sorting

# After sorting — Ascending order
1      2      3      5      8

==================================================================================

2. Sorting ke types
-------------------

* Do basic types yaad rakho:

1. Ascending order — chhote se bade ki taraf.

[1, 2, 3, 5, 8]

2. Descending order — bade se chhote ki taraf.

[8, 5, 3, 2, 1]

Python mein built-in sorting:
-----------------------------
numbers = [5, 2, 8, 1, 3]

numbers.sort()
print(numbers)

Output:
-------
[1, 2, 3, 5, 8]

Descending ke liye:
-------------------
numbers.sort(reverse=True)
print(numbers)

Output:
-------
[8, 5, 3, 2, 1]

Dhyan do: .sort() original list ko change karta hai, jabki 
           sorted(numbers) ek nayi sorted list return karta 
           hai.

==================================================================================

3. Simple Sorting Algorithm kya hota hai ?
------------------------------------------

* Algorithm ka matlab hai kisi problem ko solve karne ke 
  step-by-step instructions.

* Simple sorting algorithm mein hum numbers ko compare karke 
  unhe sahi order mein arrange karte hain.

* Ek beginner-friendly algorithm hai Bubble Sort.

- Ismein paas-paas ke do numbers compare karte hain. Agar 
  pehla number doosre se bada hai, toh unhe swap kar dete 
  hain.

Example: Bubble Sort
--------------------
Maan lo list hai:  [5, 2, 4, 1]

----------------------------------------------------------------------------------

Step-by-step sorting
--------------------

Step 1 — 5 aur 2 compare karo
-----------------------------
5    --->    2
     <---


5 bada hai, isliye swap karenge.
--------------------------------
[2, 5, 4, 1]

<------------------------------------------------->

Step 2 — 5 aur 4 compare karo
-----------------------------
5 bada hai, toh swap karenge.
[2, 4, 5, 1]

<------------------------------------------------->

Step 3 — 5 aur 1 compare karo
-----------------------------

5 bada hai, toh swap karenge.
[2, 4, 1, 5]

<------------------------------------------------->

Agla pass
---------

Isi process ko repeat karenge, jab tak list sort na 
ho jaaye.
[1, 2, 4, 5]

==================================================================================

4. Bubble Sort ka Python code
-----------------------------

* Ab wahi logic Python mein likhte hain:

CODE:
-----
numbers = [5, 2, 4, 1]

n = len(numbers)

for i in range(n):
    for j in range(n - 1 - i):
        if numbers[j] > numbers[j + 1]:
            numbers[j], numbers[j + 1] = numbers[j + 1], numbers[j]

print(numbers)

Output:
-------
[1, 2, 4, 5]

----------------------------------------------------------------------------------

# Code ko samjho:
# ---------------

Code	                                       Kaam
----------------------------------------------------------------------------------
len(numbers)	                               List mein kitne elements hain
----------------------------------------------------------------------------------
for i in range(n)	                           Sorting ke multiple passes chalata 
                                               hai
----------------------------------------------------------------------------------
for j in range(n - 1 - i)	                   Paas-paas ke elements par chalta 
                                               hai
----------------------------------------------------------------------------------
if numbers[j] > numbers[j + 1]	               Check karta hai ki swap karna hai 
                                               ya nahi
----------------------------------------------------------------------------------
numbers[j], numbers[j + 1] = numbers[j + 1],   Dono elements ko swap karta hai
numbers[j]
----------------------------------------------------------------------------------

* n - 1 - i isliye use kiya hai kyunki har pass ke baad sabse bada bacha hua 
  number list ke end mein pahunch jaata hai.

==================================================================================

5. Ab tumhari practice:
-----------------------

Is list ko ascending order mein sort karo:
[7, 3, 5, 1]

Tumhara answer kya hoga?

o/p: [1, 3, 5, 7]

- Ascending order mein numbers chhote se bade hote hain: [1, 3, 5, 7].

==================================================================================
----------------------------------------------------------------------------------
==================================================================================

# Difference between sort and sorted:

1. sort() kya hota hai ?
------------------------
* sort() list ko sort karta hai aur original list ko change 
  kar deta hai.

numbers = [5, 2, 8, 1, 3]
numbers.sort()
print(numbers)

Output:
-------
[1, 2, 3, 5, 8]

- Yahan numbers wali original list hi change ho gayi.

==================================================================================

2. sorted() kya hota hai ?
--------------------------
* sorted() bhi list ko sort karta hai, lekin original list ko 
  change nahi karta. Ye ek nayi sorted list return karta hai.

CODE:
-----
numbers = [5, 2, 8, 1, 3]
result  = sorted(numbers)

print(result)
print(numbers)

Output:
-------
[1, 2, 3, 5, 8]
[5, 2, 8, 1, 3]

- Dekho, result sorted hai, lekin numbers pehle jaisi hi hai.

==================================================================================

3. sort() vs sorted() — main difference:
----------------------------------------

Feature	              sort()	            sorted()
------------------------------------------------------------------------------
Kaam	              List sort karta hai	Iterable se sorted list banata hai
Original list	      Change hoti hai	    Change nahi hoti
Return value	      None	                Nayi sorted list
Use	                  numbers.sort()	    sorted(numbers)
------------------------------------------------------------------------------

==================================================================================

4. Descending order mein kaise sort karein ?
--------------------------------------------

* Dono mein reverse=True use kar sakte ho.

sort():
-------
numbers = [4, 1, 3, 2]
numbers.sort(reverse=True)
print(numbers)

Output: [4, 3, 2, 1]

sorted():
---------
numbers = [4, 1, 3, 2]
result = sorted(numbers, reverse=True)
print(result)

Output: [4, 3, 2, 1]

==================================================================================

5. Ek important baat yaad rakho:
--------------------------------
* sort() sirf lists ka method hai, jabki sorted() lists ke saath 
  tuples, strings, sets aur doosre iterable objects par bhi kaam 
  kar sakta hai. Ye sorted result list ke form mein deta hai.

Example:
--------
word = "python"
print(sorted(word))

Output:
-------
['h', 'n', 'o', 'p', 't', 'y']

==================================================================================

# Ab ek chhota sa question:

* Is code ka output kya hoga?

a = [3, 1, 2]
b = sorted(a)

print(a)
print(b)

o/p: [3, 1, 2] phir [1, 2, 3]

- sorted(a) ek nayi list banata hai, isliye a change nahi hoti.