# Python Built-in Functions:
# --------------------------

1. Built-in Function hota kya hai ?
-----------------------------------
* Maan lo tumhe ek list mein 5 users hain ya nahi, ye count 
  karna hai.

* Tum khud code likh sakte ho jo list ke har item ko count 
  kare. Lekin Python mein pehle se hi ek function hai jo 
  ye kaam karta hai:

users = ["Aman", "Rahul", "Priya"]
print(len(users)) 

Output: 3

- Yahan len() Python ka built-in function hai. Ye list mein kitne 
  items hain, bata deta hai.

- Simple way mein: Built-in functions woh ready-made functions hain 
                   jo Python mein pehle se available hote hain. Tum 
                   inhe bina khud define kiye use kar sakte ho.

                   Jaise print(), len(), sum(), type()

=================================================================================

2. Sabse useful built-in functions:
-----------------------------------

* Inhe ek-ek karke samjho. Ye functions tumhe code likhte waqt baar-baar 
  milenge.

1. print() — output dikhana:
----------------------------

=> print("Hello")

Output: Hello

. Debugging aur console par information dikhane ke liye.

---------------------------------------------------------------------------------

2. len() — kitne items ya characters hain:
------------------------------------------

name = "Rahul"
print(len(name))  # 5

- List, string, tuple aur dictionary ke size ko check karne mein 
  useful.

---------------------------------------------------------------------------------

3. type() — value ka data type:
-------------------------------

price = 99.5
print(type(price))  # <class 'float'>

- Jab API se data aaye aur tumhe samajhna ho ki value kis type ki 
  hai, tab helpful.

---------------------------------------------------------------------------------

4. int(), float(), str() — type conversion:
-------------------------------------------

CODE:
-----
age = int("25")
price = float("99.5")
user_id = str(101)

print(age)  # 25

- Jab input string mein mile aur tumhe number chahiye ho, tab use karo. 
  Har conversion possible nahi hota; int("hello") error dega.

---------------------------------------------------------------------------------

5. sum() — numbers ka total:
----------------------------

prices = [100, 200, 300]
print(sum(prices))  # 600

- Shopping cart ka total ya numbers ka sum calculate karne ke liye.

---------------------------------------------------------------------------------

6. max() aur min() — sabse bada aur chhota
------------------------------------------

CODE:
-----
marks = [65, 90, 72]

print(max(marks))  # 90
print(min(marks))  # 65

- Highest price, lowest score ya min/max value nikalne ke liye.

---------------------------------------------------------------------------------

7. sorted() — data ko sort karna:
---------------------------------

prices = [300, 100, 200]
print(sorted(prices))  # [100, 200, 300]

- sorted() original list ko change kiye bina ek nayi sorted list 
  return karta hai.

---------------------------------------------------------------------------------

8. range() — numbers ki sequence:
---------------------------------
for i in range(3):
    print(i)

Output: 0, 1, 2

* Loops mein baar-baar kaam karne ke liye useful.

=================================================================================

3. Ab kuch functions jo professional code mein kaafi useful hain:
-----------------------------------------------------------------

* Ye thode aur important hain, khaaskar lists aur data processing 
  ke liye.

enumerate() — item ke saath index bhi
-------------------------------------
users = ["Aman", "Priya", "Rahul"]

for index, user in enumerate(users):
    print(index, user)

- Output mein har user ke saath uska index milega. Agar counting 
  1 se chahiye, toh enumerate(users, start=1) likho.

---------------------------------------------------------------------------------

zip() — do lists ko pair karna:
-------------------------------
names = ["Aman", "Priya"]
scores = [80, 95]

for name, score in zip(names, scores):
    print(name, score)

Output:
-------
Aman 80
Priya 95

- Jab do lists ki corresponding values ko saath process karna ho, 
  tab useful.

---------------------------------------------------------------------------------

isinstance() — type check karna:
--------------------------------
age = 25
print(isinstance(age, int))  # True

- Jab function ko verify karna ho ki input expected type ka hai 
  ya nahi.

---------------------------------------------------------------------------------

any() aur all() — conditions check karna:
-----------------------------------------
scores = [40, 75, 90]

print(any(score >= 80 for score in scores))  # True
print(all(score >= 35 for score in scores))  # True

. any() — kam se kam ek condition true hai?
. all() — kya saari conditions true hain?

=================================================================================

4. Live project mein ye kaise kaam aate hain ?
----------------------------------------------

* Maan lo tum ek API se products ki list lekar unki prices 
  process kar rahe ho.

CODE:
-----
products = [
    {"name": "Mouse", "price": 500},
    {"name": "Keyboard", "price": 1200},
    {"name": "Monitor", "price": 8000},
]

prices = [product["price"] for product in products]

print("Total:", sum(prices))
print("Most expensive:", max(prices))
print("Sorted prices:", sorted(prices))

Output:
-------
Total: 9700
Most expensive: 8000
Sorted prices: [500, 1200, 8000]

- Is ek example mein tumne sum(), max() aur sorted() ka real-world use 
  dekha. Aise functions data processing, APIs aur business logic mein 
  kaafi kaam aate hain.

- Ek practical baat: API se aaye data ko process karne se pehle uska 
                     structure aur types samajhna zaroori hai. Built-in 
                     functions data processing mein help karte hain, 
                     lekin missing keys ya invalid values ko automatically 
                     handle nahi karte.

=================================================================================

5. Ab khud try karo
-------------------

* Tumhare paas ye list hai:

prices = [250, 100, 450, 200]

Question: Sabse mehenga product ka price nikalne ke liye kaunsa 
          function use karoge?


Answer) max(prices)

. Bilkul sahi! max(prices) 450 return karega.

=================================================================================

6. Ab kis order mein practice karna hai?
----------------------------------------

* Meri recommendation hai ki ek saath saare built-in functions yaad 
  mat karo. Is sequence mein practice karo:

Basics                    : print(), len(), type(), int(), float(), str()
Collections               : sum(), min(), max(), sorted()
Loops aur data processing : range(), enumerate(), zip()
Conditions aur validation : any(), all(), isinstance()

Ek aur baat: Python mein built-in functions ki list kaafi badi hai. Abhi 
             tumhe sab kuch master karne ki zaroorat nahi. Pehle in 
             functions ko code mein khud use karna seekho, phir functools 
             par aana.