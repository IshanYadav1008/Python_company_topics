1. Sabse pehle Dictionary samjho:
---------------------------------

* Python mein dictionary data ko key: value ke form mein store 
  karti hai.

marks = {    
    "Rahul": 80,    
    "Aman": 60,    
    "Priya": 90,    
    "Neha": 70
        }

Yahan:
------
- "Rahul" → key
- 80      → value

* Isi tarah Aman ke marks 60 hain, Priya ke 90 hain.

--------------------------------------------------------------------------------

Dictionary by values sorting ka matlab ?
----------------------------------------

* Humein dictionary ko marks (values) ke according sort karna hai, 
  na ki names (keys) ke according.

* Maan lo humein marks ko ascending order mein arrange karna hai, 
  yaani chhote se bade:

Original dictionary
-------------------
Rahul : 80
Aman  : 60
Priya : 90
Neha  : 70

Sorted by values (ascending)
----------------------------
Aman  : 60
Neha  : 70
Rahul : 80
Priya : 90

* Dhyan do: names nahi badle, bas unka order marks ke hisaab se 
            badal gaya.

================================================================================

2. Manually kaise karenge? (Without sort() and sorted()):
---------------------------------------------------------

* Pehle khud logic lagayenge, built-in sorting functions use 
  nahi karenge.

Step 1: Dictionary ka data lo
-----------------------------
marks = {
    "Rahul": 80,
    "Aman": 60,
    "Priya": 90,
    "Neha": 70
}

--------------------------------------------------------------------------------

Step 2: Dictionary ko list mein convert karo
--------------------------------------------
items = list(marks.items())
print(items)

Output:
-------
[
    ('Rahul', 80),
    ('Aman', 60),
    ('Priya', 90),
    ('Neha', 70)
]

- items() har key-value pair ko tuple banata hai.

- Jaise ('Rahul', 80) mein index 0 par key aur 
  index 1 par value hai.

--------------------------------------------------------------------------------

Step 3: Values compare karke manually sorting karo
--------------------------------------------------
Hum Bubble Sort ka logic use karenge.

* Simple idea: do paas-paas ke elements ki values compare karo. 
               Agar pehli value badi hai, toh unki jagah badal 
               do.

CODE:
-----

marks = {
    "Rahul": 80,
    "Aman": 60,
    "Priya": 90,
    "Neha": 70
}

items = list(marks.items())

for i in range(len(items)):
    for j in range(len(items) - 1 - i):
        if items[j][1] > items[j + 1][1]:
            items[j], items[j + 1] = items[j + 1], items[j]

result = dict(items)
print(result)

Output:
-------
{'Aman': 60, 'Neha': 70, 'Rahul': 80, 'Priya': 90}

Ab code ko ek-ek line mein samjho
---------------------------------
1. items = list(marks.items())
-  Dictionary ko list of tuples mein badla.

<------------------------------------------------------>

2. for i in range(len(items))
-  Ye outer loop hai. Ye decide karta hai ki 
   kitne rounds chalenge.

<------------------------------------------------------>

3. for j in range(len(items) - 1 - i)
-  Ye paas-paas ke elements ko compare karta hai.

<------------------------------------------------------>

4. if items[j][1] > items[j + 1][1]
-  Yahan [1] ka matlab tuple ki value hai.

Example:
--------
('Rahul', 80)[1]   # 80

* Agar pehli value doosri se badi hai, toh swap kar do.

<------------------------------------------------------>

5. items[j], items[j + 1] = items[j + 1], items[j]

- Dono elements ki position exchange ho jaati hai.

<------------------------------------------------------>

6. result = dict(items)

- Sorted list ko wapas dictionary mein convert kar diya.

Bas! Ye hai manual sorting ka logic.

================================================================================

3. Ab sorted() se karte hain:
-----------------------------

* Python mein sorted() ek built-in function hai jo kisi 
  iterable ke elements ko sort karke nayi list return 
  karta hai.

- Dictionary ko values ke according sort karne ke liye:

CODE:
-----
marks = {
    "Rahul": 80,
    "Aman": 60,
    "Priya": 90,
    "Neha": 70
}

result = dict(sorted(marks.items(), key=lambda x: x[1]))
print(result)

