1. Abstraction kya hota hai ?

* Abstraction ka matlab hai: User ko sirf zaroori cheezein dikhana aur 
                             andar ka complex implementation chhupana.

# Real-life example: ATM machine 
--------------------------------
* Jab tum ATM se paise nikaalte ho, toh tumhe bas ye steps karne hote 
  hain:

1. Card insert karo.
2. PIN enter karo.
3. Amount enter karo.
4. Cash receive karo.

* Tumhe ye jaanne ki zaroorat nahi hoti ki ATM ke andar bank server se 
  connection kaise banta hai, account balance kaise verify hota hai ya 
  cash machine se kaise nikalta hai.

* Tumhe zaroori functionality dikhai jaati hai, lekin andar ka complex 
  process chhupaya jaata hai. Yahi Abstraction hai.

=================================================================================

2. Python mein Abstraction kaise samjhein ?
-------------------------------------------

* Maan lo tum ek payment system bana rahe ho. User ko bas pay() method 
  call karna hai. Payment process andar kaise hota hai, woh user ko 
  jaanne ki zaroorat nahi.

CODE:
-----
class Payment:
    def pay(self):
        print("Payment processing...")

payment = Payment()
payment.pay()

Output:
-------
Payment processing...

* Is example mein pay() method payment karne ka ek simple interface deta 
  hai. Ye abhi sirf ek basic illustration hai; actual payment process 
  implement nahi kiya gaya hai.

* Important: Abstraction ka matlab sirf code ko kisi method ke andar rakh 
             dena nahi hai. Iska main idea hai ki user ko kya use karna 
             hai aur implementation kaise hoti hai, in dono ko alag rakhna.

=================================================================================

3. Abstraction ka fayda kya hai ?

- Complexity kam hoti hai         : User ko har internal detail samajhne ki 
                                    zaroorat nahi.

- Code use karna aasaan hota hai  : User ko pata hota hai ki kaunsa method call 
                                    karna hai.

- Implementation badal sakte hain : Andar ka code badalne par bhi, agar method 
                                    ka interface same rahe, toh use karne wala 
                                    code aksar badalne ki zaroorat nahi hoti.

=================================================================================

4. Abstraction aur Encapsulation mein farak:

Dono related hain, lekin same nahi hain.

Concept       | Simple Meaning
--------------|-----------------------------------------------
Abstraction   | Zaroori functionality dikhana, implementation
              | ki details chhupana
Encapsulation | Data aur methods ko class mein organize karna
              | aur data tak access ko control 
              
=================================================================================

5. Abstraction ke baad kya aayega ?

* Python mein formal abstraction implement karne ke liye hum Abstract Class, 
  ABC aur @abstractmethod padhte hain.

* Lekin yaad rakho: Abstraction ek OOP concept hai. ABC aur @abstractmethod 
  Python mein is concept ko implement karne ke tools hain.