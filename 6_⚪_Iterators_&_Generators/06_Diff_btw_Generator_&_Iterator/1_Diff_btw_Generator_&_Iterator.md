* Bhai, tumhara confusion bilkul valid hai.Generator aur iterator same 
  jaise lagte hain kyunki generator bhi iterator hota hai! Dono mein 
  next() chalta hai, dono values dete hain aur dono objects hote hain.

* Lekin asli difference samajhne ke liye ek cheez pakdo: value dene ka 
  mechanism kaun banata hai — Python automatically, ya tum khud?

------------------------------------------------------------------------------

1. Sabse pehle ek example dekho:
--------------------------------

A. Generator
------------
def numbers():
    yield 10
    yield 20
    yield 30

g = numbers()
print(next(g))
print(next(g))

Output:
-------
10
20

- Tum yield likhte ho. Python khud yaad rakhta hai ki function kahan 
  ruka tha aur agli value kaise deni hai.

------------------------------------------------------------------------------

B. Custom Iterator
------------------
class Numbers:
    def __init__(self):
        self.n = 10

    def __iter__(self):
        return self

    def __next__(self):
        if self.n > 30:
            raise StopIteration

        result = self.n
        self.n += 10
        return result

it = Numbers()
print(next(it))
print(next(it))

Output:
-------
10
20

* Tum class banate ho. Tum khud define karte ho ki agli value kya 
  hogi, state kaise badlegi aur kab rukna hai.

- Dekha? Output same hai. next() bhi same hai. Lekin andar ka 
  mechanism alag hai.

==============================================================================

2. Asli difference: kaam kaun kar raha hai?

Generator mein:
---------------
def numbers():
    yield 10
    yield 20
    yield 30

* Tum Python ko bas bata rahe ho: pehle 10 do, phir 20, phir 30.

Baaki kaam Python sambhalta hai:
--------------------------------
- Function ki execution kahan pause hui.
- Agli baar kahan se continue karna hai.
- Local variables ki state preserve karna.
- Generator khatam hone par iteration stop karna.

------------------------------------------------------------------------------

Custom iterator mein:
---------------------
class Numbers:
    def __iter__(self):
        return self

    def __next__(self):
        # Agli value ka logic tum likhte ho
        ...

Tumhe khud define karna padta hai:
----------------------------------
- Agli value kya hogi.
- Current state kaise store hogi.
- State kaise update hogi.
- Items khatam kab honge.

* Yahi implementation ka main difference hai.

==============================================================================

3. Lekin ek bahut important baat!
---------------------------------

* Iterator ek category/interface hai; generator uska ek specific 
  type hai.

Iska matlab:
------------
- Har generator iterator hota hai.
- Lekin har iterator generator nahi hota.

Example:
--------
g = (x for x in range(3))

print(next(g))       # 0
print(iter(g) is g)  # True

* Generator g iterator hai. iter(g) wahi object return karta hai.

------------------------------------------------------------------------------

# List iterator bhi bana sakte ho:

it = iter([10, 20, 30])

print(next(it))  # 10
print(iter(it) is it)  # True

- Yeh bhi iterator hai, lekin generator nahi. Yeh list ka iterator 
  hai, jo Python ke built-in mechanism se bana hai.

==============================================================================

4. Ek table mein clear difference:
----------------------------------

+----------------------+--------------------------+---------------------------+
| Point                | Generator                | Iterator                  |
+----------------------+--------------------------+---------------------------+
| Kya hai?             | Iterator ka ek type      | Agli value dene wala      |
|                      |                          | object / protocol         |
+----------------------+--------------------------+---------------------------+
| Kaise banate hain?   | yield wali function ya   | iter() se built-in        |
|                      | generator expression     | iterator, ya custom class |
+----------------------+--------------------------+---------------------------+
| next()               | Haan                     | Haan                      |
+----------------------+--------------------------+---------------------------+
| Object banta hai?    | Haan                     | Haan                      |
+----------------------+--------------------------+---------------------------+
| State kaun sambhalta?| Python generator ke      | Iterator ke implementation|
|                      | liye automatically       | par depend karta hai      |
+----------------------+--------------------------+---------------------------+
| Agli value ka logic  | yield aur function code  | __next__() mein define    |
|                      | se chalta hai            | hota hai                  |
+----------------------+--------------------------+---------------------------+
| Kya har iterator     | Haan, generator khud     | Nahi                      |
| generator hota hai?  | iterator hai             |                           |
+----------------------+--------------------------+---------------------------+

==============================================================================

5. Ek real-life example se samjho:
----------------------------------

* Socho tumhe ek machine banani hai jo ek-ek karke tickets de.

Generator = Simple ticket instructions
--------------------------------------
- Tum likhte ho: ticket 1 do, phir ticket 2 do, phir ticket 3 do. 
  Python pause aur resume sambhalta hai.

Custom iterator = Apni ticket machine
-------------------------------------
- Tum machine ki class aur logic design karte ho: counter kaise 
  badhega aur tickets khatam kab hongi.

* Dono ka output numbered tickets ho sakta hai. Farak ticket ke 
  number mein nahi, balki machine banane ke tareeke mein hai.

==============================================================================

6. Ab tumhara main confusion solve karte hain:
----------------------------------------------

Tumne kaha : Dono mein next() hai, function call hota hai, value return 
             hoti hai aur objects bante hain.

Bilkul sahi! Bas ek correction:
-------------------------------
- Generator function call karne par generator object banta hai; function 
  ki body turant execute nahi hoti.

- Custom iterator mein aam taur par class ka object banta hai; next() 
  uske __next__() method ko call karta hai.

- Dono next() se agla item dete hain, isliye dono iteration protocol 
  follow karte hain.

* Yaani next() common hona koi difference nahi hai — balki yahi batata 
  hai ki generator bhi iterator hai.

------------------------------------------------------------------------------

Ek final question:
------------------

* Agar tum likhte ho:

def count():
    yield 1
    yield 2

O/P: Generator bhi hai aur iterator bhi

Bilkul sahi!
------------
Generator, iterator ka special type hai. Isliye usmein next() 
bhi kaam karta hai.

* as ye line yaad rakhna: Iterator batata hai object agla item kaise dega; 
  generator us tarah ka iterator banane ka ek aasaan tareeka hai, jismein 
  tum yield likhte ho aur Python pause/resume sambhalta hai.