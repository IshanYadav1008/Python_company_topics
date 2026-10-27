1. Python Logging Module kya hota hai ?
---------------------------------------

* Python ka logging module ek built-in module hai jo program ke run 
  hone ke dauran hone wali important activities, warnings aur errors 
  ka record rakhta hai.

- Simple language mein, Logging = program ke andar kya ho raha hai, 
  uska record rakhna.

* Maan lo tum company mein ek e-commerce application bana rahe ho. 
  User login karta hai, order place karta hai aur payment process 
  hoti hai. Agar payment fail ho jaye, toh tumhe pata hona chahiye 
  ki problem kab aayi aur kis wajah se aayi.

Logging isi kaam mein help karti hai.
-------------------------------------
Application runs
User login karta hai ya payment karta hai.
           |
           |
Logging records events
Info, warning aur error messages record hote hain.
           |
           |
Console or log file
Developer baad mein records dekhkar problem samajh sakta hai.

==============================================================================

2. Logging ki zaroorat kyun hoti hai ?
--------------------------------------

* Company ke projects mein logging ke 4 main uses hote hain.

- Debugging                 : code mein problem aane par uska reason dhoondhna.

- Monitoring                : application sahi chal rahi hai ya nahi, track 
                              karna.

- Error tracking            : kab aur kis operation mein error aaya, uska record 
                              rakhna.

- Audit and troubleshooting : important events ka record rakhna, jahan application 
                              ki requirements aur privacy rules ke hisaab se  
                              zaroori ho.

==============================================================================

3. print() aur logging mein kya difference hai ?
------------------------------------------------

* Maan lo tum code mein ye likhte ho:

=> print("Payment failed")

- Ye message dikha dega, lekin message ka level, standard timestamp 
  formatting aur exception details automatically manage nahi karega.

Logging mein:
-------------
import logging
logging.error("Payment failed")

- Ismein tum message ko error level de rahe ho. Logging ko configure 
  karke tum timestamp, log level aur message ko console ya file mein 
  record kar sakte ho.

print()	                         logging
-----------------------------------------------------------------------------
Simple output dikhata hai.	     Application events record karne ke liye 
                                 bana hai.
-----------------------------------------------------------------------------
Levels built-in nahi hote.	     DEBUG, INFO, WARNING, ERROR, CRITICAL levels 
                                 hote hain.
-----------------------------------------------------------------------------
File mein record karna manually  karna padta hai.	File output configure kar 
                                 sakte ho.
-----------------------------------------------------------------------------
Basic debugging mein useful.	 Real applications mein monitoring aur 
                                 troubleshooting ke liye useful.

==============================================================================

4. Logging ke 5 levels:
-----------------------

* In levels ko samajhna important hai, kyunki company code mein inka daily 
  use hota hai.

1. DEBUG
--------
* Detailed information, development aur debugging ke liye.

=> logging.debug("Calculating order total")


2. INFO
-------
* Normal, expected activities ka record.

=> logging.info("User logged in")


3. WARNING
----------
* Kuch unusual hua hai, lekin program abhi chal raha hai.

=> logging.warning("API response is slow")


4. ERROR
--------
* Koi operation fail ho gaya.

=> logging.error("Payment processing failed")


5. CRITICAL
-----------
* Bahut serious problem, jaise application ka major component 
  unavailable hona.

=> logging.critical("Application cannot start")

Inki severity ka order hai:
---------------------------
DEBUG < INFO < WARNING < ERROR < CRITICAL

==============================================================================

5. Python mein Logging kaise use hoti hai ?
-------------------------------------------

* Sabse pehle ek basic example run karo.

import logging

logging.basicConfig(level=logging.DEBUG)

logging.debug("This is a debug message")
logging.info("User logged in")
logging.warning("Storage space is low")
logging.error("Payment failed")
logging.critical("System failure")

* Is example mein basicConfig() logging ki basic configuration set 
  karta hai aur level=logging.DEBUG sabhi paanch levels ke messages 
  allow karta hai.

- Agar tum ise run karoge, toh console mein messages ke saath level 
  names dikhenge, jaise:

DEBUG:root:This is a debug message
INFO:root:User logged in
WARNING:root:Storage space is low
ERROR:root:Payment failed
CRITICAL:root:System failure

- root default logger ka naam hai.

* Dhyan do : basicConfig() kaam tab karta hai jab root logger ke liye 
             pehle se handlers configured na hon. Jupyter notebooks 
             ya bade projects mein pehle se configuration ho sakti 
             hai.

==============================================================================

6. Company mein log file kaise banate hain ?
--------------------------------------------

* Real project mein sirf console par messages dekhna enough nahi hota. 
  Tum messages ko file mein bhi save kar sakte ho.

CODE:
-----
import logging

logging.basicConfig(
    filename="app.log",
    level=logging.INFO,
    format="%(asctime)s - %(levelname)s - %(message)s"
)

logging.info("Application started")
logging.warning("API response is slow")
logging.error("Payment failed")

- Jab code run hoga, current working directory mein app.log file create 
  ho sakti hai, agar file pehle se nahi hai. Usmein messages kuch is 
  tarah honge:

2026-10-27 12:00:00,000 - INFO - Application started
2026-10-27 12:00:01,000 - WARNING - API response is slow
2026-10-27 12:00:02,000 - ERROR - Payment failed

- Ye timestamps sirf example hain; actual time tumhare system ke hisaab 
  se hoga.

format mein kya ho raha hai ?
-----------------------------
- %(asctime)s — date aur time.
- %(levelname)s — log ka level.
- %(message)s — actual message.  

* Aur level=logging.INFO ka matlab hai ki INFO aur usse higher levels 
  record honge. DEBUG messages record nahi honge.

==============================================================================

7. Errors ko logging ke saath kaise handle karte hain ?
-------------------------------------------------------

* Company projects mein exceptions ke saath logging ka use kaafi 
  important hai.

CODE:
-----
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(levelname)s - %(message)s"
)

def divide(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        logging.exception("Division failed")
        return None

result = divide(10, 0)

- Yahan logging.exception() error message ke saath exception traceback 
  bhi log karta hai. Ye method exception handler ke andar use karna 
  chahiye.

- Is example mein error log hone ke baad function None return karta hai. 
  Real project mein error ko handle karna ya dobara raise karna 
  application ke design par depend karta hai.

- Important : logs mein passwords, API keys, payment-card details ya 
              doosri sensitive information record mat karo.
            
==============================================================================

8. Company mein logging kahan use hoti hai ?
--------------------------------------------

Backend applications
--------------------
- Login, signup, requests, server errors aur API responses track karne 
  mein.

Database operations
-------------------
- Database connection failures, query errors aur slow operations ko 
  troubleshoot karne mein.

Data pipelines and automation
------------------------------
- Kaunsa task complete hua, kaunsa fail hua aur processing mein kitna 
  time laga, ye record karne mein.


* Bade projects mein logs ko centralized systems mein bheja ja sakta hai,
  jahan team errors search aur monitor karti hai. Har project mein alag 
  setup ho sakta hai.

==============================================================================

9. Ab tumhari practical practice
--------------------------------

* Neeche ek chhota task hai. Isse tum check kar sakte ho ki concept samajh 
  aaya ya nahi.

PRACTICE 01
-----------
Maan lo tumhari application mein payment fail ho gayi. Kaunsa logging level 
use karoge?

o/p: ERROR

Correct answer: ERROR
---------------------
Payment operation fail hua hai, isliye ERROR appropriate hai. Agar failure
application ko seriously unavailable kar de, situation ke hisaab se CRITICAL 
bhi appropriate ho sakta hai.