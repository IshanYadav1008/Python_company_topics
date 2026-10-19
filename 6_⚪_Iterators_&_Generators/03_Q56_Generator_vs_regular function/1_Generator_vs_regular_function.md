Python: Generator vs Regular Function — Zero Level Se
-----------------------------------------------------

* Sabse pehle ek basic baat samjho: Python mein regular function 
  aur generator function dono kaam karne ke liye hote hain, lekin 
  dono result dene ka tareeka alag hota hai.
 
1. Regular function kya hota hai ?
----------------------------------
- Regular function woh function hai jo aam taur par return se result 
  deta hai.

CODE:
-----
def get_number():
    return 10

result = get_number()
print(result)

Output:
-------
10

----------------------------------------------------------------------------

Step-by-step samjho:
--------------------

Step 1: get_number() call hua.
      - Function ke andar execution shuru hua.

Step 2: return 10 execute hua.
      - Function ne result 10 wapas de diya aur 
        function call khatam ho gaya.

Step 3: result mein 10 store hua.
      - Isliye print(result) ne 10 print kiya.

----------------------------------------------------------------------------

* Ab multiple values wala example dekho:

CODE:
-----
def get_numbers():
    return [10, 20, 30]

result = get_numbers()
print(result)

Output:
-------
[10, 20, 30]

- Yahan function ne teeno numbers ek saath list ke roop mein return kiye.

- Dhyan do : Regular function bhi multiple values de sakta hai, lekin agar 
             list return kar raha hai, toh list ke saare elements ek saath 
             ban kar return hote hain.

============================================================================

2. Generator function kya hota hai?

* Generator function woh function hai jo yield ka use karke values ko ek-ek 
  karke produce kar sakta hai.

CODE:
-----
def get_numbers():
    yield 10
    yield 20
    yield 30

g = get_numbers()

print(next(g))
print(next(g))
print(next(g))

Output:
-------
10
20
30

----------------------------------------------------------------------------

Step-by-step samjho:
--------------------

Step 1: Generator function define hua.

CODE:
-----
def get_numbers():
    yield 10
    yield 20
    yield 30

- Yeh function yield use karta hai, isliye yeh generator 
  function hai.

<-------------------------------------------------------->

Step 2: Function call hua.

=> g = get_numbers()

- Abhi 10, 20, 30 print nahi hue. g ke andar ek generator 
  object mila hai.

<-------------------------------------------------------->

Step 3: Pehli baar next(g) chala.

=> print(next(g))

Output:
-------
10

- Generator ne yield 10 tak execution ki, 10 diya aur wahi 
  pause ho gaya.

<-------------------------------------------------------->

Step 4: Doosri baar next(g) chala.

=> print(next(g))

Output:
-------
20

- Generator wahi se continue hua jahan pehle pause hua tha. 
  Usne yield 20 par 20 diya aur phir pause ho gaya.

<-------------------------------------------------------->

Step 5: Teesri baar next(g) chala.

=> print(next(g))

Output:
-------
30

- Generator ne 30 diya. Uske baad generator khatam ho jayega. 
  Ek aur next(g) karoge toh StopIteration exception aayega.

============================================================================

3. Sabse important difference:

* Is example ko dhyan se dekho:

CODE:
-----
def regular():
    print("A")
    return 10
    print("B")

def generator():
    print("A")
    yield 10
    print("B")
    yield 20

Regular function ko call karte hain:
------------------------------------
x = regular()
print("C")

Output:
-------
A
C

- B print nahi hua, kyunki return 10 ke baad function khatam 
  ho gaya. Uske baad wali line execute nahi hoti.

<----------------------------------------------------------->

# Ab generator ko call karte hain:

g = generator()
print("C")

Output:
-------
C

* Abhi A bhi print nahi hua! Kyunki generator function call 
  karne se generator object banta hai, lekin uski body 
  execute nahi hoti.

Ab yeh chalao:
--------------
print(next(g))

Output:
-------
A
10

# Phir:
=> print(next(g))

Output:
-------
B
20

- Yahi main difference hai: return function ko khatam karta hai, 
  jabki yield value dekar execution ko pause karta hai.

============================================================================

4. Regular function vs Generator — Copy-friendly table:

* Neeche wali table ko seedha copy kar sakte ho:

+----------------------+---------------------------+------------------------------+
| Point                | Regular Function          | Generator Function           |
+----------------------+---------------------------+------------------------------+
| Main keyword         | return                    | yield                        |
+----------------------+---------------------------+------------------------------+
| Function call        | Body execute hoti hai     | Generator object milta hai   |
|                      |                           |; body abhi execute nahi hoti.|
+----------------------+---------------------------+------------------------------+
| Result               | Ek result ya collection   | Values ek-ek karke de sakta  |
|                      | return kar sakta hai      | hai.                         |
+----------------------+---------------------------+------------------------------+
| Execution            | return par khatam         | yield par pause, phir resume |
+----------------------+---------------------------+------------------------------+
| State                | Function call khatam      | Local state aur position     |
|                      | hone par normal flow end  | preserve hoti hai.           |
+----------------------+---------------------------+------------------------------+
| Values lena          | Function call se result   | next() ya for loop se values |
|                      | milta hai                 | le sakte hain.               |
+----------------------+---------------------------+------------------------------+
| Memory               | Collection banaye toh     | Values on-demand produce     |
|                      | collection memory leti hai| karke memory bacha sakta hai.|
+----------------------+---------------------------+------------------------------+
| Best use             | Final answer, total,      | Large data, streams,         |
|                      | calculation               | on-demand values             |
+----------------------+---------------------------+------------------------------+ 

============================================================================

5. Memory ka difference — ek real example:

* Maan lo tumhe 1 se 1,000,000 tak numbers process karne hain.

Regular function: poori list return karna
-----------------------------------------
def get_numbers():
    return list(range(1, 1_000_001))

numbers = get_numbers()
print(sum(numbers))

- Yeh poori list memory mein banata hai.

----------------------------------------------------------------------------

Generator: numbers ko ek-ek karke produce karna
-----------------------------------------------
def get_numbers():
    for number in range(1, 1_000_001):
        yield number

numbers = get_numbers()
print(sum(numbers))

Output dono ka same hoga:
-------------------------
500000500000

- Lekin generator wala version poori list store nahi karta. sum() generator 
  se ek-ek value leta hai aur total calculate karta hai.

- Important: Generator har situation mein automatically faster nahi hota. 
             Agar saari values ek saath chahiye aur baar-baar use karni 
             hain, toh list convenient ho sakti hai. Generator ka fayda 
             tab hota hai jab values ko ek-ek karke process karna useful 
             ho.

============================================================================

6. Ek chhota test — samajh check karo:

* Question: Is code ka output kya hoga?

CODE:
-----
def demo():
    print("Start")
    yield 5
    print("End")

g = demo()
print("Ready")
print(next(g))

O/P: Ready, Start, 5

Bilkul sahi!
------------
- Ready pehle print hota hai. next(g) par Start print hota hai, 
  phir yield 5 se 5 milta hai. End abhi execute nahi hota.

Yaad rakhne ka shortcut:
------------------------
- return    = result do aur function se bahar aa jao.
- yield     = value do, pause ho jao, baad mein wahi se continue karo.
- Generator = values ko zaroorat ke hisaab se ek-ek karke lene ka tareeka.