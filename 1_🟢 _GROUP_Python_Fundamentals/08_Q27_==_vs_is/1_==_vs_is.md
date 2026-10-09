1. Sabse pehle one-line difference

== → values same hain ya nahi?
is → dono variables same object ko refer kar rahe hain ya nahi?

* Bas ye basic difference yaad rakho.

==============================================================================

2. == kya karta hai?

* == value/content compare karta hai.

CODE:
-----
a = [10, 20, 30]
b = [10, 20, 30]
print(a == b)

Output: True

<------------------------------------------------------>

* Kyun? Dono lists ke andar same values hain:

a → [10, 20, 30]
b → [10, 20, 30]

* Chahe dono alag list objects hon, unka content 
  same hai.

Isliye: a == b → True

==============================================================================

3. is kya karta hai?

* is check karta hai: Kya a aur b exactly same object hain?

Example:
--------
a = [10, 20, 30]
b = [10, 20, 30]
print(a is b)

Output: False  // Kyun? Dono ki values same hain:

a → [10, 20, 30]
b → [10, 20, 30]

* Lekin ye do alag list objects hain.

So:
---
a == b   → True
a is b   → False

🔥 Ye == vs is ka sabse important example hai.

==============================================================================

4. Ab b = a karo

Ab dekho:
---------
a = [10, 20, 30]
b = a
print(a == b)
print(a is b)

Output:
-------
True
True

<-------------------------------------------------->

* Kyun? Is baar b ne new list nahi banayi.

* b = a ka matlab hai: b bhi usi object ko refer 
                       karega jisko a refer kar 
                       raha hai.

Conceptually:

       ┌──────────────┐
a ────►│ [10,20,30]   │
       └──────────────┘
b ────────►

Dono same object hain.

Isliye:
-------
a == b   # True
a is b   # True

==============================================================================

5. Ek table se samjho

Case 1: Same values, different objects
--------------------------------------
a = [10, 20]
b = [10, 20]

a == b   → True
a is b   → False

<---------------------------------------------------->

Case 2: Same object
-------------------
a = [10, 20]
b = a

a == b   → True
a is b   → True

==============================================================================

6. Real-life analogy 🧠
-----------------------

* Maan lo tumhare paas do notebooks hain:

Notebook A → "Python"
Notebook B → "Python"

* Dono notebooks ke andar same content hai.

A == B → True // Because content same hai.

<------------------------------------------------->

* Lekin notebooks physically alag hain:

A is B → False

------------------------------------------------------------------------------

Ab:
---
A = Notebook 1
B = Notebook 1

* Dono naam same notebook ko refer kar rahe hain.

Ab:
---
A == B → True
A is B → True

==============================================================================

7. Numbers me confusion kyu hota hai?

Ab ye dekho:
------------
a = 10
b = 10
print(a == b)
print(a is b)

Output kai situations me:
-------------------------
True
True

<------------------------------------------------->

* Ye dekhkar beginners sochte hain:

"Toh == aur is same hi hain!"  // ❌ Nahi.

* Python kuch immutable objects, especially small 
  integers, ko internally reuse/cache kar sakta hai.

Isliye:
-------
a = 10
b = 10

* me dono kabhi same object ko refer kar sakte hain.

* Lekin is ko value comparison ke liye use nahi karna 
  chahiye.

* Number compare karna ho: a == b, Use karo.

==============================================================================

8. String me bhi confusion ho sakta hai:
----------------------------------------

a = "hello"
b = "hello"
print(a == b)
print(a is b)

. is ka result kuch cases me True aa sakta hai because 
  Python strings ko internally reuse/intern kar sakta 
  hai.

. Lekin tumhe is se strings compare nahi karni chahiye.

Correct:
--------
a == b

==============================================================================

9. is ka sabse important use: None

* is ka most common practical use hai:

=> x = None

CODE:
-----
if x is None:
    print("No value")

Output:
-------
No value

* Yahan is None use karna Python convention hai.

Aisa mat karo:
--------------
if x == None:    // Technically kaam kar sakta hai.

lekin Python me preferred style:
--------------------------------
if x is None:

==============================================================================

10. None kya hai?

* None ka meaning roughly: "Abhi koi value nahi hai."

Example:
--------
result = None  // Matlab result ke paas currently koi 
                  actual value nahi hai.

Check:
------
if result is None:
    print("Result nahi mila")

==============================================================================

11. is not bhi hota hai

Jaise:
------
x = None
print(x is None)

Output:
-------
True

<------------------------------------------>

Opposite:
---------
print(x is not None)

Output:
-------
False

==============================================================================

12. == ka opposite !=

==:
---
=> a == b   // Meaning: values equal hain?

!=:
---
a != b      // Meaning: values equal nahi hain?

<------------------------------------------------->

Similarly:
----------
==     → value equal?
!=     → value not equal?

is     → same object?
is not → different object?

==============================================================================

13. Ek important point: is value compare nahi karta

Ye bahut important hai.
-----------------------
a = [1, 2, 3]
b = [1, 2, 3]
a == b

* Python basically pooch raha hai: "Kya dono ka content equal hai?"

Answer:
-------
True

<---------------------------------------------------->

Lekin:
------
a is b

Python pooch raha hai: "Kya dono EXACT SAME object hain?"

Answer:
-------
False

==============================================================================

14. Mutable objects me ye aur clear hota hai:

CODE:
-----
a = [10, 20]
b = a
b.append(30)
print(a)
print(b)

Output:
-------
[10, 20, 30]
[10, 20, 30]

Kyun?
-----
Because: a is b True hai.

* Dono same list object ko refer kar rahe hain.

==============================================================================

15. == vs is — final table 🔥

| Operator | Kya check karta hai? | Example      |
| -------- | -------------------- | ------------ |
| `==`     | Values/content same? | `a == b`     |
| `!=`     | Values different?    | `a != b`     |
| `is`     | Same object?         | `a is b`     |
| `is not` | Different objects?   | `a is not b` |

==============================================================================

🧠 Golden Rule
--------------

* Normal values compare karni hain → ==

age == 20
name == "Rahul"
marks == 90
list1 == list2

<--------------------------------------------------->

* Check karna hai ki same object hai → is

a is b

<--------------------------------------------------->

Specially None check karna hai → is None

if result is None:
    ...

<--------------------------------------------------->

Sabse important:
----------------
==  → "Kya same VALUE hai?"
is  → "Kya same OBJECT hai?"

* Ye distinction clear ho gaya to == vs is ka confusion 
  almost khatam.