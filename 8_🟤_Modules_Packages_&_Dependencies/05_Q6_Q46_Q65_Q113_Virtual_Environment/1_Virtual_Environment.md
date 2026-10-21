# 37. Virtual Environment:
# ------------------------

Step 1: Pichhla topic yaad karo — Dependencies
----------------------------------------------
* Pichhle topic mein humne padha tha ki dependency wo package ya 
  library hai jiski hamare project ko zaroorat hoti hai.

* Jaise tum apna shopping_app bana rahe ho aur usmein requests 
  package use karte ho.

=> import requests

* Lekin requests use karne se pehle use install karna pad sakta 
  hai:

=> python -m pip install requests

===========================================================================

# Ab ek problem samjho.

Step 2: Virtual environment ki zaroorat kyun padi ?
---------------------------------------------------

* Maan lo tumhare computer mein do Python projects hain:

MyProjects/
|
|--- shopping_app/
|    └── main.py
|
|--- weather_app/
     └── main.py

- shopping_app ko requests ka version 2 chahiye.

- weather_app ko kisi purane version ki zaroorat hai.

* Agar dono projects ek hi Python environment ke packages use 
  karte hain, toh package versions manage karna mushkil ho 
  sakta hai.

Solution: Dono projects ke liye alag virtual environments banao.

===========================================================================

Step 3: Virtual environment kya hota hai ?
------------------------------------------

* Virtual environment ek isolated Python environment hai, jisme 
  tum kisi project ke packages aur dependencies ko doosre
  projects se alag rakh sakte ho.

Is tarah samjho:
----------------

                            Tumhara computer
                            Python installed hai
                                    |
                                    |
            shopping_app                      weather_app
        Apna virtual environment        Apna virtual environment
        Apni dependencies               Apni dependencies

- Iska matlab hai ki ek project mein package install ya update karne 
  se doosre project ke environment par aam taur par asar nahi padta.

===========================================================================

Step 4: Virtual environment create kaise karein ?
-------------------------------------------------

* Maan lo tumhara project folder shopping_app hai.

- Terminal mein pehle project folder mein jao:
=> cd shopping_app

- Ab virtual environment create karo:
=> python -m venv .venv

Yahan har part ka meaning samjho:
---------------------------------
python  → Python interpreter run karta hai
-m      → Ek Python module ko run karta hai
venv    → Virtual environment banane wala module
.venv   → Environment ke folder ka naam

* Command chalne ke baad tumhare project mein .venv naam ka 
  folder banega.

shopping_app/
|
|--- .venv/
|
|--- products/
|--- payments/
|--- orders/
|
└── main.py

* .venv folder ka naam fixed nahi hai. Tum ise venv bhi naam de 
  sakte ho, lekin .venv common convention hai.

===========================================================================

Step 5: Virtual environment activate kaise karein ?
---------------------------------------------------

* Environment create karna aur activate karna alag steps hain.

macOS / Linux:
--------------
=> source .venv/bin/activate

* Activate hone ke baad terminal mein aam taur par (.venv) dikhai 
  dega:

=> (.venv) C:\MyProjects\shopping_app>

- Iska matlab hai ki virtual environment active hai.

===========================================================================

Step 6: Ab environment ke andar package install karo
----------------------------------------------------

* Ab jab .venv active hai, toh command chalao:

=> python -m pip install requests   // Isse requests package active virtual 
                                       environment mein install hoga.

* Ab main.py mein ise use kar sakte ho:

import requests
print(requests.__version__)

Yaad rakho:
-----------
- pip install → Package install karta hai.
- import      → Python code mein package use karne deta hai.
- venv        → Project ke packages ko alag environment mein rakhta hai.

===========================================================================

Step 7: Virtual environment deactivate kaise karein?
----------------------------------------------------

* Jab kaam khatam ho jaaye, terminal mein likho:

=> deactivate

- Bas! Virtual environment deactivate ho jayega aur terminal wapas 
  normal environment mein aa jayega.

- Important: Deactivate karne se virtual environment delete nahi 
  hota. Usmein installed packages bhi wahin rehte hain.

- Dobara kaam karna ho, toh use phir se activate kar lena.

===========================================================================

Step 8: Virtual environment important kyun hai ?
------------------------------------------------

+-----------------------------+-----------------------------------------------+
| Problem                     | Virtual environment ka fayda                  |
+-----------------------------+-----------------------------------------------+
| Alag projects ko alag       | Har project ki dependencies alag rakh sakte   |
| packages chahiye            | ho                                            |
+-----------------------------+-----------------------------------------------+
| Package versions ka conflict| Ek project ka environment doosre se isolate  |
| ho sakta hai                | kar sakte ho                                  |
+-----------------------------+-----------------------------------------------+
| Project doosre computer par | requirements.txt se dependencies install      |
| chalana hai                 | karna aasaan hota hai                         |
+-----------------------------+-----------------------------------------------+
| System Python ko clean      | Project ke packages ko system environment     |
| rakhna hai                  | se alag rakh sakte ho                         |
+-----------------------------+-----------------------------------------------+

===========================================================================

Step 9: Pichhle 3 topics ka connection
--------------------------------------

35. pip

- Packages install aur manage karne ka tool.
      |
      |
36. Dependencies

- Project ko jin packages ki zaroorat hai.
      |
      |
37. Virtual Environment

- Har project ki dependencies ko isolate rakhne 
  ka tareeka.

* Yaani sequence ye hai: pip se packages install karte hain, 
  dependencies un packages ki zaroorat batati hain, aur 
  virtual environment unhe project ke hisaab se alag rakhta 
  hai.

===========================================================================

Ab tumhari practice:
--------------------

* Maan lo tumne shopping_app mein ye command chalayi:

=> python -m venv .venv

- Environment create ho gaya, lekin tumne use activate nahi kiya.

Question: Kya sirf environment create karne se terminal automatically 
          us environment ko use karne lagta hai ?

Answer  : Nahi, aam taur par use activate karna padta hai.

* Bilkul sahi! Environment create karne ke baad use aam taur par 
  alag se activate karna padta hai.