Question)
---------
Hum bina deque() ke quese nhi ban skte kya ?

Answer)
-------

* Haan bilkul! 😊 Hum bina deque() ke bhi Queue bana sakte hain.
  Python mein Queue banane ke multiple tareeke hain.

C- halo simple se samajhte hain.

------------------------------------------------------------------------------

1. Method 1: Normal list se Queue:
----------------------------------

CODE:
-----
queue = []

queue.append(10)
queue.append(20)
queue.append(30)

print(queue)

item = queue.pop(0)

print("Removed:", item)
print("Queue:", queue)

Output:
-------
[10, 20, 30]
Removed: 10
Queue: [20, 30]

Yahan:
------
- queue = [] → empty list banayi.
- append()   → right side mein item add kiya.
- pop(0)     → index 0, yani first item remove kiya.

* Is tarah Queue ka FIFO rule follow hota hai.

==============================================================================

2. Method 2: collections.deque se Queue:
----------------------------------------

CODE:
-----
from collections import deque

queue = deque()

queue.append(10)
queue.append(20)
queue.append(30)

item = queue.popleft()

print(item)
print(queue)

Output:
-------
10
deque([20, 30])

==============================================================================

3. Dono mein difference kya hai ?
---------------------------------

Normal list	                     collections.deque
-------------------------------------------------------------------
queue = []	                     queue = deque()
-------------------------------------------------------------------
Item add: append()	             Item add: append()
-------------------------------------------------------------------
Item remove: pop(0)	             Item remove: popleft()
-------------------------------------------------------------------
Front se remove karna            Front se remove karna efficient hai
comparatively slow ho 
sakta hai.
-------------------------------------------------------------------

==============================================================================

Toh Q44 mein deque hi kyun use karna hai ?
------------------------------------------

* Kyunki tumhare question ka topic specifically 
  “Queue using collections.deque” hai. Isliye us 
  question ko solve karte waqt deque use karna 
  seekhna hai.

Yaad rakhna:
------------
- Queue ek concept hai — FIFO.
- list aur deque us concept ko implement karne ke tareeke hain.

* Yaani Queue banane ke liye deque() compulsory nahi hai, lekin
  Q44 ke liye deque() use karna seekhna zaroori hai.

==============================================================================
------------------------------------------------------------------------------
==============================================================================

* Python ko khud nahi pata ki tumhari list Stack hai ya Queue. Python ko 
  sirf itna pata hai ki stack ek list hai. Stack ya Queue ka behaviour 
  tum decide karte ho ki items kaise add aur remove karoge

1. Tumhare code mein ho kya raha hai ?
--------------------------------------
stack = []

stack.append(10)
stack.append(20)
stack.append(30)

item = stack.pop(0)

print(item)
print(stack)

Output:
-------
10
[20, 30]

- Tumne variable ka naam stack rakha hai, lekin pop(0) se first element 
  remove kiya hai.

- Isliye tumhara code Stack ki tarah nahi, Queue ke FIFO behaviour ki 
  tarah kaam kar raha hai.

- Variable ka naam stack rakhne se woh automatically Stack nahi ban 
  jaata!

==============================================================================

2. Ek hi list, lekin behaviour alag:
------------------------------------

# Stack — LIFO : Last In, First Out

stack = [10, 20, 30]
item = stack.pop()


10          20          30
                        Remove

- Result: 30 remove hoga.

------------------------------------------------------------------------------

# Queue — FIFO behaviour: First In, First Out

queue = [10, 20, 30]
item = queue.pop(0)

Remove
10       20       30

Result: 10 remove hoga. 

==============================================================================

3. Phir kisi ko kaise pata chalega ki Stack hai ya Queue ?
----------------------------------------------------------

Teen baatein yaad rakho:
------------------------
- Variable ka naam       : stack ya queue — sirf samajhne ke liye rakha gaya 
                           naam hai.

- Operations             : Kaise item add aur remove ho raha hai, usse behaviour 
                           pata chalta hai.

- Question ki requirement: Agar question Stack maangta hai, toh append() aur 
                           pop() use karoge. Agar Queue maangta hai, toh 
                           append() ke saath deque ka popleft() use kar sakte 
                           ho.

* Ek hi list ko kabhi Stack aur kabhi Queue ke behaviour mein use kar sakte 
  ho. Lekin iska matlab ye nahi ki dono ke rules same hain.

==============================================================================

4. Ek line mein final concept
-----------------------------

* Stack aur Queue Python ke variable ke naam se decide nahi hote; unmein 
  elements add aur remove karne ke tareeke se unka behaviour decide hota 
  hai.

* Tumne jo observation kiya hai, woh bilkul correct hai. Isi tarah questions 
  karte hue tum Data Structures ko achhe se samajh paoge!