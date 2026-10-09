1. Sabse pehle: Public ka matlab kya hai?

* Public attribute ya method woh hai jise normally class ke bahar 
  se object ke through access kiya ja sakta hai.

Simple example:
---------------
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def show_details(self):
        print(self.name, self.age)

Ab object banate hain:
----------------------
s = Student("Rahul", 20)

Yahan do public attributes hain:
--------------------------------
- name
- age

Aur ek public method hai:
-------------------------
- show_details()

Hum inhe class ke bahar se use kar sakte hain:
----------------------------------------------
print(s.name)
print(s.age)
s.show_details()

Output:
-------
Rahul
20
Rahul 20

* Yahan important baat: s.name ka matlab object ke name attribute 
  ko access karna hai, jabki s.show_details() ka matlab object ke 
  method ko call karna hai.

============================================================================

2. Public Attributes kya hote hain?

* Pehle attribute ka meaning samjho.

  Attribute = object ke andar stored information ya data.

* Jaise ek student ke paas name, age aur marks ho sakte hain.

CODE:
-----
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age
s = Student("Rahul", 20)

Is object ke andar:
------------------
Object --> s
name   --> "Rahul"
age    --> 20

----------------------------------------------------------------------------

* Ab kyunki name aur age public attributes hain, hum unhe directly 
  access kar sakte hain:

=> print(s.name)  # Rahul
=> print(s.age)   # 20

Aur unki values change bhi kar sakte hain:
------------------------------------------
=> s.age = 21
=> print(s.age)  # 21

----------------------------------------------------------------------------

Dhyan do: 
---------

* s.age = 21 ka matlab object ke age attribute mein nayi value assign 
  karna hai.

* Is simple example mein koi validation nahi hai, isliye ye bhi possible 
  hai:

=> s.age = -100  // Python ise automatically reject nahi karega.

* Yahi public attributes ki ek important baat hai: unhe class ke bahar 
  se access aur modify kiya ja sakta hai.

============================================================================

3. Public Methods kya hote hain?

Ab method samjho.
-----------------
Method = class ke andar define kiya gaya function, jo object ke through 
         call kiya ja sakta hai.

Example:
--------
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def show_details(self):
        print("Name:", self.name)
        print("Age:", self.age)

Object banao:
-------------
s = Student("Rahul", 20)

Ab method ko call karo:
-----------------------
s.show_details()

Output:
-------
Name: Rahul
Age: 20

* Yahan show_details() ek public method hai, kyunki jise normally class 
  ke bahar se object ke through access kiya ja sakta hai.

----------------------------------------------------------------------------

Public Attribute
----------------
s.name            --> Object ki information ko access karta hai.

Public Method
-------------
s.show_details()  --> Object ka defined operation perform karta hai.

============================================================================

4. Attribute aur Method mein exact difference:

Attribute                                    Method
---------                                    ------
Data ya information rakhta hai               Koi operation perform karta hai
Example: s.age                               Example: s.show_details()
Normally parentheses nahi lagte              Call karte waqt () lagte hain

Ek chhota sa difference dekho:
------------------------------
s.age             # Attribute access
s.show_details()  # Method call

* Method ka naam likh dena aur method ko call karna alag baatein hain. 
  s.show_details method ko refer karta hai, jabki s.show_details() 
  use execute karta hai.

============================================================================

5. Kya har self.something public hota hai?

Nahi. Lekin agar tum likhte ho:
-------------------------------
self.name = name          // Toh name ek normal public attribute hai.

Aur:
----
def show_details(self):  // Toh show_details ek normal public method hai.
    ... 

* Python mein public members ke liye koi special keyword likhne ki zaroorat 
  nahi hoti.

* Tumhe public name ya public def nahi likhna hota. Normal naming hi public 
  access ke liye use hoti hai.

============================================================================

6. Public Attributes aur Methods ko ek saath use karna

* Ab ek complete example dekhte hain.

