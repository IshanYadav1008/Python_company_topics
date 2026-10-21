1. Sabse pehle: pip kya hai ?
-----------------------------

* pip Python ka package installer hai.

* Matlab, jab tumhe apne Python project mein kisi doosre developer ki 
  banayi hui library ya package use karna hota hai, toh pip ki help 
  se use install kar sakte ho.

Ek example lete hain.
---------------------
* Maan lo tum ek Python program bana rahe ho jo kisi website se data 
  download karega. Iske liye tum requests naam ki library use karna 
  chahte ho.

* Lekin tumhare computer mein requests installed nahi hai.

* Toh tum pip se ise install kar sakte ho

Tumhara Python project
----------------------
       |
      pip
Package installer
       |
       |
requests package installed
Ab tum ise Python code mein use kar sakte ho.

===============================================================================

2. Package kya hota hai ?
-------------------------

* Abhi tumne Python ke modules aur packages padhe hain.

* Yaad karo, tumhara structure tha:

shopping_app/
├── products/
│   ├── laptops.py
│   └── phones.py
├── payments/
│   ├── upi.py
│   └── cards.py
└── orders/
    ├── new_order.py
    └── cancel_order.py

- Ye tumhare apne banaye hue modules aur packages hain.

- Lekin Python mein bahut saare ready-made packages bhi 
  available hain, jinhe doosre developers bana chuke hain.


Examples:
---------
Package	        Kaam
--------------------------------------------------
requests	    HTTP requests bhejna
numpy	        Numerical calculations karna
pandas	        Data ko organize aur analyze karna
flask	        Web applications banana
--------------------------------------------------

- In packages ka use karne se tumhe har cheez zero se nahi 
  banani padti.

===============================================================================

3. Install packages using pip ka kya matlab hai ?

Iska simple meaning hai:
------------------------
* pip command ka use karke kisi package ko apne Python 
  environment mein install karna.

- Jaise tum requests install karna chahte ho.

Terminal ya Command Prompt mein likho:
--------------------------------------
=> python -m pip install requests

Is command ko samjho:
---------------------
- python   → Python interpreter ko run karta hai.
- -m pip   → Python ko pip module run karne ke liye kehta hai.
- install  → package install karne ka action hai.
- requests → jis package ko install karna hai uska naam hai.


* Agar tumhare system mein command python3 se chalti hai, 
  toh ye bhi use kar sakte ho:

=> python3 -m pip install requests

* Installation ke baad tum apne Python code mein likh sakte 
  ho:

=> import requests

Dhyan do: install karna aur import karna alag kaam hain
-------------------------------------------------------
- pip install requests → package install karta hai.
- import requests      → Python code mein package ko use 
                          karne ke liye import karta hai.

===============================================================================

4. Packages install kyun karte hain ?
-------------------------------------

* Maan lo tumhe kisi website se information leni hai.

* Bina kisi external library ke tumhe HTTP communication 
  ke liye zyada code likhna pad sakta hai.

requests use karke tum aisa kar sakte ho:
-----------------------------------------
import requests
response = requests.get("https://example.com")
print(response.status_code)

- Yahan requests.get() website par HTTP GET request bhejta hai, 
  aur status_code response ka status batata hai.

- Humne requests khud nahi banaya. Humne package install kiya 
  aur uski functionality use kar li.

- Isliye packages install karte hain taaki existing functionality 
  ka use karke development ko aasan aur tez bana sakein.

===============================================================================

5. Package install kahan hota hai ?

Jab tum ye command chalate ho:
------------------------------
=> python -m pip install requests

- Toh package us Python environment mein install hota hai jise tumhari 
  command target kar rahi hai.

- Agar tum virtual environment use kar rahe ho, toh package us environment 
  mein install kiya ja sakta hai. Isse alag projects ki dependencies alag 
  rakhi ja sakti hain.

Example:
--------
my_project/
├── .venv/
└── main.py

- Agar .venv activate hai aur tum requests install karte ho, toh aam taur 
  par package isi virtual environment mein install hoga.

- Ek aur important baat: pip se install kiya hua package zaroori nahi ki 
                         tumhare project folder ke andar hi dikhe. Wo 
                         Python environment ki site-packages directory 
                         mein install ho sakta hai.

===============================================================================

6. Ab khud try karo:
-------------------

* Agar tumhe numpy package install karna hai, toh terminal mein kaunsi 
  command likhoge?

Ans) python -m pip install numpy

Bilkul sahi!
------------
- python -m pip install numpy terminal mein chalane wali command hai.

===============================================================================

Q) pip ka full form kya hai ?

ANS) pip ka commonly used full form hai: “Pip Installs Packages”.

- ise Python package installer ke roop mein use kiya jata hai.

Yaad rakhne ke liye:
--------------------
- Pip     → Python packages install karne ka tool.
- Install → Package ko Python environment mein available karna.
- Import  → Python code mein us package ko use karna.