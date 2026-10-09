1. Sabse pehle: Encapsulation hota kya hai?

* Encapsulation Python ki Object-Oriented Programming (OOP) ka 
  ek important concept hai.

Simple language mein:
---------------------
Encapsulation ka matlab hai data aur us data par kaam karne wale 
methods ko ek class ke andar organize karna, aur data ko access 
ya modify karne ke tareeke ko control karna.

Is definition ko do parts mein samjho:
--------------------------------------
Data    : Kisi cheez ki information, jaise bank account ka balance, 
          student ka marks ya car ki speed.

Methods : Aise functions jo us data par kaam karte hain, jaise paise 
          deposit karna, marks update karna ya speed badhana.

Chalo, ab ek real-life example se samajhte hain.

==================================================================================

2. Real-life example: Bank Account

* Socho tumhara ek bank account hai aur usmein ₹10,000 pade hain.

Tum kya kar sakte ho ?
----------------------
--> Paise deposit kar sakte ho.
--> Paise withdraw kar sakte ho.
--> Apna balance check kar sakte ho.

* Lekin kya tum bank mein jaakar bas bol sakte ho ki mera balance 
  ₹10,000 se badhakar ₹1 crore kar do, bina paise deposit kiye ??
  Nahi!

* Bank ek proper process follow karta hai. Deposit karne par amount 
  add hoti hai aur withdrawal karne par check hota hai ki account 
  mein sufficient balance hai ya nahi.

Yahan ek important idea hai:
----------------------------
Data ko directly kisi bhi tarah change karne dene ke bajaye, us par 
controlled operations perform karna.

Programming mein Encapsulation isi tarah ka design banane mein help 
karta hai.

==================================================================================

3. Python mein bina Encapsulation ke kya problem ho sakti hai?

* Sabse pehle ek simple class dekhte hain.

CODE:
-----
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

Ab is code ki har line samjho.
------------------------------
. class BankAccount: — ek class define kar rahe hain.

. __init__() — object banne par automatically chalne 
               wala special method.

. self.balance = balance — object ke andar balance naam 
                 ka attribute store kar rahe hain.

Ab object banate hain:
----------------------
account = BankAccount(10000)
print(account.balance)

Output:
-------
10000    // Ab tak sab sahi hai.

<------------------------------------------------------->

Lekin dekho:
------------
account.balance = -500
print(account.balance)

Output:
-------
-500

* Kya hua? Humne bina kisi validation ke balance negative kar 
  diya.

* Python ne humein nahi roka, kyunki balance ek public attribute 
  hai aur us par koi restriction nahi lagayi gayi hai.

* Dhyan do: Problem ye nahi hai ki public attributes galat hain. 
  Problem ye hai ki is example mein balance ko validate karne ka 
  koi rule nahi hai.

==================================================================================

4. Ab Encapsulation ka use karke problem solve karte hain:

Hum chahte hain ki: 
-------------------
1. Account ka balance check kiya ja sake.
2. Paise deposit kiye ja sakein.
3. Paise withdraw kiye ja sakein.
4. Invalid amount deposit ya withdraw na ho.
5. Available balance se zyada paise withdraw na hon.

* Iske liye data aur us par kaam karne wale methods ko class 
  mein organize karenge.

CODE:
-----
class BankAccount:
    def __init__(self, balance):
        if balance < 0:
            raise ValueError("Balance negative nahi ho sakta")

        self.balance = balance

    def deposit(self, amount):
        if amount <= 0:
            print("Amount positive honi chahiye")
            return

        self.balance += amount

    def withdraw(self, amount):
        if amount <= 0:
            print("Amount positive honi chahiye")
            return

        if amount > self.balance:
            print("Insufficient balance")
            return

        self.balance -= amount

    def show_balance(self):
        print("Balance:", self.balance)


account = BankAccount(10000)
account.deposit(2000)
account.withdraw(3000)
account.show_balance()

Output:
-------
Balance: 9000

----------------------------------------------------------------------------------

# Chalo, ise step by step samajhte hain.

1. Data — self.balance : Account mein kitne paise hain, 
                         ye store karta hai.

2. deposit()           : Amount positive hai ya nahi check 
                         karta hai, phir balance badhata hai.

3. withdraw()          : Amount aur available balance check 
                         karne ke baad hi paise ghataata hai.

4. show_balance()      : Balance ko dekhne ka ek defined tareeka 
                         deta hai.

* Yahan Encapsulation ka idea samajh aata hai: data aur us data ke 
  operations ek class mein hain, aur operations ke through rules 
  apply kiye ja rahe hain.

----------------------------------------------------------------------------------

**Lekin ek important limitation abhi bhi hai.**

