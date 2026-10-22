1. Queue hota kya hai ?
-----------------------
* Queue ek Data Structure hai, jismein items ek order mein rakhe 
  jaate hain. Jo item sabse pehle aata hai, woh sabse pehle bahar 
  nikalta hai.

- Is rule ko kehte hain FIFO — First In, First Out.

------------------------------------------------------------------------------

# Real-life example: Ticket ki line

* Socho 3 log ticket lene ke liye line mein khade hain:

1. Rahul sabse pehle aaya.
2. Aman doosre number par aaya.
3. Neha teesre number par aayi.

- Ticket bhi sabse pehle Rahul ko milega.
- Jo pehle line mein aaya, woh pehle line se niklega.

==============================================================================

2. Queue dikhta kaisa hai ?
---------------------------

* Maan lo Queue mein teen numbers hain: 10, 20, 30.

FRONT — yahan se item niklega:
------------------------------
10            20           30

Remove: 10            Add: 40

FRONT ← [10] [20] [30] ← REAR (back side)

- Front: jahan se purana item nikalta hai.
- Rear: jahan naya item add hota hai.

* Agar 10 ko remove karein, toh 20 sabse aage aa jayega. 
  Agar naya number 40 add karein, toh woh 30 ke baad 
  aayega.

==============================================================================

3. Queue ki zaroorat kyun hoti hai ?
------------------------------------

* Jab kaam ko jis order mein request aayi hai, usi order mein process 
  karna ho, tab Queue useful hota hai.

1. Ticket counter ya bank
-------------------------
* Jo pehle aaya, uska kaam pehle.


2. Printer
----------
* Multiple print requests ko order mein print karna.


3. Computer programs
--------------------
* Kai systems mein tasks aur requests ko order se 
  process karne ke liye Queue use hoti hai.

==============================================================================

4. Python mein Queue kaise use hoti hai ?
-----------------------------------------

* Python mein hum collections module ke andar available deque use 
  kar sakte hain.

* deque ka full form hai Double-Ended Queue. Ismein dono ends se 
  items add ya remove kiye ja sakte hain. Queue banane ke liye 
  hum rear par add aur front se remove karenge.

------------------------------------------------------------------------------

Step 1: deque import karo
-------------------------
=> from collections import deque

- Is line se hum collections module ke andar se deque ko laate 
  hain.

------------------------------------------------------------------------------

Step 2: Empty Queue banao
-------------------------
queue = deque()
print(queue)

Output:
-------
deque([])

- Abhi Queue khaali hai.

------------------------------------------------------------------------------

Step 3: Items add karo — append()
---------------------------------
queue.append(10)
queue.append(20)
queue.append(30)

print(queue)

Output:
-------
deque([10, 20, 30])

- Har append() naya item rear, yaani right side, par add 
  karta hai.

------------------------------------------------------------------------------

Step 4: Item remove karo — popleft()
------------------------------------

item = queue.popleft()

print(item)
print(queue)

Output:
-------
10
deque([20, 30])

- Dhyaan do: popleft() left side se item remove karta hai. Isliye 
  sabse pehle add hua 10 hi nikla. Yahi FIFO rule hai.

==============================================================================

5. Ab poora Q44 program dekho:
------------------------------

CODE:
-----

from collections import deque

queue = deque()

queue.append(10)
queue.append(20)
queue.append(30)

print("Queue:", queue)

item = queue.popleft()

print("Removed item:", item)
print("Queue after removal:", queue)

Output:
Queue: deque([10, 20, 30])
Removed item: 10
Queue after removal: deque([20, 30])

Output:
-------
Queue              : deque([10, 20, 30])
Removed item       : 10
Queue after removal: deque([20, 30])

==============================================================================

6. Notes ke liye important methods:
-----------------------------------

Method	    | Kaam
------------|---------------------------------------
deque()	    | Empty Queue banana
append(x)	| Rear/right side par item add karna
popleft()	| Front/left side se item remove karna
len(queue)	| Queue mein kitne items hain, batana
not queue	| Check karna ki Queue empty hai ya nahi
----------------------------------------------------

* Ek important baat: Queue ke liye Python ki normal list bhi use ho 
                     sakti hai, lekin deque se front par item remove 
                     karna (popleft()) zyada efficient hota hai.

==============================================================================

7. Chhota sa test:
------------------

# Maan lo:
# --------
from collections import deque

queue = deque([5, 8, 12])
queue.append(20)

item = queue.popleft()

print(item)
print(queue)

<------------------------------------------------------>

* Tumhare hisaab se output kya hoga ?

- 5 aur deque([8, 12, 20])

. Bilkul sahi!Pehle 5 niklega kyunki woh Queue ka sabse 
  purana item hai. Baaki Queue mein [8, 12, 20] rahenge.

<------------------------------------------------------>

* Bas abhi ke liye ye 3 baatein yaad rakho:

1. Queue = FIFO — First In, First Out.
2. append() se item add hota hai.
3. popleft() se sabse purana item remove hota hai.