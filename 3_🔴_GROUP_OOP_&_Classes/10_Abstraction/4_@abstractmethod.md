@abstractmethod ek decorator hai jo Python mein kisi method ko abstract 
method mark karta hai. Jab ye method kisi Abstract Class mein hota hai, 
toh us class ki Child Class ko us method ko implement karna padta hai, 
warna Child Class ka object nahi bana sakte.

1. Pehle bina @abstractmethod ke dekho:
---------------------------------------

CODE:
-----
class Payment:
    def pay(self, amount):
        pass

class UPI(Payment):
    pass

upi = UPI()
upi.pay(500)

* Ye code chalega. Kyun? Kyunki Python ke liye pay() ek normal method 
  hai. Python Child Class ko ise implement karne ke liye force nahi 
  karta.

==============================================================================

2. Ab @abstractmethod use karo:

CODE:
-----
from abc import ABC, abstractmethod

class Payment(ABC):
    @abstractmethod
    def pay(self, amount):
        pass

class UPI(Payment):
    pass

upi = UPI()

Output:
-------
TypeError: Can't instantiate abstract class UPI
with abstract method pay

* Ab error kyun aaya? Kyunki UPI ne Parent Class se pay() method 
  inherit kiya, lekin use implement nahi kiya. Isliye Python ne 
  UPI ka object banane se rok diya.

==============================================================================

3. Child Class mein method implement karo:

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

upi = UPI()
upi.pay(500)

Output:
-------
UPI payment: 500

* Ab code chal gaya, kyunki UPI ne pay() method implement kar diya.

==============================================================================

4. @abstractmethod actually karta kya hai ??

1. Method ko mark karta hai:
   @abstractmethod Python ko batata hai ki ye method abstract hai.


2. Python implementation check karta hai:
   ABC ke mechanism ki help se Python check karta hai ki Child Class 
   ke required abstract methods implement hue hain ya nahi.


3. Incomplete Child Class ka object rokta hai:
   Agar required method implement nahi hua, toh us Child Class ka 
   object nahi ban sakta.

==============================================================================

5. Kya @abstractmethod akela use kar sakte hain ?

* Aam taur par formal Abstract Class banane ke liye ABC aur
  @abstractmethod dono use karte hain.

CODE:
-----
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass

Yahan:
------
- ABC             — class ko Python ke abstract-class mechanism se jodta 
                    hai.

- @abstractmethod — sound() ko abstract method mark karta hai.

- pass            — method ka body khaali rakhta hai; pass khud method ko 
                    abstract nahi banata.

**Ek important baat**
---------------------
Child Class mein method ka naam aur parameters compatible hone chahiye. 
Sirf same naam ka method likh dena har situation mein sahi implementation 
ki guarantee nahi deta; Python mainly ye check karta hai ki abstract method 
override hua hai ya nahi.

Short mein: @abstractmethod ek rule define karne mein help karta hai: jo 
            Child Class is Abstract Class ka object banana chahti hai, 
            use required abstract methods implement karne honge.

==============================================================================
------------------------------------------------------------------------------
==============================================================================

Q) Tumhara doubt bilkul logical hai. Tum ye pooch rahe ho: Agar abstract 
   method ko implement karna Child Class ki responsibility hai, toh jis 
   Parent Class mein abstract method hai, usi ka object banane par error 
   kyun aata hai ?

------------------------------------------------------------------------------

ANS) 

1. Sabse pehle: Abstract Method ka rule kya hai ?

Maan lo hum Animal ki class bana rahe hain:
-------------------------------------------
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass

* Humne sound() method banaya, lekin usmein actual implementation 
  nahi di.

* Ab socho, kya har animal ki sound ek jaisi hoti hai ?

- Dog ki sound: Bhau bhau
- Cat ki sound: Meow meow
- Cow ki sound: Moo moo

--> Isliye hum chahte hain ki har specific animal ki class apne 
    hisaab se sound() implement kare.