account.balance = -500  // Ye line abhi bhi chal sakti hai!

* Kyun? Kyunki humne balance ko public hi rakha hai. Sirf 
  deposit() aur withdraw() methods banane se direct 
  modification band nahi hota.

* Isliye abhi humne data aur behavior ko organize kiya aur 
  defined operations mein validation lagayi; data ki direct
  access ko abhi strictly control nahi kiya.

==================================================================================

5. Encapsulation ke do important parts:

Part 1
------
# Bundling

* Data aur us par kaam karne wale methods ko ek class mein rakhna.

--> Example: balance, deposit() aur withdraw() ek BankAccount class 
              mein.

----------------------------------------------------------------------------------

Part 2
------
# Controlled access

* Data ko modify karne ke liye rules aur suitable methods provide 
  karna.

--> Example: negative deposit reject karna aur insufficient balance 
             par withdrawal rokna.

----------------------------------------------------------------------------------

* Ye dono ideas related hain, lekin exactly same nahi hain.

Ek class mein data aur methods ko rakhna bundling hai. Us data 
ko kaise access ya modify kiya ja sakta hai, is par rules lagana 
controlled access hai.

Python mein Encapsulation in dono ideas ko combine karke achha 
program design karne mein help karta hai.

==================================================================================

6. Kya Encapsulation ka matlab data ko hide karna hai?

**Ye bahut important question hai.**

* Nahi, sirf data hide karna Encapsulation ki poori definition 
  nahi hai.

* Data hiding, Encapsulation se related ek technique hai. 
  Encapsulation ka broader goal data aur behavior ko 
  organize karna aur access ko manage karna hai.

----------------------------------------------------------------------------------

* Python mein attributes ke teen common patterns dekhne ko milenge:

Pattern                     Example               Meaning
-------                     -------               -------
Public                      balance               Normal public access
Protected convention        _balance              Internal use ka signal
Private-style               __balance             Name mangling apply hoti hai

--> Inka practical difference hum agle lessons mein detail se padhenge.

----------------------------------------------------------------------------------

Abhi sirf yaad rakho:
---------------------
. _balance par Python automatic strict restriction nahi lagata.

. __balance bhi completely inaccessible nahi hota.

. Sirf double underscore likh dene se har tarah ki invalid 
  modification nahi rukti.

==================================================================================

7. Real Encapsulation ka ek aur practical example

* Ab hum balance ko private-style attribute __balance banayenge 
  aur balance check karne ke liye method provide karenge.

CODE:
-----
class BankAccount:
    def __init__(self, balance):
        if balance < 0:
            raise ValueError("Invalid opening balance")

        self.__balance = balance

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Amount positive honi chahiye")

        self.__balance += amount

    def get_balance(self):
        return self.__balance


account = BankAccount(10000)
account.deposit(2000)
print(account.get_balance())

Output:
-------
12000

----------------------------------------------------------------------------------

Is example mein:
----------------
. self.__balance balance store karta hai.

. deposit() amount validate karke balance update karta hai.

. get_balance() balance return karta hai.

. Bahar ka code normal account.__balance se attribute access 
  nahi kar sakta, kyunki Python name mangling use karta hai.

----------------------------------------------------------------------------------

* Lekin yaad rakho: ye bhi absolute security nahi hai. Python mein name 
  mangling ka purpose primarily accidental access aur subclass mein 
  naming conflicts ko reduce karna hai.

* Ek aur subtle point: agar tum get_balance() use kar rahe ho, toh iska 
  matlab ye nahi ki attribute automatically read-only ban gaya. Python 
  mein is design ko aur robust banane ke liye properties aur suitable 
  validation techniques bhi use ki ja sakti hain.

==================================================================================

8. Encapsulation ke benefits kya hain?

1. Data integrity          : Invalid changes ko defined operations ke through rok 
                             sakte ho.

2. Maintainability         : Validation ka logic ek jagah rakhne se changes manage 
                             karna aasaan hota hai.

3. Abstraction             : User ko har internal detail jaane bina deposit() jaise 
                             methods use karne milte hain.

4. Controlled modification : Class ke rules ke according data update karne ka 
                             interface milta hai.

* Ek practical limitation bhi samjho: agar public attribute ko kahin bhi 
  directly modify kiya ja sakta hai, toh sirf methods mein validation 
  likhne se data integrity guarantee nahi hoti. Design mein direct 
  modification ko bhi consider karna padta hai.

----------------------------------------------------------------------------------

Final revision: Ek line mein Encapsulation
------------------------------------------
Encapsulation = data aur uske related methods ko ek unit mein organize karna, 
                aur data ko access ya modify karne ke tareeke ko manage karna.