3. ABC (abc module) kya hota hai ??

* ABC ka full form Abstract Base Class hai.

* Python mein abc ek built-in module hai, jiska use Abstract Classes 
  banane ke liye kiya jata hai.

* Abhi humne padha ki Abstract Class common structure aur rules define 
  karti hai. Lekin Python ko kaise batayenge ki koi class Abstract Class 
  hai?

  Iske liye hum ABC ko import karke apni class ko usse inherit karwate 
  hain.

===============================================================================

1. Example dekho
----------------
from abc import ABC

class Animal(ABC):
    pass

Ab is code ko samjho:
---------------------
- from abc import ABC — Python ke abc module se ABC import kiya.

- class Animal(ABC):  — Animal class, ABC ko inherit kar rahi hai.

Lekin ek important baat: Sirf ABC ko inherit karne se class mein 
                         abstract methods automatically nahi ban 
                         jaate.

===============================================================================

2. Phir ABC ka actual fayda kya hai?

* ABC humein aisi class banane ka base deta hai jisme hum abstract 
  methods define kar sakte hain.

CODE:
-----
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        print("Bhau bhau")

dog = Dog()
dog.sound()

Output:
-------
Bhau bhau

-------------------------------------------------------------------------------

* Yahan Animal(ABC) se Abstract Class banayi aur @abstractmethod se sound() 
  ko abstract method banaya.

* Agar Dog class sound() implement nahi karegi, toh Dog() ka object banate 
  waqt Python TypeError dega.

Abhi tak kya samjhe ?
---------------------
Term                 | Kaam
---------------------|--------------------------------------------
abc module           | Python ka built-in module
ABC                  | Abstract Base Class banane ka base
Abstract Class       | Common structure aur rules define karti hai
@abstractmethod      | Method ko abstract declare karta hai

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Q) agr hum aisa naa kre toh kya acstract class or abstract method nhi bana 
   sakte hum ??

   from abc import ABC, abstractmethod

-------------------------------------------------------------------------------

ANS) Haan, tumne sahi jagah question poocha. Lekin iska answer do parts mein 
     samjho. Python mein ABC aur @abstractmethod use kiye bina bhi abstraction 
     ka concept use kar sakte ho, lekin Python ka built-in abstract class 
     mechanism use karne ke liye inki zaroorat hoti hai.

===============================================================================

1. Agar hum ABC aur @abstractmethod import na karein:

class Animal:
    def sound(self):
        pass

a = Animal()
a.sound()

--> Ye code bina error ke chalega.

Lekin:
------
- Animal ek normal class hai, abstract class nahi.
- sound() ek normal method hai, abstract method nahi.
- Python Animal ka object banane se nahi rokega.
- Python Child class ko sound() implement karne ke liye force nahi karega.

===============================================================================

2. Agar hum ABC aur @abstractmethod use karein:

from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass

a = Animal()

* Is baar Python TypeError dega, kyunki Animal mein abstract method 
  sound() hai aur uska object directly nahi banaya ja sakta.

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Q) Python mein ABC aur @abstractmethod ke bina bhi Abstraction ka concept
   use ho sakta hai, lekin uske liye implementation details ko hide karke 
   user ko sirf zaroori functionality deni hoti hai.

   es baat ko proof krke batana or tu ABC or @abstractmethod ka use krke
   nhi batayega.

-------------------------------------------------------------------------------

ANS) Bilkul. Is baar ABC aur @abstractmethod use kiye bina example se prove 
     karte hain ki Python mein Abstraction kaise ho sakta hai.

Example: ATM Machine
--------------------
ATM use karte waqt tumhe sirf amount enter karke paise withdraw karne hote 
hain. Andar balance check karna aur balance update karna kaise hota hai, 
uski details tumhe jaanne ki zaroorat nahi hoti.

