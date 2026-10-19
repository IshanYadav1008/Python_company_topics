Hum 4 cheezein seekhenge:
-------------------------
1. yield kya hai aur kyun use hota hai.
2. yield function ko pause kaise karta hai.
3. next() function ko resume kaise karta hai.
4. Function ki execution state kaise preserve hoti hai.

==============================================================================

Part 1 — yield kya hai?
-----------------------

* Sabse pehle ek normal function dekho.

CODE:
-----
def test():
    print("Hello")
    return 10

result = test()
print(result)

Output:
-------
Hello
10

Yahan kya hua ?
---------------
- test() call hua.
- "Hello" print hua.
- return 10 ne value 10 wapas di.
- Function khatam ho gaya.

------------------------------------------------------------------------------

* Ab isi tarah ka function yield se banate hain:

CODE:
-----
def test():
    print("Hello")
    yield 10

g = test()
print(next(g))

Output:
-------
Hello
10

- Output dekhne mein similar hai, lekin andar ka behavior alag hai.

- yield generator function mein value produce karta hai aur function 
  ki execution ko temporarily pause kar deta hai. Baad mein jab agli 
  value maangi jaati hai, function wahi se continue kar sakta hai.

Ek important baat: yield wala function call karne par generator object 
                   banta hai. Function ka body tab execute hota hai jab 
                   tum next() ya for loop se values maangte ho.

==============================================================================

Part 2 — yield function ko pause kaise karta hai ?

* Ab ek important example lete hain.

CODE:
-----
def test():
    print("A")
    yield 10

    print("B")
    yield 20

    print("C")
    yield 30

g = test()

- Abhi tak "A", "B" ya "C" kuch bhi print nahi hua, kyunki humne sirf 
  generator object banaya hai.

- Ab ek-ek karke execute karte hain.

------------------------------------------------------------------------------

# STEP-1:

CURRENT ACTION
---------------
Abhi tak koi next() call nahi hua

OUTPUT
------
Koi output nahi

- g = test() se sirf generator object bana hai. Function body abhi 
             execute nahi hui.

------------------------------------------------------------------------------

# STEP-2:

CURRENT ACTION
--------------
next(g)

OUTPUT
------
A
10

- Function start hua, A print hua, phir yield 10 ne value di aur 
  function pause ho gaya.

------------------------------------------------------------------------------

# STEP-3:

CURRENT ACTION
--------------
next(g)

OUTPUT
------
B
20

- Function A ke baad se nahi, balki yield 10 ke baad se continue hua. 
  B print hua, phir 20 return hua.

------------------------------------------------------------------------------

# STEP-3:

CURRENT ACTION
--------------
next(g)

OUTPUT
------
C
30

- Function yield 20 ke baad se resume hua. C print hua, phir 30 mila.

------------------------------------------------------------------------------

# STEP-4:

CURRENT ACTION
--------------
next(g)

OUTPUT
------
StopIteration

- Generator ke paas ab aur koi yield nahi hai. Function khatam ho chuka 
  hai.

------------------------------------------------------------------------------

* Is simulator mein steps change karke dekho. Tum notice karoge ki har 
  next(g) par function shuru se execute nahi hota.

* Yahi yield ka sabse important behavior hai: pause karo, value do, phir 
  wahi se resume karo.

==============================================================================

Part 3 — Function ko resume kaise karta hai?
--------------------------------------------

* Ye code dekho:

CODE:
-----
def test():
    print("Start")
    yield 1

    print("Middle")
    yield 2

    print("End")

g = test()

print("First call")
print(next(g))

print("Second call")
print(next(g))

Output:
-------
First call
Start
1
Second call
Middle
2

- Dhyan do, "End" print nahi hua. Kyun? Kyunki doosre next(g) ke baad 
  function yield 2 par pause hua. Function ke end tak abhi execution 
  nahi pahunchi.

------------------------------------------------------------------------------

* Agar tum teesri baar next(g) call karoge:

=> print(next(g))

To output hoga:
---------------
End
StopIteration


* End print hone ke baad function khatam ho gaya. Isliye agli value 
  available nahi hai aur Python StopIteration exception raise karta 
  hai.

==============================================================================

Part 4 — Function apni state kaise yaad rakhta hai?
---------------------------------------------------

* Ab deep concept samjho.

CODE:
-----
def counter():
    x = 1
    yield x

    x = x + 1
    yield x

    x = x + 1
    yield x

g = counter()

print(next(g))
print(next(g))
print(next(g))

Output:
-------
1
2
3

------------------------------------------------------------------------------

* Tum soch sakte ho ki doosre next(g) par x dobara 1 kaise nahi hua?

  Kyunki generator apni execution state preserve karta hai. Ismein 
  local variable x ki current value aur execution kahan tak pahunchi 
  thi, ye information shamil hoti hai.

State kaise change hoti hai?
----------------------------
x = 1              x = 2                x = 3 
Pehla yield        Doosra yield         Teesra yield  

* Har baar execution purani state se resume hoti hai. x ko dobara 
  initialize nahi kiya jaata.

------------------------------------------------------------------------------

* Agar hum isi function mein return use karte:

CODE:
-----
def counter():
    x = 1
    return x

g = counter()

- To function ek baar 1 dekar khatam ho jata. Uske baad function ki 
  execution resume karne ke liye generator object nahi hota.

==============================================================================

Part 5 — yield vs return:
-------------------------

Feature	                yield	                  return
------------------------------------------------------------------------------
Kaam	                Value produce karta hai	  Function ka result deta hai
------------------------------------------------------------------------------
Function	            Pause hota hai	          Khatam ho jata hai
------------------------------------------------------------------------------
Dobara execution	    Agle request par resume   Usi function call ko resume 
                        hoti hai                  nahi kar sakte
------------------------------------------------------------------------------
Multiple values	        Ek-ek karke de sakta hai  Ek return se function exit 
                                                  hota hai
------------------------------------------------------------------------------
Use	                    Generator functions	      Normal functions aur generator 
                                                  ko end karne ke liye bhi
------------------------------------------------------------------------------

* Ek subtle point: generator function ke andar return bhi ho sakta hai. 
  Wahan return generator ko end kar deta hai; agar return ke saath value 
  di gayi ho, toh woh StopIteration ke value attribute mein hoti hai, 
  agla yielded item nahi banti.

==============================================================================

Part 6 — Real-life use kahan hota hai?
--------------------------------------

* Maan lo ek file mein hazaaron lines hain aur tumhe ek-ek line padhni 
  hai.

CODE:
-----
def read_numbers():
    for number in range(1, 1001):
        yield number

for number in read_numbers():
    print(number)

- Generator har number ko zaroorat ke hisaab se produce karta hai. 
  Saari values ki list pehle banane ki zaroorat nahi hoti.

- File processing, large datasets aur streaming jaise kaamon mein 
  ye useful hota hai.

==============================================================================

Part 7 — Ab tumhari practice:
-----------------------------

Question 1: Is code ka output kya hoga?

CODE:
-----
def demo():
    print("A")
    yield 5
    print("B")
    yield 10

g = demo()
print(next(g))
print(next(g))

O/P: A, 5, B, 10

Correct!
--------
- Pehla next(g) "A" print karke 5 deta hai. Doosra next(g) resume 
  karke "B" print karta hai aur 10 deta hai.

Final revision:
---------------
- yield            = value produce karo aur function pause karo.
- next(g)          = generator ko start ya resume karke agli value lo.
- Generator state  = execution position aur local variables ki current state.
- Generator khatam = aur values nahi; next() par StopIteration.