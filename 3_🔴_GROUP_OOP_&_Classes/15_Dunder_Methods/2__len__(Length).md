1. __len__ hota kya hai ?

* __len__ Python ka ek special method hai, jo kisi object ki length 
  ya size batane ke liye use hota hai.

Jaise normal Python mein:
-------------------------
name = "Rahul"
numbers = [10, 20, 30]

print(len(name))
print(len(numbers))

Output:
-------
5
3

- "Rahul" mein 5 characters hain.
- [10, 20, 30] mein 3 items hain.

* Python ko in built-in objects ki length nikalna pehle se aata 
  hai.

* Lekin agar hum apni khud ki class banayein, toh Python ko kaise 
  pata chalega ki us object ki length kya hai ? 

* Hum __len__ method define karke Python ko batate hain ki length 
  kaise nikalni hai.

============================================================================

2. Apni class mein __len__ kaise use karein ?

* Maan lo hum ek Bag class bana rahe hain, jismein kuch items hain.

Bag object
----------
Ball
Book
Pen

Total items = 3

Ab code dekho:
--------------
class Bag:
    def __init__(self):
        self.items = ["Ball", "Book", "Pen"]

    def __len__(self):
        return len(self.items)

bag1 = Bag()
print(len(bag1))

Output:3

* Ab is code ko ek-ek line karke samajhte hain.

============================================================================

3. Code ko line-by-line samjho:

Step 1 — Class banana
---------------------
class Bag:

- Humne Bag naam ki class banayi. Ye ek blueprint hai.

<-------------------------------------------------------->

Step 2 — Items store karna:
---------------------------
def __init__(self):
    self.items = ["Ball", "Book", "Pen"]

- Jab hum Bag() ka object banayenge, toh uske items attribute 
  mein ye list store hogi.

<-------------------------------------------------------->

Step 3 — Length ka rule define karna:
-------------------------------------

def __len__(self):
    return len(self.items)

- Iska matlab hai: jab Python is object ki length pooche, 
                   toh self.items ki length return kar do.

- Yahan len(self.items) list ki built-in length nikalta hai, 
  jo 3 hai.

<-------------------------------------------------------->

Step 4 — Object banana
----------------------
=> bag1 = Bag()

- Ab bag1 ek Bag object ko refer karta hai.

<-------------------------------------------------------->

Step 5 — Length poochna:
------------------------
=> print(len(bag1))

* Python bag1 ki length nikalne ke liye uske __len__ method ko 
  use karta hai. Method 3 return karta hai aur print() use 
  screen par dikhata hai.

============================================================================

4. Poora flow ek diagram mein:

bag1 = Bag()
Bag object banta hai
       |
bag1.items
["Ball", "Book", "Pen"]
       |
len(bag1)
Python __len__() ko call karta hai
       |
return len(self.items)
List ki length = 3
       |
Output: 3

============================================================================

5. Ek important difference samjho:

In dono mein difference dekho:
------------------------------

Code	                Matlab
-----------------------------------------------------------------
len(bag1)	            Python ke normal syntax se length maangna
-----------------------------------------------------------------
bag1.__len__()	        Method ko directly call karna
-----------------------------------------------------------------
return len(self.items)	Items ki length nikal kar result dena
-----------------------------------------------------------------

- Normal Python code mein len(bag1) likhna preferred hai, direct 
  bag1.__len__() nahi.

- Aur yaad rakho: __len__ ko apni class mein define karna zaroori 
  nahi hai, agar tumhe object ke liye length ka behavior chahiye 
  hi nahi.

- Ek aur baat: __len__ ko non-negative integer return karna chahiye. 
               Agar method define nahi hai ya galat result deta hai, 
               toh len(obj) par error aa sakta hai.

============================================================================

6. Ab tum khud try karo:

* Neeche wale code mein list mein 4 fruits hain:

CODE:
-----
class Basket:
    def __init__(self):
        self.fruits = ["Apple", "Mango", "Banana", "Grapes"]

    def __len__(self):
        return len(self.fruits)

b1 = Basket()
print(len(b1))

- Tumhare hisaab se output kya aayega ?

ANS)
----
Bilkul sahi! Output 4 hai.
List mein 4 fruits hain. __len__ unki length return karta hai.

* Bas main concept ye hai: __len__ tumhari class ke object ke liye length 
                           nikalne ka rule define karta hai, jise Python 
                           len(object) ke through use kar sakta hai. Ab agla 
                           Dunder Method __eq__ hai, jo do objects ko == se 
                           compare karne ka behavior define karta hai.

============================================================================
----------------------------------------------------------------------------
============================================================================

Doubt:
------
mera ek sawal hai ?
pehle toh ye method call ho kaise raha hai or kon ise call kr rha 
hai ye batao

 def __len__(self):
        return len(self.items)