CODE:
-----
class ATM:
    def __init__(self, balance):
        self.__balance = balance

    def withdraw(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
            print("Cash withdrawn:", amount)
            print("Remaining balance:", self.__balance)
        else:
            print("Insufficient balance")

atm = ATM(5000)
atm.withdraw(1000)

Output:
-------
Cash withdrawn   : 1000
Remaining balance: 4000

===============================================================================

# Abstraction kahan hai?

User ko kya dikh raha hai ?
---------------------------
atm.withdraw(1000) — user ko sirf withdraw karne ka method use karna 
hai.

Implementation details kya hain ?
---------------------------------
Balance kaise check hota hai, paise kaise deduct hote hain aur balance 
kaise update hota hai — ye sab withdraw() method ke andar handle hota 
hai.

__balance ka kya role hai ?
---------------------------
Double underscore Python mein name mangling karta hai, jisse balance 
ko class ke bahar directly access karna mushkil hota hai. Ye complete 
security nahi hai, lekin internal detail ko hide karne mein madad 
karta hai.

-------------------------------------------------------------------------------

Proof: User ko internal details likhne ki zaroorat nahi:

User sirf ye likhta hai:
------------------------
=> atm.withdraw(1000)

Usse ye sab manually nahi likhna padta:
---------------------------------------
# Balance check karo
# Balance se amount minus karo
# Updated balance store karo
# Result print karo

--> Ye kaam withdraw() method khud karta hai.

-------------------------------------------------------------------------------

Conclusion: Ye Abstraction ka example hai, aur ismein ABC ya @abstractmethod 
            ka use nahi hua. Yahan Abstraction ka matlab hai user ko simple 
            interface dena aur internal implementation details ko method ke 
            andar rakhna.
    
===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Q) agr isse hi Abstraction achieve ho rha hai toh phir ABC ya @abstractmethod 
   ko kyu use kar rhe hai ??

-------------------------------------------------------------------------------

ANS) Bhai, yahi main difference hai: Abstraction achieve karna aur subclasses 
     ko rules follow karne ke liye force karna, dono alag cheezein hain.

     ATM wale example mein Abstraction ho raha hai. Lekin ABC aur @abstractmethod 
     ka purpose thoda alag hai.

===============================================================================

1. ABC aur @abstractmethod ke bina:

* Maan lo tumhare paas alag-alag payment methods hain:

CODE:
-----
class Payment:
    def pay(self, amount):
        print("Payment processing...")

class UPI(Payment):
    pass

class Card(Payment):
    pass

upi = UPI()
card = Card()

upi.pay(500)
card.pay(1000)

--> Ye code chalega, lekin problem ye hai ki UPI aur Card ne apna 
    payment logic implement hi nahi kiya. Phir bhi unke objects 
    ban gaye aur payment method call ho gaya.

===============================================================================

2. ABC aur @abstractmethod ke saath

CODE:
-----
from abc import ABC, abstractmethod

class Payment(ABC):
    @abstractmethod
    def pay(self, amount):
        pass

class UPI(Payment):
    def pay(self, amount):
        print("UPI payment:", amount)

class Card(Payment):
    def pay(self, amount):
        print("Card payment:", amount)

upi = UPI()
card = Card()

upi.pay(500)
card.pay(1000)

* Ab agar UPI ya Card class mein pay() method implement nahi kiya, 
  toh us class ka object banane par Python TypeError dega.

===============================================================================

# Dono ka main difference:

Feature                    | Normal class             | ABC + @abstractmethod
---------------------------|--------------------------|------------------------
Abstraction possible?      | Haan                     | Haan
Method implementation hide?| Haan, design par depend  | Haan, design par depend
Method implement karna     | Force nahi hota          | Force hota hai
Incomplete object rokna    | Automatically nahi       | Haan

===============================================================================

Yaad rakhne wali baat:
---------------------
- Abstraction ka purpose           : user ko zaroori functionality dena aur 
                                     implementation details hide karna.

- ABC + @abstractmethod ka purpose : abstract methods ko subclasses mein 
                                     implement karna compulsory banana.

* Matlab, ABC aur @abstractmethod Abstraction achieve karne ka ek formal 
  tareeka hain, lekin ye Abstraction ke liye compulsory nahi hain. Ye bade
  projects mein useful hain, jahan ensure karna hota hai ki har subclass 
  required methods implement kare.