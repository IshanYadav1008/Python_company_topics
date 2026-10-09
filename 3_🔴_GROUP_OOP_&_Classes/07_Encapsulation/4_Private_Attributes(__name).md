1. Private attribute (__name) kya hota hai?

* Jab Python class mein kisi attribute ke naam ke aage double 
  underscore __ lagate hain, toh Python us naam ko special 
  tarike se handle karta hai.

CODE:
-----
class Student:
    def __init__(self):
        self.__marks = 80

s = Student()
print(s.__marks)  # Error

Error kyun aayega ?
-------------------
Kyunki Python __marks ko name mangling ke through internally doosre 
naam mein badal deta hai. Isliye s.__marks se directly access nahi 
kar sakte.

Dhyan rahe: Python ise completely private nahi banata, lekin direct 
access ko mushkil banata hai.

================================================================================

2. Name Mangling kya hai?

* Name mangling ka matlab hai: Python class ke andar __ se shuru hone 
  wale attribute ka naam internally badal deta hai.

Example:
--------
class Student:
    def __init__(self):
        self.__marks = 80

s = Student()
print(s._Student__marks)  # 80

* Yahan Python __marks ko internally _Student__marks naam se store 
  karta hai.

* Isliye s._Student__marks likhne par value mil jaati hai.

================================================================================

3. Kya Name Mangling ko alag se padhna chahiye?

* Nahi, abhi alag se padhne ki zaroorat nahi. Private attributes ke 
  saath hi name mangling samajhna sahi rahega, kyunki dono directly 
  related hain.

Copy karne ke liye table
------------------------
Sawal                                      | Jawab
================================================================================
__marks ka matlab?                         | Private-style attribute
-------------------------------------------|------------------------------------
Double underscore __ kyun lagate hain?     | Direct access ko mushkil banane ke 
                                           | liye
-------------------------------------------|------------------------------------
Bahar se s.__marks access hoga?            | Nahi, normally error aayega
-------------------------------------------|------------------------------------
Name mangling kya hai?                     | Python attribute ka naam badal deta
                                           | hai
-------------------------------------------|------------------------------------
__marks ka internal naam kya hoga?         | _Student__marks
-------------------------------------------|------------------------------------
Kya name mangling se attribute completely  | Nahi
private hai?                               | 

--------------------------------------------------------------------------------

* Yaad rakhne wali baat:

marks   → Public
_marks  → Protected convention
__marks → Private-style + name mangling

* Abhi itna samajhna kaafi hai. Getter/Setter mein aage chal kar 
  private attributes ka use bhi dekh sakte hain.

================================================================================
--------------------------------------------------------------------------------
================================================================================

Q) bhale Python __marks ko internally _Student__marks naam se store karta hai. 
   lekin jab s._Student__marks likhne par value mil hi jaati hai, toh file 
   private hone ka kya mtlb nikla access toh ho hi gaya naa phir bhi

--------------------------------------------------------------------------------

ANS) Bilkul sahi pakda tune! 👍 Tera question valid hai. Agar s._Student__marks 
     likhne par value mil jaati hai, toh ye completely private nahi hai.

Simple tarike se samajh:
------------------------

1. Phir __marks ka fayda kya hai?

Maan le class mein marks hain:
------------------------------
class Student:
    def __init__(self):
        self.__marks = 80

    def show_marks(self):
        print(self.__marks)

s = Student()
s.show_marks()            # 80
print(s.__marks)          # Error
print(s._Student__marks)  # 80

. s.__marks         → Direct access nahi hota.
. s._Student__marks → Access ho jaata hai.
. s.show_marks()    → Class ka method marks dikha sakta hai.

================================================================================

2. Toh private banane ka asli matlab kya hai?

* __marks ka matlab ye nahi ki koi bhi bahar se access nahi 
  kar sakta.

Iska main fayda hai:
--------------------
. Galti se attribute ko bahar se access ya modify karne se bachana.

. Child class mein same naam ke attributes ke saath takraav hone 
  ki possibility kam karna.

. Class ke internal data ko manage karna aasan banana.

================================================================================

Copy karne ke liye table
------------------------

Sawal                                      | Jawab
-------------------------------------------|----------------------------------
Kya __marks completely private hai?        | Nahi
Kya s.__marks se access hoga?              | Normally nahi
Kya s._Student__marks se access hoga?      | Haan
Phir __marks ka fayda kya hai?             | Accidental access aur name conflicts 
                                           | kam karna.
Kya ye security feature hai?               | Nahi, strong security nahi hai

Ek line mein: Python mein __marks ka purpose data ko completely chhupana 
              nahi, balki accidental access aur inheritance mein name 
              conflicts ko kam karna hai.