Output:
-------
{'Aman': 60, 'Neha': 70, 'Rahul': 80, 'Priya': 90}

--------------------------------------------------------------------------------

sorted() ki line ko tod kar samjho
----------------------------------
=> sorted(marks.items(), key=lambda x: x[1])

marks.items()
Dictionary ke key-value pairs deta hai.
Example: ('Rahul', 80)
       |
       |
key=lambda x: x[1]
Python ko batata hai ki sorting kis cheez ke basis par karni hai.
x[0] = key, x[1] = value
       |
       |
sorted(...)
Pairs ko value ke hisaab se ascending order mein arrange karta hai.
       |
       |
dict(...)
Sorted pairs ko wapas dictionary mein convert karta hai.

--------------------------------------------------------------------------------

lambda x: x[1] ka matlab kya hai ?
----------------------------------
* Maan lo Python ke paas ye tuple hai:

=> x = ("Rahul", 80)

Toh:
----
x[0]   # Rahul
x[1]   # 80

* lambda x: x[1] ka matlab hai: har item mein se value nikalo aur 
            uske basis par sorting karo.

--------------------------------------------------------------------------------

Descending order kaise karenge?
-------------------------------

* Bade se chhote marks:

result = dict(
    sorted(marks.items(), key=lambda x: x[1], reverse=True)
)
print(result)

Output:
-------
{'Priya': 90, 'Rahul': 80, 'Neha': 70, 'Aman': 60}

- reverse=True order ko descending bana deta hai.

================================================================================

4. Ab sort() ka use samjho:
---------------------------

* Ek important difference yaad rakho:

- sorted() kisi bhi iterable ko sort karke nayi list 
  deta hai.

- sort() list ko usi jagah modify karta hai aur None 
  return karta hai.

* Dictionary par directly marks.sort() nahi chalega, 
  kyunki dictionary mein sort() method nahi hota.

* Pehle dictionary ko list mein convert karenge, phir 
  sort() lagayenge.

CODE:
-----
marks = {
    "Rahul": 80,
    "Aman": 60,
    "Priya": 90,
    "Neha": 70
}

items = list(marks.items())
items.sort(key=lambda x: x[1])
result = dict(items)
print(result)

Output:
-------
{'Aman': 60, 'Neha': 70, 'Rahul': 80, 'Priya': 90}

- Yahan items.sort(key=lambda x: x[1]) list ko values ke 
  according sort kar raha hai.

--------------------------------------------------------------------------------

Descending order ke liye:
-------------------------
=> items.sort(key=lambda x: x[1], reverse=True)

Note: sort() ko is tarah assign mat karna:
------------------------------------------
items = items.sort(key=lambda x: x[1])

- Isse items ki value None ho jayegi, kyunki sort() list ko 
  modify karta hai, sorted list return nahi karta.

================================================================================

5. sort() vs sorted() — quick revision:
---------------------------------------

Feature	                  sort()	                sorted()
-------------------------------------------------------------------------------
Kahan use hota hai?	      Sirf lists par method     Lists, tuples, dictionaries 
                          ke roop mein              ke iterables, etc.
-------------------------------------------------------------------------------
Nayi list banata hai?	  Nahi	                    Haan
-------------------------------------------------------------------------------
Original list badalta     Haan	                    Nahi
hai?
-------------------------------------------------------------------------------
Return value	          None	                    Sorted list
-------------------------------------------------------------------------------
Dictionary by values	  list(items) banakar	    sorted(marks.items(), ...)
-------------------------------------------------------------------------------

================================================================================

6. Ab tum khud practice karo:
-----------------------------

Question 1: Is dictionary ko values ke ascending order mein sort 
            karna hai.
        
data = {"A": 40, "B": 10, "C": 30}

Kaunsa code sahi hai?

o/p: dict(sorted(data.items(), key=lambda x: x[1]))


Yaad rakhne ka sabse simple formula:
------------------------------------
# By values — ascending
dict(sorted(d.items(), key=lambda x: x[1]))

# By values — descending
dict(sorted(d.items(), key=lambda x: x[1], reverse=True))

* Pehle manual Bubble Sort ka logic samjho, phir sorted() wali 
  line apne aap easy lagne lagegi.