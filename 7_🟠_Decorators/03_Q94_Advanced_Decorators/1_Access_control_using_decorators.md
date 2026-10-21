1. Access control kya hota hai ?
--------------------------------

* Access control ka matlab hai: kisi function ko execute karne 
  ki permission sirf authorized user ko dena.

Example: Ek website par do tarah ke users hain:
-----------------------------------------------
- admin — jise secret data dekhne ki permission hai.
- guest — jise secret data dekhne ki permission nahi hai.

* Hum decorator ki help se check karenge ki user admin hai ya 
  nahi.

==================================================================================

2. Program dekho:
-----------------
def access_control(func):

    def wrapper(role):
        if role == "admin":
            return func(role)
        else:
            print("Access Denied!")

    return wrapper

@access_control
def show_secret(role):
    print("Secret data is: 12345")

show_secret("admin")
show_secret("guest")

Output:
-------
Secret data is: 12345
Access Denied!

==================================================================================

3. Ab har line ka matlab samjho:
--------------------------------

Step 1 — Decorator define hua
-----------------------------
=> def access_control(func):

- access_control ek decorator hai. Ismein original function 
  argument ke roop mein aayega.

----------------------------------------------------------------------------------

Step 2 — Wrapper define hua
---------------------------
=> def wrapper(role):

- Wrapper function ko call karte waqt user ka role milega, 
  jaise "admin" ya "guest".

----------------------------------------------------------------------------------

Step 3 — Permission check hogi
------------------------------
=> if role == "admin":

- Agar role "admin" hai, toh condition True hogi.

=> return func(role)

* Original function execute hoga. Yahan func, show_secret ke original 
  function ko refer karta hai.

Lekin agar role admin nahi hai:
--------------------------------
else:    
print("Access Denied!")

- Toh original function execute nahi hoga. Sirf access-denied message 
  print hoga.

----------------------------------------------------------------------------------

Step 4 — Wrapper return hoga
----------------------------
=> return wrapper

Decorator wrapper ko return karta hai. Isliye:
----------------------------------------------
@access_control
def show_secret(role):
    print("Secret data is: 12345")

Conceptually iske barabar hai:
------------------------------
def show_secret(role):
    print("Secret data is: 12345")

show_secret = access_control(show_secret)

- Ab show_secret naam wrapper ko refer karta hai.

==================================================================================

4. Execution flow samjho
------------------------

Jab ye line chalegi:
--------------------
=> show_secret("admin")

* Toh actually wrapper("admin") execute hoga.

1. role = "admin" hoga.
2. if role == "admin" check hoga.
3. Condition true hogi.
4. func(role) original show_secret ko call karega.
5. Secret data print hoga.

----------------------------------------------------------------------------------

Lekin jab ye chalega:
---------------------
=> show_secret("guest")

1. role = "guest" hoga.
2. Admin wali condition false hogi.
3. else execute hoga.
4. Access Denied! print hoga.
5. Original function call nahi hoga.

==================================================================================

5. Ab tumhari practice:
-----------------------

Question: Agar hum show_secret("guest") call karte hain, toh 
          original show_secret function execute kyon nahi 
          hota ?

Answer :  Kyunki if condition false hone par func(role) call 
          hi nahi hota.

Bilkul sahi! 
------------
Guest ke liye condition false hai, isliye original function ko 
call karne wali line execute hi nahi hoti.

Ek important baat: Ye learning example hai. Real applications mein access 
                   control ko sirf user ke diye hue "admin" jaise string 
                   par bharosa karke implement nahi karna chahiye; role ko 
                   trusted authentication/authorization system se verify 
                   karna zaroori hai.