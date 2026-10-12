# Polymorphism with Built-in Functions:

* Python mein Built-in Functions woh functions hote hain jo pehle se 
  Python mein available hote hain. Jaise len(), print(), max().

* Jab ek hi built-in function alag-alag types ke objects par kaam 
  karta hai aur unke hisaab se result deta hai, toh ye Polymorphism 
  ka example hota hai.

==============================================================================

1. len() function se samjho:

* len() ka kaam kisi cheez ki length ya number of items batana hai.

CODE:
-----
name    = "Rahul"
fruits  = ["Apple", "Mango", "Banana"]
numbers = (10, 20, 30, 40)

print(len(name))
print(len(fruits))
print(len(numbers))

Output:
-------
5
3
4

------------------------------------------------------------------------------

Samjho kya hua:
---------------
- len(name) ne string ke characters gine.
- len(fruits) ne list ke items gine.
- len(numbers) ne tuple ke items gine.

* Humne har baar same function len() use kiya, lekin usne alag-alag 
  types ke data par kaam kiya.

* Yahi Polymorphism hai — same function, different types of objects 
                          ke saath kaam karna.

==============================================================================

2. max() function se samjho:

* max() sabse badi value deta hai.

CODE:
-----
print(max(10, 20, 30))
print(max("Apple", "Mango", "Banana"))

Output:
-------
30
Mango

* Pehli baar max() ne numbers mein sabse badi value di. Doosri baar 
  usne strings mein alphabetical order ke hisaab se sabse badi 
  string di.

* Yaani same function, lekin data ke type ke hisaab se comparison ka 
  tareeka alag.

------------------------------------------------------------------------------

# Quick revision table

Function | Data ka type | Function kya karta hai
---------|--------------|---------------------------------------
len()    | String       | Characters ki sankhya batata hai
len()    | List         | Items ki sankhya batata hai
len()    | Tuple        | Items ki sankhya batata hai
max()    | Numbers      | Sabse badi numerical value deta hai
max()    | Strings      | Alphabetical order ke hisaab se maximum deta hai

Iska fayda kya hai?
-------------------
* Tumhe har data type ke liye alag function yaad rakhne ki zaroorat nahi. 
  Tum len() ko string, list aur tuple ke saath use kar sakte ho.

* Yaad rakho: Built-in functions ke saath Polymorphism ka matlab hai ki 
              ek hi function, alag-alag types ke data ke saath kaam kar 
              sakta hai.