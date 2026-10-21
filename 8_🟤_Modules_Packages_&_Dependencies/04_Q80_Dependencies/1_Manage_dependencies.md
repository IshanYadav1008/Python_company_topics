1. Dependencies kya hoti hain ?
-------------------------------

* Dependency ka matlab hai aisi library ya package jis par tumhara 
  Python program apna kaam karne ke liye depend karta hai.

* Maan lo tum ek shopping_app bana rahe ho. Tum chahte ho ki is app 
  mein payment process ho aur customer ko email bhi send ho.

* Tum apne code mein doosre developers ke banaye hue packages use karte 
  ho. Ab tumhara project un packages par depend karta hai.

Example:
--------
shopping_app/
├── main.py
└── requirements.txt

Maan lo main.py mein tum ye code likhte ho:
-------------------------------------------
import requests

response = requests.get("https://example.com")
print(response.status_code)

- Yahan requests tumhare program ki dependency hai, kyunki tumhara 
  code ise use kar raha hai.

=============================================================================

2. Dependencies ke examples:
----------------------------

* Ye copy karne layak Markdown table hai:

Package	    Kaam
-----------------------------------------------
requests	HTTP requests bhejna
numpy	    Numerical calculations karna
pandas	    Data ko organize aur analyze karna
flask	    Web applications banana
Django	    Web applications develop karna
-----------------------------------------------

- Agar tumhara project in packages ko use karta hai, 
  toh ye us project ki dependencies ho sakti hain.

=============================================================================

3. Dependencies manage karna kya hota hai ?
-------------------------------------------

* Manage dependencies ka matlab hai apne project ko jin packages ki zaroorat 
  hai, unhe install karna, unke versions control karna aur unki list maintain 
  karna.

* Maan lo tumne apne computer par shopping_app banaya hai aur usmein requests 
  install kiya hai.

* Ab tum apna project kisi doosre computer par le jaate ho. Wahan requests 
  installed nahi hai.

Toh program error de sakta hai:
-------------------------------
=> ModuleNotFoundError: No module named 'requests'

- Ab har package ka naam manually yaad rakhne ke bajaye, tum dependencies 
  ki list maintain kar sakte ho.

- Yahi dependency management ka ek important purpose hai.

=============================================================================

4. requirements.txt kya hoti hai ?
----------------------------------

* Python projects mein dependencies ki list rakhne ke liye commonly 
  requirements.txt file use hoti hai.

Example:
--------
requests==2.32.3
numpy==2.1.0

* Is file mein package names aur zaroorat ke hisaab se unke versions 
  likhe ja sakte hain.

- requests aur numpy package names hain.
- == ka matlab hai specified version ko pin karna.
- 2.32.3 aur 2.1.0 package versions hain.

* Ye sirf example versions hain; har project ke liye ye versions 
  suitable hon, zaroori nahi.

=============================================================================

5. Dependencies ko practically manage kaise karte hain?
-------------------------------------------------------

Step 1: Package install karo
----------------------------
Terminal mein:

=> python -m pip install requests

<------------------------------------------------------------->

Step 2: Installed packages ki list banao
----------------------------------------
=> python -m pip freeze > requirements.txt

- Ye current Python environment mein installed packages aur unke 
  versions ko requirements.txt mein likhta hai. Isliye project 
  ke liye virtual environment use karna behtar hai.

<------------------------------------------------------------->

Step 3: Doosre environment mein dependencies install karo
---------------------------------------------------------

- Jab project doosre computer ya environment mein set up karna 
  ho:

=> python -m pip install -r requirements.txt

* Ye file mein listed packages install karne ki koshish karta hai.

=============================================================================

6. Dependency management kyun important hai ?
---------------------------------------------

+----------------------------------+----------------------------------------
| Problem                          | Dependency management ka fayda        
+---------+-----------------------------------------------------------------
| Required package missing hai     | Required packages install kar sakte ho
+----------------------------------+----------------------------------------
| Doosre computer par project      | Dependencies ki list se setup aasaan 
  chalana hai                      | hota hai                  
+-------+-------------------------------------------------------------------
| Package version badal gaya       | Versions pin karke unexpected changes 
                                   | ka risk kam hota hai  
+----------------------------------+----------------------------------------
| Multiple projects hain           | Alag virtual environments se packages 
                                   | isolate kar sakte ho.
+----------+----------------------------------------------------------------

=============================================================================

7. Ab dono concepts ka difference yaad rakho:
---------------------------------------------

Term	                Meaning
-------------------------------------------------------------------------
Dependency	            Wo package ya library jiski tumhare project ko 
                        zaroorat hai
-------------------------------------------------------------------------
Dependency management   Un packages ko install, track aur versions ke 
                        saath maintain karna
-------------------------------------------------------------------------
pip	                    Python packages install aur manage karne ka tool
-------------------------------------------------------------------------
requirements.txt	    Dependencies aur unke version requirements list 
                        karne wali file
-------------------------------------------------------------------------
Virtual environment   	Ek project ke Python packages ko doosre projects 
                        se alag rakhne ka environment
-------------------------------------------------------------------------

* Short mein: Dependency wo package hai jiski tumhare project ko 
              zaroorat hai, aur dependency management us zaroorat 
              ko properly handle karne ka process hai.

=============================================================================

Ab ek chhota sa practice question:
----------------------------------
* Maan lo tumhare main.py mein import requests likha hai, lekin 
  tumhare Python environment mein requests installed nahi hai.

Tumhe kya karna chahiye ??

ANS)
----
=> python -m pip install  // requests chala kar package install karna.

python -m pip install requests — isse requests package install hoga.