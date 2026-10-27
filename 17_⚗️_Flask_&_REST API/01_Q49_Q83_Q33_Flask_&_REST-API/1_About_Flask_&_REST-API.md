# 1. Flask kya hai ?
# ------------------

* Flask ek Python framework hai jiska use website aur web applications 
  banane ke liye hota hai.

Pehle ek example samjho.
------------------------
- Maan lo tum ek company mein kaam karte ho aur company ko ek website 
  banani hai, jahan employees apni details dekh sakein.

- Website banane ke liye tum Python mein code likhna chahte ho. Lekin 
  Python ko browser ke saath connect karna, URL handle karna aur 
  browser ko response dena bhi zaroori hai.

- Yahan Flask help karta hai.

---------------------------------------------------------------------------------

Browser
-------
User website open karta hai
    |
    |
Flask + Python
--------------
Request ko handle karta hai
    |
    |
Website ka response
-------------------
Page browser mein dikhai deta hai

---------------------------------------------------------------------------------

Real-life example
-----------------
* Maan lo user browser mein ye URL open karta hai:

=> www.company.com/about

- Flask ko request milti hai aur woh About Us page return kar deta 
  hai.

- Yaad rakhna : Python programming language hai, aur Flask Python ka 
                framework hai jo web application banana aur uski 
                requests handle karna aasaan banata hai.

=================================================================================

# 2. API kya hoti hai ?
# ---------------------

* REST API samajhne se pehle API samjho.

* API ek madhyam hai jiske through do software ek doosre se baat karte 
  hain.

Real-life example: restaurant:
------------------------------
- Tum customer ho.
- Kitchen tumhare liye food prepare karti hai.
- Waiter tumhara order kitchen tak pahunchata hai aur food tum tak laata 
  hai.

* Is example mein waiter ko API ki tarah samajh sakte ho.

---------------------------------------------------------------------------------

Software mein bhi aisa hi hota hai:
-----------------------------------

- Ek application request bhejti hai.
- Doosri application us request ko process karti hai.
- Phir response bhejti hai.

Example : tumhari company ki mobile app ko employee ki salary details 
          chahiye. App API ko request bhejti hai aur API se data
          milta hai.

=================================================================================

# 3. REST API kya hai ?
# ---------------------

* REST API ek aisi API hai jo REST ke rules aur principles ko use karke 
  software ke beech communication karne ke liye design ki jaati hai.

* REST ka full form hai Representational State Transfer.

Isko simple example se samjho.
------------------------------
- Maan lo company ke paas employees ka data hai. Tumhe employee ki details 
  chahiye, to tum request bhejte ho:

=> GET /employees

Server response deta hai:
-------------------------
[
  {
    "id": 1,
    "name": "Rahul"
  },
  {
    "id": 2,
    "name": "Priya"
  }
]

- Ye data JSON format mein hai, jise applications aasani se read kar sakti 
  hain.

---------------------------------------------------------------------------------

REST API mein HTTP methods
--------------------------

Method	  Simple meaning	        Example
----------------------------------------------------------------------------
GET	      Data dekhna	            Employee list dekhna
----------------------------------------------------------------------------
POST	  Naya data add karna	    Naya employee banana
----------------------------------------------------------------------------
PUT	      Poora data update karna	Employee ki saari details replace karna
----------------------------------------------------------------------------
PATCH	  Kuch data update karna	Sirf employee ka naam badalna
----------------------------------------------------------------------------
DELETE	  Data delete karna      	Employee record remove karna
----------------------------------------------------------------------------

- In methods ko tum actions ki tarah yaad rakh sakte ho.

=================================================================================

4. REST API aur RESTful API mein kya difference hai ?
-----------------------------------------------------

* Ye sabse important point hai.

* REST API aur RESTful API ka meaning bahut similar hai. RESTful API 
  aam taur par us API ko kehte hain jo REST ke principles ko properly 
  follow karti hai.

# Example dekho:

Example A — Less RESTful design
-------------------------------

=> GET /getEmployees
=> GET /deleteEmployee/5

- Yahan URL mein action likha gaya hai. Aur GET request se data delete 
  karna sahi design nahi hai.

Example B — RESTful design
--------------------------

=> GET /employees
=> GET /employees/5
=> DELETE /employees/5

- Yahan URL employee resource ko represent karta hai aur HTTP method 
  batata hai ki kya karna hai.

---------------------------------------------------------------------------------

RESTful API mein aam taur par:
------------------------------

- URLs resources ko represent karte hain, jaise /employees.

- HTTP methods ka sahi use hota hai.

- Requests stateless hoti hain, yani har request ko process karne ke 
  liye zaroori information us request mein available honi chahiye.

- Appropriate HTTP status codes use hote hain, jaise 200, 201, 404.

* Dhyan rahe, REST API aur RESTful API do alag technologies nahi hain. 
  Dono ke liye Flask use kiya ja sakta hai.

=================================================================================

5. Teeno ka difference ek saath:
--------------------------------

Term	     Kya hai?	                   Kya kaam hai ?
------------------------------------------------------------------------------
Flask	     Python framework	           Website ya API banana
------------------------------------------------------------------------------
REST API     API design karne ka tareeka   Applications ke beech data exchange 
                                           karna
------------------------------------------------------------------------------     
RESTful-API	 REST principles ko follow     Consistent aur standard tareeke se 
             karne wali API.               resources access karna
------------------------------------------------------------------------------             

* Ek company project mein tum teeno ko is tarah use kar sakte ho:

- Flask se backend application banaoge.
- REST API endpoints banaoge.
- Un endpoints ko REST principles ke according design karoge, 
  taaki API RESTful ho.