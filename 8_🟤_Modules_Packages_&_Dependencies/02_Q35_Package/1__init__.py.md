1. Sabse pehle: Module kya hota hai ?
-------------------------------------

* Maan le tu ek online shopping app bana raha hai. Usmein products, 
  payments aur orders ka code hai.

* Agar saara code ek hi file mein likhega, toh file bahut badi aur 
  sambhalna mushkil ho jayegi.

Isliye tu code ko alag-alag files mein rakhega:
-----------------------------------------------
- products.py  : Products se related code

- payments.py  : Payment se related code

- orders.py    : Orders se related code

* Python mein, ek .py file ko module kehte hain.

-------------------------------------------------------------------------------

Example:
--------
# products.py

CODE:
-----
def get_products():
    return ["Laptop", "Phone"]

* Ab agar kisi doosri file mein ye function chahiye, toh import kar 
  sakta hai:

CODE:
-----
from products import get_products
print(get_products())

Output:
-------
['Laptop', 'Phone']

- Bas bhai, module ka matlab filhaal itna hi samajh: ek Python file 
  jismein code rakha ho, jise doosri files mein bhi use kar sakein.

===============================================================================
 
2. Ab Package kya hota hai ?
----------------------------

* Maan le teri shopping app mein 50 Python files ho gayi hain. Sabko 
  ek hi jagah rakh dega toh dhoondhne mein dikkat hogi.

- Isliye tu related files ko alag-alag folders mein rakh dega.

shopping_app/
-------------
products/
- laptops.py, phones.py

payments/
- upi.py, cards.py

orders/
- new_order.py, cancel_order.py

* Ab products ka code ek folder mein, payments ka doosre mein aur 
  orders ka teesre mein.

* Python mein aise related modules ko ek saath rakhne wale folder 
  ko aam taur par package kehte hain.

Ek simple example:
------------------
- Module  = ek file.
- Package = related files ko rakhne ka folder.

* Python 3 mein kuch packages __init__.py ke bina bhi kaam kar sakte 
  hain. Isliye har folder mein ye file daalna compulsory nahi hai.

===============================================================================

3. Ab aate hain __init__.py par
-------------------------------

* Bhai, ab tak humne do cheezein samajh li:

- Module yaani Python file.
- Package yaani related files ko rakhne wala folder.

-------------------------------------------------------------------------------

Ab maan le tera folder aisa hai:
--------------------------------

shop/
-----
- __init__.py

- products.py

products.py mein:
-----------------
def get_products():
    return ["Laptop", "Phone"]

* Ab __init__.py mein tu likhta hai:

=> from .products import get_products

- Iska matlab hai: shop folder ko import karne par get_products 
                   ko bhi uske naam se available kara do.

-------------------------------------------------------------------------------

* Ab doosri file mein tu likh sakta hai:

from shop import get_products
print(get_products())

Output:
-------
['Laptop', 'Phone']

-------------------------------------------------------------------------------

* Lekin ye file banane ki zarurat kyun padi ?

Ab sabse important baat sun: 
----------------------------
- __init__.py ke bina bhi tu ye likh sakta tha:

=> from shop.products import get_products

-------------------------------------------------------------------------------

* Aur ye bhi kaam kar sakta hai.

- Toh __init__.py ka asli fayda ye hai ki tu package ko import karte 
  waqt kuch khaas cheezein pehle se taiyaar kar sakta hai aur decide 
  kar sakta hai ki package se kaunse functions aasani se use kiye ja 
  sakein.

- Sirf import ka naam chhota karna iska ek fayda hai, koi majboori 
  nahi.

- Ek aur baat: jab Python regular package ko pehli baar import karta 
  hai, toh uska __init__.py code chalta hai. Ismein zarurat ke kaam 
  rakhe ja sakte hain, lekin bina wajah zyada code rakhna achha nahi 
  hota.

===============================================================================

4. Ek chhota sa difference yaad rakh:
-------------------------------------

Cheez	            Simple matlab
---------------------------------------------------------------
products.py	        Code rakhne wali file
---------------------------------------------------------------
shop/	            Related files rakhne wala folder
---------------------------------------------------------------
shop/__init__.py	Package import hone par chalne wali file, 
                    jismein package ke liye setup ya convenient 
                    imports rakhe ja sakte hain.
---------------------------------------------------------------

* Meri practical advice: abhi har folder mein __init__.py mat banata 
  phir. Pehle modules aur imports achhe se samajh. Jab package ko 
  ek jagah se functions dene hon ya import ke waqt setup karna ho, 
  tab iska use karna.

===============================================================================

Ab tera ek chhota sa test:
--------------------------

* Maan le tere paas ye structure hai:

project/
├── shop/
│   ├── __init__.py
│   └── products.py
└── main.py

- products.py mein get_products() function hai.

- Agar __init__.py mein kuch bhi nahi likha, toh 
  kaunsa import us function ko seedha la sakta 
  hai, project root se run karte waqt ?

-------------------------------------------------------------------------------

ANSWER
------
=> from shop.products import get_products

Bilkul sahi, bhai!
------------------
products.py ka naam likhkar function import kar sakte 
hain. __init__.py mein function ko alag se expose 
karna zaroori nahi.

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