==============================================================================

2. Phir Animal ka object kyun nahi bana sakte ?

=> a = Animal()   // Isse TypeError aayega.

* Kyunki humne Animal class mein sound() ko abstract mark kiya hai. 
  Python ke abstract-class mechanism ko bataya gaya hai ki sound() 
  ek required method hai, jiski implementation abhi pending hai.

------------------------------------------------------------------------------

Yahan ek important baat samjho:
-------------------------------
* Animal class khud bhi us rule ke under aati hai. Usne sound() ko 
  implement nahi kiya, isliye Python uska object banane nahi deta.

* Ye sirf Child Class par lagne wala rule nahi hai. Abstract Class 
  ka object banane par bhi error aata hai agar usmein abstract 
  methods pending hain.

==============================================================================

3. Toh Child Class ka kya role hai ?

Ab hum Dog class banate hain:
-----------------------------
class Dog(Animal):
    def sound(self):
        print("Bhau bhau")

d = Dog()
d.sound()

Output:
-------
Bhau bhau

* Yahan Dog ne Animal ka abstract method sound() implement kar diya. 
  Isliye Dog ka object ban sakta hai.

------------------------------------------------------------------------------

* Lekin agar implementation nahi dete:

class Dog(Animal):
    pass

d = Dog()

* Toh TypeError aayega, kyunki Dog mein abhi bhi sound() implement 
  nahi hua.

==============================================================================

4. Lekin Python ko kaise pata chalta hai ki object rokna hai?

Ismein teen cheezein kaam karti hain:
-------------------------------------

ABC
----
* Animal ko Python ke abstract-class mechanism se jodta hai.


@abstractmethod
---------------
* sound() ko abstract method mark karta hai, yaani is method 
  ki implementation required hai.


ABCMeta
-------
* Python ka metaclass hai jo track karta hai ki abstract methods 
  implement hue hain ya nahi. Agar pending abstract methods hain, 
  toh object banane se rokta hai.

**Ek zaroori correction:**
sirf ABC inherit karne se class ka object banana mana nahi hota. 
Object tab block hota hai jab us class mein abstract methods 
implement hona baaki hon.

==============================================================================

5. Kya Abstraction ke liye ye sab zaroori hai?

* Nahi. Tumne pehle ATM wala example dekha tha:

class ATM:
    def __init__(self, balance):
        self.__balance = balance

    def withdraw(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
            print("Cash withdrawn:", amount)
        else:
            print("Insufficient balance")

* Is example mein user sirf atm.withdraw(1000) call karta hai. Balance 
  check karne aur deduct karne ki details method ke andar hain. Ye 
  Abstraction ka example hai, aur ismein ABC ya @abstractmethod ki 
  zaroorat nahi.

* Toh phir ABC aur @abstractmethod kyun use karte hain ?
 
  Jab humein ye compulsory karna ho ki har Child Class apne required 
  methods implement kare, tab ye tools kaam aate hain.

==============================================================================

6. Saare concepts ka final difference:

Concept                 | Kaam
------------------------|-----------------------------------------------------
Abstraction             | Implementation details hide karna
Abstract Class          | Required methods/rules define karne wali class
ABC                     | Python ka abstract-class mechanism provide karta hai
@abstractmethod         | Method ko abstract mark karta hai
ABCMeta                 | Pending abstract methods ke rules enforce karta hai
Parent Class            | Jis class ko doosri class inherit karti hai
Child Class             | Jo class Parent Class ko inherit karti hai

* Final baat: Animal ka object isliye nahi ban sakta kyunki uska sound() method 
              abstract hai aur pending hai. Dog ka object tab ban sakta hai jab 
              Dog us method ko implement kar de. Ye rule Python ke abstract-class mechanism ke through enforce hota hai. ABC aur @abstractmethod 
              Abstraction ke liye compulsory nahi hain; ye required methods ko 
              enforce karne ke liye use hote hain.

==============================================================================
------------------------------------------------------------------------------
==============================================================================

Q) tmne bola, Animal class khud bhi us rule ke under aati hai. Usne 
   sound() ko implement nahi kiya. agr kar de toh kya phir iska 
   object ban sakta hai or agr haan toh uska example muje dekhana ??

