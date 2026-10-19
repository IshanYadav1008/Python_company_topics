* Python: Implement Generator + Advantages (Zero Level Se):

Is topic mein hum 3 cheezein seekhenge:
---------------------------------------
1. Generator khud kaise banate hain.
2. Generator ko run karke values kaise nikalte hain.
3. Generator ke advantages kya hain aur real code mein 
   kab use karna chahiye.

===============================================================================

1. Generator implement karna kya hota hai ?
-------------------------------------------
* Implement generator ka simple matlab hai: Python mein aisa code likhna jo 
                                            values ko ek-ek karke produce 
                                            kare, jab unki zaroorat ho.

Normal function ka example dekho:
---------------------------------
def get_numbers():
    return [10, 20, 30]

numbers = get_numbers()
print(numbers)

Output:
-------
[10, 20, 30]

- Yeh teeno values ek list mein return karta hai.
- Ab wahi kaam generator se karte hain.

===============================================================================

2. Apna pehla generator banao:
------------------------------

def get_numbers():
    yield 10
    yield 20
    yield 30

numbers = get_numbers()

print(next(numbers))
print(next(numbers))
print(next(numbers))

Output:
-------
10
20
30

- Chalo, is code ko line by line samajhte hain.

-------------------------------------------------------------------------------

Step 1 — Generator function define karna:
-----------------------------------------
def get_numbers():    
yield 10    
yield 20    
yield 30


- def function banata hai.
- get_numbers function ka naam hai.
- yield ek value deta hai aur execution ko pause karta hai. 

-------------------------------------------------------------------------------

Step 2 — Generator object banana:
---------------------------------
=> numbers = get_numbers()

- Yahan numbers mein 10, 20, 30 ki list nahi hai. Ismein ek 
  generator object hai jo in values ko produce kar sakta hai.

-------------------------------------------------------------------------------

Step 3 — Pehli value nikalna:
----------------------------
=> print(next(numbers))

Output:
-------
10

- Generator pehle yield 10 tak chalta hai aur pause ho jata hai.

-------------------------------------------------------------------------------

Step 4 — Agli value nikalna:
----------------------------
=> print(next(numbers))

Output:
-------
20

- Generator dobara shuru se nahi chalta. Woh apni pichhli position 
  se aage continue karta hai.

-------------------------------------------------------------------------------

Step 5 — Teesri value nikalna:
------------------------------
=> print(next(numbers))

Output:
-------
30

- Teesri value ke baad generator complete ho jata hai. Ab dobara 
  next(numbers) call karoge, toh StopIteration exception aayega.

===============================================================================

3. next() ke bina generator kaise use karein ? 

- Har value ke liye manually next() call karna zaroori nahi hai. 
  Tum for loop use kar sakte ho.

CODE:
-----
def get_numbers():
    yield 10
    yield 20
    yield 30

for number in get_numbers():
    print(number)

Output:
-------
10
20
30

for loop automatically:
-----------------------
- Generator se next value leta hai.
- Value ko number mein rakhta hai.
- Loop ke andar ka code chalata hai.
- Generator complete hone par loop rok deta hai.

* Beginner ke liye rule: Generator ki saari values process karni hon, 
                         toh aam taur par for loop sabse convenient 
                         hai.

===============================================================================

4. Real example: Even numbers ka generator:

* Maan lo tumhe 1 se 10 tak sirf even numbers chahiye.

CODE:
-----
def even_numbers():
    for number in range(1, 11):
        if number % 2 == 0:
            yield number

for num in even_numbers():
    print(num)

Output:
-------
2
4
6
8
10


Code ke andar kya ho raha hai ?
-------------------------------
- range(1, 11) numbers 1 se 10 tak deta hai.
- number % 2 == 0 check karta hai ki number even hai ya nahi.
- Even hone par yield number us value ko produce karta hai.
- Odd number par yield execute nahi hota, isliye generator 
  agli iteration par chala jata hai.

* Dhyan do: yield sirf fixed values ke liye nahi hai. Tum loops 
            aur conditions ke saath bhi generator bana sakte ho.

===============================================================================

5. Generator ke advantages

- Yeh copy-friendly table hai:

+----------------------+-----------------------------------------------+
| Advantage            | Simple explanation                            |
+----------------------+-----------------------------------------------+
| 1. Memory efficient  | Saari values ki list ek saath store nahi      |
|                      | karni padti.                                  |
+----------------------+-----------------------------------------------+
| 2. Lazy evaluation   | Value tab produce hoti hai jab maangi jaaye.  |
+----------------------+-----------------------------------------------+
| 3. Large data        | Bahut saari values ko ek-ek karke process     |
|    processing        | kar sakte hain.                               |
+----------------------+-----------------------------------------------+
| 4. Better for        | File ya data stream ko chunks/lines mein      |
|    streams           | process karne mein useful hai.                |
+----------------------+-----------------------------------------------+
| 5. Pause and resume  | yield par execution pause hota hai aur        |
|                      | next request par continue hota hai.           |
+----------------------+-----------------------------------------------+
| 6. Cleaner code      | Values generate karne ka logic ek function    |
|                      | mein rakh sakte hain.                         |
+----------------------+-----------------------------------------------+