CODE:
-----
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

    def show_balance(self):
        print("Balance:", self.balance)


account = BankAccount("Rahul", 1000)

# Public attributes
print(account.owner)
print(account.balance)

# Public method
account.deposit(500)
account.show_balance()

Output:
-------
Rahul
1000
Balance: 1500

----------------------------------------------------------------------------

Yahan:
------
. owner aur balance public attributes hain.
. deposit() aur show_balance() public methods hain.
. account.deposit(500) method ko call karta hai.
. Method self.balance += amount ke through object ka balance update karta hai.

* Lekin is code mein validation nahi hai. Agar tum account.deposit(-5000) 
  call karoge, toh balance negative ho sakta hai. Public method hone ka 
  matlab ye nahi ki method automatically safe hai.

============================================================================

7. Tumhare Getter/Setter wale concept se iska connection

Tumne pehle ye padha tha:
-------------------------
class Student:
    def __init__(self, age):
        self._age = age

    def get_age(self):
        return self._age

* Yahan get_age() ek normal public method hai. Lekin _age attribute 
  internal-use convention follow karta hai.

* Iska matlab public method kisi aise attribute ko bhi access kar 
  sakta hai jo normal public naming follow nahi karta.

* Public method aur public attribute alag cheezein hain. Ek method 
  public ho sakta hai, jabki uske andar use hone wala attribute _age 
  ho.

* Baad mein jab tum Encapsulation ko aur deeply samjhoge, tab dekhenge 
  ki public methods ke through controlled access kaise design karte hain.

============================================================================

Final revision
--------------
. Public Attribute : Object ka data, jaise self.age.

. Public Method    : Object ka operation, jaise show_details().

. Access           : s.age se attribute access hota hai; 
                     s.show_details() se method call hota hai.

. Modification     : Public attributes ko normally bahar se directly 
                     modify kiya ja sakta hai.

============================================================================
----------------------------------------------------------------------------
============================================================================

1. Class ke bahar aur object ke bahar mein kya difference hai?

Dono ka meaning alag hai:
-------------------------
Class ke bahar : Class ke code block ke bahar likha hua code.

Object ke bahar: Class ke bahar se object ke attributes ko access 
                 karna ya uske methods ko call karna.

----------------------------------------------------------------------------

* Normally, jab hum public attributes aur methods padhte hain, toh 
  hum unhe class ke bahar likhe code se, object ke through access 
  karte hain.

Example:
--------
class Student:
    def __init__(self):
        self.age = 20

    def show_details(self):
        print(self.age)


s = Student()
print(s.age)
s.show_details()

----------------------------------------------------------------------------

#Yahan samjho:

Class ke andar
--------------
def show_details(self):
    print(self.age)

* Method class ke andar define hota hai. self.age se method, 
  current object ki age value access karta hai.

Class ke bahar
--------------
s = Student()
print(s.age)
s.show_details()

* Yahan hum object s ke through attribute access aur method call 
  kar rahe hain.

============================================================================

2. Toh public ki correct definition kya hogi?

* Public attribute ya method woh hai jise normally class ke bahar se 
  object ke through access kiya ja sakta hai.

Isliye meri dono statements ka intended meaning ek hi tha:
----------------------------------------------------------
. "Object ke bahar se access" — object ke methods ke andar ke bajaye 
                                bahar se access.

. "Class ke bahar se access"  — class ki definition ke bahar se access.

----------------------------------------------------------------------------

* Python mein is topic ko samjhane ke liye class ke bahar se object 
  ke through access kehna zyada precise hai.

* Ek chhoti si nuance : Python mein public member ko class ke andar 
                        se bhi access kar sakte hain. Public ka 
                        matlab ye nahi ki use sirf class ke bahar 
                        hi access karna hai.

* Final rule          : Public ka matlab access ki permission sirf 
                        bahar ke liye nahi, balki normal access par 
                        koi special restriction nahi hai. Class ke 
                        bahar se s.age aur s.show_details() iska 
                        simple example hain.

