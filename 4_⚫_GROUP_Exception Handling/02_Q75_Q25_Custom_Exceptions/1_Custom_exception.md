1. Custom Exception kya hoti hai?

* Python mein ValueError, TypeError jaise built-in exceptions pehle se 
  hoti hain.

* Lekin maan le tu ek college admission program bana raha hai. Tera rule 
  hai ki admission ke liye age kam se kam 18 honi chahiye.
  
* Agar age 16 hai, toh tu apne program ke liye ek specific exception banana 
  chahta hai: AgeError.

* Apne program ki specific problem ke liye khud ki exception banana hi Custom 
  Exception kehlata hai.

==================================================================================

2. Custom Exception kaise banate hain ?

class AgeError(Exception):
    pass

Iska matlab:
------------
- class     — nayi class banata hai.

- AgeError  — teri custom exception ka naam hai.

- Exception — Python ki existing exception class hai. Isse inherit 
              karne par AgeError bhi valid exception ban jaati hai.

- pass      — class ke andar abhi extra code nahi likhna.

Exception kyun likha? Taaki Python AgeError ko exception ke roop mein 
pehchaan sake. Normal class ko seedha raise nahi kar sakte.

==================================================================================

3. raise ka use kaise hota hai ?

CODE:
-----
class AgeError(Exception):
    pass

age = 16

if age < 18:
    raise AgeError("Age 18 se kam hai!")

Yahan:
------
1. if age check karta hai.
2. Age 18 se kam hai, toh condition true hoti hai.
3. raise AgeError exception ko trigger karta hai.
4. Kyunki yahan exception handle nahi ki gayi, program 
   traceback ke saath ruk jayega.

==================================================================================

4. Custom Exception ko try-except se handle karna

* Ab isi code mein exception handle karte hain:

CODE:
-----
class AgeError(Exception):
    pass

try:
    age = 16

    if age < 18:
        raise AgeError("Age 18 se kam hai!")

    print("Admission successful!")

except AgeError as e:
    print("Admission failed:", e)

print("Program continues.")

Output:
-------
Admission failed: Age 18 se kam hai!
Program continues.


Dhyan de:
---------
- raise ne exception trigger ki.
- except AgeError as e ne exception handle ki.
- e mein error ka message aaya.
- Admission successful! print nahi hua, kyunki exception aane
  ke baad try block ki baaki statements skip ho gayin.
- Program aage chala, lekin admission successful nahi hua.

==================================================================================

5. Kya har baar Custom Exception banana zaroori hai?

Nahi yaar! Agar built-in exception kaafi hai, toh wahi 
use kar sakte ho:

=> raise ValueError("Invalid age")

* Custom exception tab banao jab tumhe apne program ki specific 
  problem ko alag naam dena ho, jaise AgeError, PaymentError ya
  InsufficientBalanceError.

==================================================================================

Ab ek chhota sa test:
---------------------

Question: class AgeError(Exception) mein Exception likhne ka main 
          reason kya hai?

ANS) AgeError ko valid exception type banane ke liye

* Exception se inherit karne par AgeError Python ke exception-handling 
  system ke saath kaam karti hai.