1. Tumhara folder structure:
----------------------------
shopping_app/
│
├── products/
│   ├── laptops.py
│   └── phones.py
│
├── payments/
│   ├── upi.py
│   └── cards.py
│
└── orders/
    ├── new_order.py
    └── cancel_order.py

===============================================================================

2. In sabko kya kahenge ?
-------------------------

# shopping_app/
---------------
* Top-level folder / Project folder
- Ye tumhare poore application ka main folder hai, jiske andar 
  baaki packages hain. Ise project root directory bhi keh sakte 
  hain.

# products/, payments/, orders/
-------------------------------
* Packages
- Ye related Python modules ko organize karne wale folders hain. 
  Traditional Python packages mein inke andar __init__.py file 
  hoti hai.

# laptops.py, phones.py, upi.py etc.
------------------------------------
* Modules
- Har .py file ek Python module hoti hai.

===============================================================================

3. Ek important baat: __init__.py:
----------------------------------

* Agar tumhara structure aisa hai:

shopping_app/
├── products/
│   ├── __init__.py
│   ├── laptops.py
│   └── phones.py
├── payments/
│   ├── __init__.py
│   ├── upi.py
│   └── cards.py
└── orders/
    ├── __init__.py
    ├── new_order.py
    └── cancel_order.py

- Toh products, payments aur orders regular packages hain.

- Lekin dhyan do: Python 3 mein __init__.py ke bina bhi folders 
  namespace packages ke roop mein kaam kar sakte hain, kuch 
  conditions ke saath.

- Aur shopping_app/ ko bhi Python package banana ho, toh uske 
  andar bhi __init__.py rakh sakte ho.

-------------------------------------------------------------------------------

Yaad rakhne ka shortcut
-----------------------
- Project root directory → shopping_app/
- Package                → products/
- Module                 → laptops.py
- __init__.py            → Package initialization se related file

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Question:1 
----------
Bas ek chhota sa sawaal: agar shopping_app/ ke andar products/ hai aur 
products/ ke andar laptops.py hai, toh laptops.py ko import karte waqt 
uska full dotted module name kya hoga ?

Answer:
-------
=> from shopping_app.products import laptops

-------------------------------------------------------------------------------

Chalo, isko break karke samajhte hain:
--------------------------------------
- shopping_app → Top-level package (agar ismein __init__.py hai)
- products     → Subpackage
- laptops      → Module (laptops.py)

Ek important baat : shopping_app/ ko project root directory bhi keh sakte 
                    hain. Agar ismein __init__.py nahi hai, toh Python 3 
                    mein ye namespace package bhi ho sakta hai.

===============================================================================

Question:2 
----------
Agar tumhe payments package ke andar se upi.py module import karna ho, 
toh kya likhoge?

Answer:
-------
=> from shopping_app.payments import upi

-------------------------------------------------------------------------------

* Tumne import ka concept achhe se samajh liya hai!

Isko break karke dekho:
-----------------------
- shopping_app → Project root / Top-level package
- payments     → Subpackage
- upi          → Module (upi.py)

===============================================================================

Question:3
----------
* Maan lo tumhara folder structure ye hai:

shopping_app/
└── products/
    ├── __init__.py
    └── laptops.py

Step 1: laptops.py ke andar function hai:
-----------------------------------------
def show_laptops():
    print("Available laptops")

Step 2: Ab maan lo tum shopping_app folder ke bahar 
        ek main.py file bana rahe ho:

project/
├── main.py
└── shopping_app/
    └── products/
        ├── __init__.py
        └── laptops.py

Tumhe main.py mein show_laptops() function import karna hai.
Toh kya likhoge ?

-------------------------------------------------------------------------------

Answer:
-------
from shopping_app.products.laptops import show_laptops
show_laptops()

Output:
-------
Available laptops


Samjho difference:
------------------
- from shopping_app.products import laptops 
  → poora module import hota hai.

- from shopping_app.products.laptops import show_laptops 
  → seedha function import hota hai.

Dhyan rahe: main.py ko us parent directory se run karna 
            hoga jahan shopping_app/ folder hai.

-------------------------------------------------------------------------------

1. Sirf import karna
--------------------
=> from shopping_app.products.laptops import show_laptops

* Iska matlab hai: laptops.py file se show_laptops function ko apni 
                   current file mein le aao, taaki hum use kar sakein.

* Abhi function execute nahi hoga. Sirf import hoga.

2. Function ko call karna
-------------------------
=> show_laptops()

* Iska matlab hai: ab show_laptops function ko execute karo.

Output:
-------
Available laptops

-------------------------------------------------------------------------------

3. Dono ko saath likhne par:
----------------------------
=> from shopping_app.products.laptops import show_laptops
=> show_laptops()

- Pehli line  → function import karti hai.
- Doosri line → function ko chalati hai.

* Ek real-life example samjho: 
------------------------------
import karna        = TV ka remote haath mein lena; 
function call karna = remote ka button dabana. 😄

- Remote haath mein lene se TV apne aap on nahi hota, hai na ? 

Yaad rakho: Agar tumhara kaam sirf function import karna hai, 
            toh pehli line hi kaafi hai. show_laptops() likhna 
            zaroori nahi hai, jab tak tum function ko execute 
            nahi karna chahte.