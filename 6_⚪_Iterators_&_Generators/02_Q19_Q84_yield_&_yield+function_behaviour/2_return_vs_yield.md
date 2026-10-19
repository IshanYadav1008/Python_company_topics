Sabse pehle ek line yaad rakho:
-------------------------------

- return = result do aur function ka kaam khatam karo.
- yield  = ek value do, function ko pause karo aur baad mein 
           wahin se continue karo.

* Ab isko practically samajhte hain.

============================================================================

1. Ek hi example, dono tareekon se:
-----------------------------------

* Maan lo humein ek function se number 10 chahiye.

# return

CODE:
-----
def test():
    return 10

x = test()
print(x)

Output:
-------
10

- Kya hua? Function ne 10 diya aur apna kaam khatam kar diya.

----------------------------------------------------------------------------

# yield

CODE:
-----
def test():
    yield 10

g = test()
print(next(g))

Output:
-------
10

- Kya hua? Function ne 10 diya aur pause ho gaya. Function technically 
  abhi complete nahi hua; agla next() use aage chalayega.

----------------------------------------------------------------------------

- Dono ka output 10 hai. Lekin andar ka behavior alag hai.

- Ek important baat: yield wale example mein test() call karne se pehle hi 
                     10 nahi milta. Pehle generator object banta hai, phir 
                     next(g) se value milti hai.

============================================================================

2. Sabse important difference: function khatam hota hai ya pause ?

* Ab ye code dekho.

# return ke saath:
------------------
def demo():
    print("A")
    return 10
    print("B")

demo()

Output:
-------
A

- "B" print nahi hua, kyunki return aate hi function khatam ho gaya.

----------------------------------------------------------------------------

# yield ke saath:
-----------------
def demo():
    print("A")
    yield 10
    print("B")
    yield 20

g = demo()

print(next(g))
print(next(g))

Output:
-------
A
10
B
20

----------------------------------------------------------------------------

# Is baar "B" bhi print hua. Kyun?

1. Pehla next(g) function ko chalata hai.

2. "A" print hota hai.

3. yield 10 value deta hai aur function pause hota hai.

4. Doosra next(g) wahin se function ko resume karta hai.

5. "B" print hota hai aur yield 20 value deta hai.

- Yahi core difference hai: return function ko exit karta hai, jabki
                            yield generator ko suspend karta hai.

============================================================================

3. Real-life example: ek baar result chahiye ya baar-baar values?

* Maan lo tum ek shop ka total bill calculate kar rahe ho.

<-------------------------------------------------------------->

Case A — return
---------------
* Tumhe poore bill ka total chahiye, jaise ₹500.

def total_bill():    
return 500

- Yahan ek final result chahiye. return sahi choice hai.

<-------------------------------------------------------------->

Case B — yield
--------------
* Tumhe bill ki items ek-ek karke dikhani hain.

def items():    
yield "Book"    
yield "Pen"    
yield "Bag"

- Yahan multiple values ek-ek karke chahiye. yield useful 
  hai.

<-------------------------------------------------------------->

Dhyan rahe, return bhi list de sakta hai:
-----------------------------------------

def items():    
return ["Book", "Pen", "Bag"]

- Toh multiple values dene ke liye yield compulsory nahi hai. 
  Difference ye hai ki return yahan poori list ek saath deta 
  hai, jabki yield values ko ek-ek karke produce kar sakta 
  hai.

============================================================================

4. Dono ka result bhi alag hota hai:
-----------------------------------

* Ye point beginners ko confuse karta hai.

CODE:
-----
def normal():
    return 10

def generator():
    yield 10

print(normal())
print(generator())

Output kuch aisa hoga:
----------------------
10
<generator object generator at ...>

Kyun?
-----
- normal() ka result seedha 10 hai.
- generator() ka result generator object hai.
- Generator ki value lene ke liye next() call karna hoga.

<-------------------------------------------------------------->

g = generator()
print(next(g))

Output:
-------
10

- Isliye yield ko return ka bas doosra version mat samajhna. 
  Dono ka behavior aur use alag hai.

============================================================================

5. return kab aur yield kab use karna chahiye ?

+--------------------------------------+----------------+-------------------
| Situation                            | Kya use karein | Kyun?    |
+-------------------------------------+------------------------------------+
| Ek final result chahiye              | return         | Function ka kaam 
                                                        | complete ho jata 
                                                        | hai.
+--------------------------------+------------------------------------------+
| Total, average ya answer chahiye     | return         | Ek final result 
                                                        | milta hai.    
+------------------------------- +------------------------------------------+
| Values ek-ek karke generate karni    | yield          | Values ek-ek karke 
  hain                                                  | milti hain.
+----------------------------------+----------------------------------------+
| Bahut saara data process karna hai   | yield          | Saara data ek saath 
                                                        | store nahi karna
|                                      |                | padta, isliye memory
                                                        | bach sakti hai.
+--------------------------------------+----------------+---------------------
| Execution pause karke continue karni | yield          | Generator apni state 
                                                        | preserve karta hai.
+--------------------------------------+----------------+---------------------

* Ek aur baat: har jagah yield use karna better nahi hota. Agar tumhe ek 
               number, ek string ya ek final answer chahiye, toh generally 
               return simple aur sahi choice hai.

============================================================================

6. Chhota sa test — ab tum decide karo:

Question: Tumhe 1, 2, 3, 4, 5 numbers ek-ek karke generate karne hain, 
          bina poori list pehle banaye. Kaunsa option zyada suitable 
          hai?

Answer  : yield ko loop ke andar use karna.

Bilkul sahi!
------------
def numbers():    
for x in range(1, 6):        
yield x

- Har baar agla number produce hoga, bina poori list banaye.

Final shortcut
--------------
return = result do, function khatam.
yield  = value do, pause karo, phir zaroorat padne par resume 
         karo.