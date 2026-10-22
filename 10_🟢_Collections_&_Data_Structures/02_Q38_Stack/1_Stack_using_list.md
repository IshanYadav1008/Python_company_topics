1. Stack kya hota hai ?
-----------------------

* Stack ek data structure hai, jisme data ko ek particular order 
  mein add aur remove kiya jaata hai.

Stack ka rule hota hai:
-----------------------
LIFO — Last In, First Out

Iska matlab: jo cheez sabse aakhir mein andar aayegi, woh sabse 
             pehle bahar niklegi.

* Socho tumne plates ko ek ke upar ek rakha hai. Tum ek plate doosri 
  ke upar rakhte jaate ho. Jab plate nikalni hoti hai, toh sabse pehle 
  upar wali plate nikalte ho.

- Yahi Stack ka concept hai!

================================================================================

2. Stack dikhta kaisa hai?
--------------------------


# Stack ka visual example

* Socho ye 3 plates ek ke upar ek rakhi hain.

Plate 30
Last added
   |
Plate 20
   |
Plate 10
First added
   |
Yahin se plate add aur remove hoti hai

- Sabse upar wali plate 30 pehle niklegi, phir 20, 
  phir 10.

================================================================================

3. Stack ki zarurat kyun hoti hai ?
-----------------------------------

* Stack ka use tab hota hai jab humein latest item ko sabse 
  pehle process karna ho.

# Kuch real-life examples:

1. Plates ka stack              : Sabse aakhri mein rakhi plate sabse 
                                  pehle nikalti hai.

2. Undo operation               : Text editor mein tumne teen changes 
                                  kiye. Undo karoge toh sabse recent 
                                  change pehle reverse hoga.

3. Function calls aur navigation: Programming mein function calls ko 
                                  manage karne ke liye call stack use 
                                  hota hai. Kuch navigation-history 
                                  implementations bhi stack ka use 
                                  karti hain.

================================================================================

4. Ab Python mein Stack kaise banega ?
--------------------------------------

* Python mein hum list ka use karke Stack bana sakte hain.

List ka example:
----------------
stack = []

* Ye ek empty list hai, jo abhi empty Stack ki tarah kaam 
  karegi.

Stack mein do important operations hain:
----------------------------------------
- append() — item ko top par add karta hai.
- pop()    — top se item remove karke return karta hai.

--------------------------------------------------------------------------------

Step 1: Items add karo
----------------------
stack = []

stack.append(10)
stack.append(20)
stack.append(30)

print(stack)

Output:
-------
[10, 20, 30]

Samjho:
-------
- Pehle 10 add hua.
- Phir 20 add hua.
- Phir 30 add hua.

* List mein right side wala item Stack ka top hai.

TOP
---
30
20
10
------
BOTTOM

--------------------------------------------------------------------------------

Step 2: Top wala item remove karo
---------------------------------
item = stack.pop()
print(item)
print(stack)

Output:
-------
30
[10, 20]

- pop() ne 30 ko remove kiya, kyunki woh top par tha.
- Ab dobara stack.pop() karoge toh 20 niklega.

================================================================================

5. Poora Stack program — Q38
----------------------------

### Q38 — Implement Stack Using List in Python

**Definition:** A stack is a linear data structure that follows 
                the LIFO (Last In, First Out) principle.

**Program:**
------------
stack = []

# Push elements into the stack
stack.append(10)
stack.append(20)
stack.append(30)

print("Stack:", stack)

# Pop an element from the stack
item = stack.pop()

print("Popped element:", item)
print("Stack after pop:", stack)
```

Output:
-------
Stack: [10, 20, 30]
Popped element: 30
Stack after pop: [10, 20]

Explanation:
------------
- append() adds an element to the top of the stack.
- pop() removes and returns the top element.
- The stack follows LIFO: the last element added is 
  the first element removed.

================================================================================

6. Ab khud check karo:
----------------------

Maan lo:
--------
stack = []
stack.append(5)
stack.append(8)
stack.append(12)
stack.pop()

Ab stack ki value kya hogi ? [5, 8]

* Bilkul sahi! 12 sabse last mein add hua tha, isliye pop() 
  ne use remove kiya.