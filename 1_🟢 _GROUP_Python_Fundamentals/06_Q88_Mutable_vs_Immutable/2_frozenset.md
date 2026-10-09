# Sabse pehle ek line

* frozenset khud ek data type hai, bilkul set ki tarah.

Bas difference ye hai:
----------------------
set       → unique collection + mutable
frozenset → unique collection + immutable

* Iska direct relation SET se yahi hai: dono ka kaam unique elements 
                                        ka collection rakhna hai.

=============================================================================

1. frozenset() me list dene ka matlab kya hai?

Maan lo:
--------
a = [10, 20, 20, 30]   // Ye ek list hai.

Ab:
---
b = frozenset(a)      // Yahan a input hai.

* Python us list ke elements lekar ek naya frozenset 
  object banata hai.

LIST
[10, 20, 20, 30]
        ↓
   frozenset()
        ↓
FROZENSET
{10, 20, 30}

Notice karo:
------------
* List frozenset nahi ban gayi.

* Balki list ko input dekar naya frozenset banaya gaya.

=============================================================================

2. "Toh relation SET se kaise hai?"

Ab normal set() dekho:
----------------------
a = set([10, 20, 20, 30])

Output: {10, 20, 30}

Aur:
----
b = frozenset([10, 20, 20, 30])

Output: frozenset({10, 20, 30})

* Dono ne same basic kaam kiya:

<-------------------------------------------->

Input:
------
[10, 20, 20, 30]

        ↓

       set()              frozenset()
        ↓                     ↓
 {10, 20, 30}          {10, 20, 30}
   mutable                immutable

* Yahi frozenset ka Set se relation hai.

=============================================================================

3. Ab ek real example

* Socho tumhare paas:

=> students = ["Rahul", "Aman", "Rahul", "Priya"]

Tumhe unique students chahiye.

Normal Set:
-----------
=> unique_students = set(students)

Result:
-------
{"Rahul", "Aman", "Priya"}

* Lekin ye collection change ho sakta hai:

=> unique_students.add("Rohit")

✅ Allowed.

CODE:
-----
students = ["Rahul", "Aman", "Rahul", "Priya"]
unique_students = set(students)
print(unique_students)
unique_students.add("Rohit")
print(unique_students)

O/P: 
----
{'Rahul', 'Priya', 'Aman'}
{'Rahul', 'Priya', 'Rohit', 'Aman'}

-----------------------------------------------------------------------------

Frozenset:
----------
unique_students = frozenset(students)

Result:
-------
frozenset({"Rahul", "Aman", "Priya"})

Ab:
---
unique_students.add("Rohit")   // ❌ Allowed nahi.

* Kyunki frozenset immutable hai.

=============================================================================

4. Toh list/tuple/string ka kya relation hai ? Koi direct relation nahi hai.

Ye bahut important hai.
-----------------------
frozenset() list, tuple, string etc. ko input ke roop me accept kar 
sakta hai, iska matlab ye nahi ki frozenset unka immutable version 
hai.

For example:
------------
frozenset([1, 2, 3])  // ka matlab "immutable list" nahi hai.

* Ye hai: "List ke elements se ek immutable set banao."

<-------------------------------------------------------------------->

Similarly:
----------
frozenset((1, 2, 3))

* ka matlab: "Tuple ke elements se ek immutable set banao."

=============================================================================

5. String wala example aur clear karega

a = frozenset("hello")

Output roughly:
---------------
frozenset({'h', 'e', 'l', 'o'})

Notice:
-------
hello me l do baar tha.

Lekin frozenset me:
-------------------
h
e
l
o

* sirf unique characters hain.

* Ye exactly set ka behavior hai.

* Aur tum ise modify nahi kar sakte.

Isliye:
-------
frozenset = Set ke rules
             +
            immutable

=============================================================================

6. Sabse important distinction

Tum ye mat socho:
-----------------
frozenset
   ↓
"har iterable ka immutable version"

❌ Wrong

<----------------------------------------->

Instead:
--------
list / tuple / set / string
          ↓
      input data
          ↓
    frozenset(...)
          ↓
   immutable SET

✅ Correct

=============================================================================

7. Ekdum simple analogy
-----------------------

* Maan lo tumhare paas alag-alag containers hain:

List    → [A, B, A, C]
Tuple   → (A, B, A, C)
String  → "ABAC"
Set     → {A, B, C}

<------------------------------------------------------------>

* Ab frozenset() ek machine hai jo kisi iterable ke elements 
  lekar "Frozen Set" banati hai:

[A, B, A, C] ──┐
(A, B, A, C) ──┤
{A, B, C}   ───┤──→ frozenset({A, B, C})
"ABAC"      ───┘

* Input kuch bhi ho sakta hai jo iterable hai.

* Lekin output ek hi type ka hota hai: frozenset.

=============================================================================

🔥 Ab final answer
------------------

* frozenset actual me kya hai?

  Ek Python data type hai jo Set jaisa unique collection store karta hai, 
  lekin immutable hota hai.

* Iska relation kiske saath hai?

Direct relation set ke saath hai.

set
├── unique elements
├── unordered
└── mutable

frozenset
├── unique elements
├── unordered
└── immutable

-----------------------------------------------------------------------------

# Phir list/tuple/string kyu de sakte hain?

* Kyuki frozenset() unke elements ko input ke roop me lekar 
  ek naya frozenset banata hai.

frozenset([1, 2, 3])       # list   → frozenset
frozenset((1, 2, 3))       # tuple  → frozenset
frozenset({1, 2, 3})       # set    → frozenset
frozenset("abc")           # string → frozenset

* Input ka type important nahi; frozenset() ke baad jo object 
  banta hai uska type frozenset hota hai.

Bas ye sentence yaad kar lo:
----------------------------
frozenset() kisi iterable ko "immutable" nahi karta; us iterable 
ke elements se ek "immutable set" banata hai.