------------------------------------------------------------------------------

ANS) Haan, agar Animal class khud sound() method implement kar de, toh 
     uska object ban sakta hai, kyunki ab usmein koi pending abstract 
     method nahi hai.

Lekin ek important baat: agar sound() par @abstractmethod laga hua hai, 
toh method ki implementation dene ke baad bhi Animal abstract rahegi. 
Isliye example mein decorator bhi hatana hoga.

==============================================================================

Example 1: Animal khud method implement karti hai:
--------------------------------------------------

from abc import ABC, abstractmethod

class Animal(ABC):
    def sound(self):
        print("Animal makes a sound")

a = Animal()
a.sound()

Output:
-------
Animal makes a sound


* Yahan object ban gaya, kyunki sound() ab abstract method nahi hai.

==============================================================================

Example 2: @abstractmethod laga rahe toh ?
------------------------------------------

from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        print("Animal makes a sound")

a = Animal()4

Is baar TypeError aayega:
-------------------------
Kyun ? Kyunki sound() ke andar code likhne ke baad bhi @abstractmethod 
use method ko abstract mark karta hai. Sirf method ki body likh dene 
se ye marking khatam nahi hoti.

==============================================================================

Yaad rakho:
-----------
- Abstract method ko implement karke aur @abstractmethod hata kar Animal 
  ka object bana sakte ho.

- @abstractmethod laga rahe, toh method ke andar code likha hone par bhi 
  Animal ka object nahi bana sakte.

- Abstract method ke andar code ho sakta hai; pass hona zaroori nahi hai.

==============================================================================
------------------------------------------------------------------------------
==============================================================================

Q) Bahut sahi doubt hai! Tum pooch rahe ho: Agar abstract method ke andar 
   code likha hai, lekin Parent Class ka object nahi bana sakte, toh us 
   code ko execute kaun karega aur uska fayda kya hai ?

------------------------------------------------------------------------------

ANS) Jawab: Child Class us method ko implement karte waqt Parent Class ke 
             abstract method ke code ko super() se call kar sakti hai. 
             Chalo example dekhte hain.

==============================================================================

Example: Abstract method ke andar code
--------------------------------------
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        print("Animal sound system started")

class Dog(Animal):
    def sound(self):
        super().sound()
        print("Bhau bhau")

d = Dog()
d.sound()

Output:
-------
Animal sound system started
Bhau bhau

==============================================================================

Yahan kya hua ?
---------------
1. Animal ka direct object nahi banaya.
2. Animal ke abstract sound() method ke andar code likha hua tha.
3. Dog ne sound() ko implement kiya.
4. super().sound() se Dog ne Parent Class ke method ka code execute 
   kar diya.
5. Uske baad Dog ne apna code execute kiya.

* Isliye abstract method ke andar likha code bhi useful ho sakta hai.

==============================================================================

# Toh abstract method mein code likhne ka fayda kya hai ??

* Maan lo sabhi animals ke sound process karne se pehle ek common kaam 
  karna hai. Parent Class us common code ko abstract method mein rakh 
  sakti hai. Child Class us code ko super() se reuse kar sakti hai aur 
  phir apna specific kaam kar sakti hai.

* Ek important baat: @abstractmethod method ko abstract mark karta hai, 
                     chahe uske andar code ho ya pass. Jab tak Child 
                     Class us abstract method ko override nahi karti, 
                     us Child Class ka object nahi ban sakta.

* Yaani abstract method ka code automatically execute nahi hota. Use 
  explicitly call karna padta hai, jaise super().sound() se.