- Ab har advantage ko example se samjho.

-------------------------------------------------------------------------------

# Advantage 1: Memory efficient

List se:
--------
numbers = list(range(1, 1000001))
print(sum(numbers))

- Yeh ek million numbers ki list memory mein banata hai.

Generator expression se:
------------------------
numbers = (x for x in range(1, 1000001))
print(sum(numbers))

Dono ka output:
---------------
500000500000

- Lekin generator expression saare numbers ki list nahi banata. 
  sum() values ko ek-ek karke consume karta hai.

- Important: Generator zero memory use nahi karta. Woh apni state 
             rakhta hai aur current value process hoti hai. Bas 
             poori collection ko ek saath store karne ki zaroorat 
             nahi padti.

-------------------------------------------------------------------------------

# Advantage 2: Lazy evaluation

* Lazy evaluation ka matlab hai ki values zaroorat padne par calculate 
  ya produce hoti hain.

CODE:
-----
def demo():
    print("Pehli value")
    yield 100

    print("Doosri value")
    yield 200

g = demo()

print("Generator ready")
print(next(g))

Output:
-------
Generator ready
Pehli value
100

- Doosri value abhi print nahi hui, kyunki humne doosri value
   maangi hi nahi.

Jab yeh chalaoge:
-----------------
=> print(next(g))

Output:
-------
Doosri value
200

- Yahi lazy evaluation hai: poora kaam pehle se execute nahi hota.

-------------------------------------------------------------------------------

Advantage 3: Large data process karna
-------------------------------------

* Maan lo tumhe bahut saari IDs generate karni hain.

CODE:
-----
def generate_ids():
    for i in range(1, 6):
        yield i

for user_id in generate_ids():
    print("Processing user:", user_id)

Output:
-------
Processing user: 1
Processing user: 2
Processing user: 3
Processing user: 4
Processing user: 5

- Har ID ko process karne ke liye pehle saari IDs ki list 
  banane ki zaroorat nahi.

-------------------------------------------------------------------------------

Advantage 4: Files ko line by line read karna
---------------------------------------------

def read_lines(file_name):
    with open(file_name, "r") as file:
        for line in file:
            yield line

- Is generator se file ki lines ek-ek karke mil sakti hain. Badi file 
  ke liye yeh aksar poori file ko ek string ya list mein load karne 
  se zyada memory-efficient hota hai.

- Yeh function tabhi chalega jab tum ise call karke iterate karoge, 
  aur file ko read karne ke liye woh file maujood honi chahiye.

===============================================================================

6. Generator ki limitations bhi samjho:

- Generator har jagah best option nahi hota.

def get_numbers():
    yield 10
    yield 20
    yield 30

g = get_numbers()

print(next(g))
print(next(g))
print(next(g))

<------------------------------------------------------------------>

- Ab generator exhaust ho gaya. Agar values ko dobara use karna hai, 
  toh naya generator banana padega.

=> g = get_numbers()

<------------------------------------------------------------------>

- List ki tarah generator par directly indexing bhi nahi kar sakte:

g = get_numbers()# 
print(g[0])  # TypeError

- Agar tumhe values baar-baar chahiye, indexing karni hai ya 
  poori collection par multiple passes karne hain, toh list 
  zyada convenient ho sakti hai.

===============================================================================

7. Final comparison:

+------------------------+--------------------------+-------------------------+
| Requirement            | List                     | Generator               |
+------------------------+--------------------------+-------------------------+
| Saari values ek saath  | Haan                     | Nahi, on-demand values  |
| Store karna            |                          | produce karta hai       |
+------------------------+--------------------------+-------------------------+
| Indexing, jaise [0]    | Haan                     | Directly nahi           |
+------------------------+--------------------------+-------------------------+
| Values dobara use      | Haan                     | Exhaust hone par naya   |
| karna                  |                          | generator chahiye       |
+------------------------+--------------------------+-------------------------+
| Bahut saari values     | Memory zyada lag sakti   | Memory bach sakti hai   |
| process karna          | hai                      |                         |
+------------------------+--------------------------+-------------------------+

Yaad rakhna:
------------
- yield generator function ke andar values produce karta hai.

- next() agla yielded value nikalta hai.

- for loop generator ko automatically consume karta hai.

- Generator tab useful hai jab values ko ek-ek karke process 
  karna ho.

- List tab useful hai jab saari values store karke baar-baar 
  access karni hon.