jab yha se return len(self.items) hum length nikal rhe hai toh phir 
yha waous se ye print(len(bag1)) likhne ka kya mtlb hai mtlb len ??

----------------------------------------------------------------------------

ANS)
----
Bahut achha sawal hai! Tum actually Python ke andar ho kya raha hai, 
woh samajhna chahte ho. Chalo ek-ek karke dekhte hain.

Tumhare 2 questions hain:
-------------------------
1. __len__(self) ko call kaun kar raha hai ?

2. Jab return len(self.items) se length nikal rahe hain, toh 
   print(len(bag1)) mein dobara len() kyun likha hai ??

============================================================================

1. Sabse pehle ye code dekho:

CODE:
-----
class Bag:
    def __init__(self):
        self.items = ["Ball", "Book", "Pen"]

    def __len__(self):
        return len(self.items)

bag1 = Bag()
print(len(bag1))

- Is code mein len(bag1) Python ka built-in function call hai, 
  aur Python is function ke through tumhare object ke __len__() 
  method ko call karta hai.

Yaani:
------
- len()     — Python ka pehle se bana hua function hai.
- __len__() — tumhari class mein define kiya gaya method hai.
- bag1      — woh object hai jiski length tum pooch rahe ho.

============================================================================

2. Method ko call kaun kar raha hai ?

- Jawab: Python ka built-in len() function.

Is flow ko dekho:
-----------------

Tum likhte ho
len(bag1)
        |
Python ka built-in len() function
Check karta hai ki object length support karta hai ya nahi
        |
Bag.__len__()
Python tumhare method ko call karta hai
        |
return len(self.items)
List ki length nikalti hai = 3
        |
len(bag1) ka result = 3
Phir print() us result ko dikhata hai

* Tumhe apne code mein explicitly bag1.__len__() call nahi 
  karna padta. len(bag1) likhne par Python khud appropriate 
  special method ko use karta hai.

============================================================================

3. Ab tumhara doosra sawaal: len() do baar kyun hai ?

Code ki in dono lines ko alag samjho:
-------------------------------------
=> return len(self.items)

=> print(len(bag1))

- Dono jagah len() hai, lekin dono alag cheezon ki length 
  nikal rahe hain.

----------------------------------------------------------------------------

Pehla len() — list ki length:
-----------------------------

=> return len(self.items)

- Yahan self.items ki value hai:
=> ["Ball", "Book", "Pen"]

- Python is list ki length nikalta hai:
=> len(self.items)  # 3

- Phir return 3 hota hai. Matlab tumhara __len__() method 3 
  wapas deta hai.

----------------------------------------------------------------------------

Doosra len() — Bag object ki length:
------------------------------------
=> print(len(bag1))

- Yahan bag1 ek Bag object hai, list nahi.

- Python ko bataya gaya hai ki Bag object ki length kaise nikalni 
  hai: uske __len__() method ke through.

- Woh method andar jaakar self.items ki length nikalta hai aur 3 
  return karta hai. Uske baad print() ko 3 milta hai aur woh use 
  display karta hai.

============================================================================

4. Ek real-life example:

* Maan lo tum kisi dukaan par poochte ho:

- Tum: "Is bag mein kitne items hain?"

- Python ka len(): "Theek hai, Bag object se iska jawab poochta 
  hoon."

- Tumhara __len__(): "Mere bag ki items list mein 3 items hain."

- len(): "Mujhe jawab 3 mil gaya."

- print(): Screen par 3 dikha deta hai.

* Yeh sirf samajhne ke liye analogy hai, lekin code ka flow bhi 
  isi tarah hai.

============================================================================

5. Ek aur important cheez: self kya hai?

Jab tum likhte ho:
------------------
bag1 = Bag()
print(len(bag1))

* Python bag1 object ke __len__() method ko use karta hai. Is call 
  mein self usi object ko refer karta hai, yaani bag1.

sliye:
------
self.items

ka matlab hai:
--------------
bag1.items

<---------------------------------------------------->

Aur:
----
return len(self.items)

ka matlab hai:
--------------
return len(bag1.items)

----------------------------------------------------------------------------

* Yahan doosra code sirf samjhane ke liye equivalent form hai; method ke 
  andar aam taur par self.items hi likhte hain.

Ek line mein yaad rakho:
------------------------
- print(len(bag1)) → Python ka len() → tumhara __len__() → len(self.items) 
  → 3 return → print() output dikhata hai.

- Isliye len() ko do baar likhne ka matlab same length ko do baar nikalna 
  nahi hai. Bahar wala len() tumhare Bag object ki length poochta hai, 
  aur andar wala len() uski items list ki length nikalta hai.