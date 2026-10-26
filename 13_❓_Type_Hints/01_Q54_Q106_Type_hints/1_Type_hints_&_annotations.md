# Type Hints & Type Annotations:
# ------------------------------

1. Sabse pehle samjho: Type Hint hota kya hai ?
-----------------------------------------------

* Python mein har value ka ek data type hota hai, jaise:

age   = 20          # int
name  = "Rahul"     # str
price = 99.5        # float

* Ab maan lo tum kisi function mein chahte ho ki age mein integer 
  aaye aur function integer hi return kare. Python mein tum iska 
  hint de sakte ho.

CODE:
-----
def square(number: int) -> int:
    return number * number

print(square(5))

Output:
-------
25

- Yahan int batata hai ki number se integer value ki expectation hai 
  aur -> int batata hai ki function integer return karne ke liye 
  intended hai.

- Simple definition: Type hints Python code mein batate hain ki kisi 
                     variable, parameter ya function ke return value 
                     se kis data type ki expectation hai.

===============================================================================

2. Type Annotation kya hota hai ?
---------------------------------

* Type annotation, type information likhne ka syntax hai.

Example:
--------
age:  int = 20
name: str = "Rahul"

Ismein:
-------
- age:  int — age ke liye integer type indicate kiya hai.
- name: str — name ke liye string type indicate kiya hai.

* Python mein type hint aur type annotation terms aksar ek hi concept 
  ke liye use hote hain. Technically, annotation type information 
  likhne ka tareeka hai, aur type hint us information ka intended 
  use batata hai.

===============================================================================

3. Type Hints ke important examples:
------------------------------------

Example 1: Variable Type Hint
-----------------------------
age:    int = 21
name:   str = "Aman"
marks: float = 85.5

- Variables ke expected data types batata hai.

-------------------------------------------------------------------------------

Example 2: Function Parameters
------------------------------
def greet(name: str):
    print("Hello", name)

greet("Aman")

- name: str batata hai ki function string expect karta hai.

-------------------------------------------------------------------------------

Example 3: Return Type
----------------------
def add(a: int, b: int) -> int:
    return a + b

- -> int function ke expected return type ko batata hai.

===============================================================================

4. Kya Python galat type dene par error dega ?
----------------------------------------------

* Ye bahut important exam point hai.

CODE:
-----
def square(number: int) -> int:
    return number * number

print(square("5"))

Output:
-------
555

- Python string "5" ko bhi accept kar leta hai aur use teen baar 
  repeat karta hai. Sirf int likhne se Python automatically type 
  enforce nahi karta.

Isliye yaad rakho:
------------------
- Type hints code ko readable banate hain.
- Errors pakadne mein static type checkers ki help karte hain.
- Type hints khud generally runtime par type restrictions enforce 
  nahi karte.

===============================================================================

5. Type Hints ke advantages
---------------------------

1. Readability     : Code samajhna easy hota hai.

2. Error detection : Type checkers possible type-related mistakes dhoondh 
                     sakte hain.

3. IDE support     : Editors better suggestions aur warnings de sakte hain.

4. Maintenance     : Bade projects ko samajhna aur update karna easy hota 
                     hai.

===============================================================================

Ab chhota sa test do:
---------------------

Q1. -> int ka kya matlab hai ?

Ans) Function integer return karne ke liye intended hai.

✓ Correct — -> int expected return type batata hai.

<-------------------------------------------------------->

Q2. Kya type hints automatically wrong types ko runtime 
    par reject karte hain ?

Ans) Nahi, generally nahi

✓ Correct — Type hints apne aap runtime enforcement nahi 
            karte.

<-------------------------------------------------------->

Q3. name: str = "Aman" mein str kya batata hai ?

Ans) Expected string type

✓ Correct — str string data type ko indicate karta hai.

* Bas ye line yaad kar lo: Type hints aur annotations expected types 
                           batate hain; ye code ko readable banate 
                           hain aur static type checking mein help 
                           karte hain, lekin Python mein automatically 
                           runtime enforcement nahi karte.

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

1. Pehle ye code dekho
----------------------

* Maan lo tumhari company ek application bana rahi hai jisme users 
  ki age store hoti hai.

age = 25


- Tum aur Python, dono jaante ho ki age mein 25 rakha hai, jo ek 
  integer hai.

- Ab ek doosra developer tumhara code padhta hai. Use abhi nahi 
  pata ki age mein integer aana chahiye, string ya kuch aur.

Tum is tarah likh sakte ho:
---------------------------
=> age: int = 25


* Yahan : int ek additional information hai jo tum code mein de 
          rahe ho.

Iska matlab hai:
----------------
* "Developer, is variable mein integer value rakhne ka intention hai."

- Dhyan do, tumne Python ko koi naya data type nahi diya. Tumne bas 
  code padhne wale ko information di hai.

===============================================================================

2. Lekin agar galat value daal di toh ?
---------------------------------------

age: int = "Rahul"
print(age)

Output:
-------
Rahul

* Python ne error nahi diya! Kyun?

* Kyunki : int likhne se Python khud value ko check karke rokta nahi hai.

- Ab socho, company ke project mein 20 developers kaam kar rahe hain. 
  Agar sabko har variable ka intended type samajhna hai, toh type hints 
  kaafi useful hain. Aur mypy jaise static type checker is tarah ki 
  galti ko pakadne mein help kar sakte hain.

===============================================================================

3. Ab function mein samjho — live project ke liye important:
------------------------------------------------------------

* Maan lo tum ek shopping application bana rahe ho. Tumhe user 
  ka total bill calculate karna hai.

def calculate_total(price: float, quantity: int) -> float:
    return price * quantity

-------------------------------------------------------------------------------

Isko parts mein samjho:
-----------------------

Part 1
------
=> price: float

- Price ke liye decimal number expected hai, jaise 99.50.


Part 2
------
=> quantity: int

- Kitne products kharide, woh whole number expected hai, jaise 3.


Part 3
------
=> -> float

- Function se decimal number return karne ka intention hai.

Ab function call karo:
----------------------
total = calculate_total(99.50, 3)
print(total)

Output:
-------
298.5

- Is example mein type hints se tumhe aur tumhare teammates 
  ko function ka intended use samajh aa jata hai, bina poora 
  function padhe.

===============================================================================

4. Toh Type Hints aur Type Annotations mein difference kya hai ?
----------------------------------------------------------------

* Practical Python development mein tum in terms ko aksar ek doosre 
  ki jagah use hote dekhoge.

age: int = 25

- Type annotation : : int likhne ka syntax.
- Type hint       :   int ki information ka intended use, yaani batana 
                      ki age ka expected type integer hai.

* Abhi internship ke liye dono terms ko alag-alag ratne ki zaroorat 
  nahi hai. Bas syntax aur uska purpose samjho.

===============================================================================

5. Ek real-project wali practice
--------------------------------
* Maan lo tumhe ek function banana hai jo user ka naam aur age lekar uski 
  information print kare.

* Pehle khud socho  : name ke liye kaunsa type hint aur age ke liye 
                      kaunsa type hint use karoge?

Incomplete code
---------------
def show_user(name: ___, age: ___) -> None:
    print(name, age)

Show Solution:
--------------
def show_user(name: str, age: int) -> None:
    print(name, age)

show_user("Rahul", 25)

- str naam ke liye, int age ke liye aur None ka matlab hai ki function 
  koi meaningful value return nahi karta.