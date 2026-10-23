# Python f-strings — Simple aur Clear Explanation
-------------------------------------------------

* Sabse pehle samjho: f-string ka use Python mein kisi string ke andar 
                      variable ki value insert karne ke liye hota hai.

1. f-string kya hoti hai ?
--------------------------
* Maan lo tumhare paas ek variable hai:

=> name = "Rahul"   // Ab tumhe print karna hai: My name is Rahul

Iske liye f-string ke bina:
---------------------------
=> name = "Rahul"print("My name is " + name)

Output:
-------
My name is Rahul

----------------------------------------------------------------------------------

* Lekin Python mein ek aur easy method hai — f-string.

name = "Rahul"
print(f"My name is {name}")

Output:
-------
My name is Rahul

* Dekha ? Kaam wahi hai, lekin code likhna aur samajhna 
          easy ho gaya.

==================================================================================

2. f-string ka rule kya hai ?
-----------------------------

* Bas 2 cheezein yaad rakho:

Rule 1: String se pehle f lagao
-------------------------------
f"Hello"

Rule 2: Variable ko {} ke andar likho
-------------------------------------
name = "Rahul"
print(f"Hello {name}")

Output: Hello Rahul

* Yaad rakhna: f + string + {variable} = f-string.

==================================================================================

3. Ek se zyada variables kaise use karein ?
-------------------------------------------

name = "Rahul"
age  = 20
print(f"My name is {name} and I am {age} years old.")

Output:
-------
My name is Rahul and I am 20 years old.

- Tum ek hi f-string mein jitne chaaho variables use kar 
  sakte ho.

==================================================================================

4. Kya f-string mein calculations bhi kar sakte hain ?
------------------------------------------------------

* Haan! Ye f-strings ka ek useful feature hai. 

a = 10
b = 20
print(f"Total = {a + b}")

Output:
-------
Total = 30

<------------------------------------------------------->

Ek aur example:
---------------
price = 100
quantity = 3
print(f"Total price = {price * quantity}")

Output:
-------
Total price = 300

- Curly braces {} ke andar sirf variables hi nahi, balki 
  Python expressions bhi likh sakte ho.

==================================================================================

5. Common mistake — isse bachna:
--------------------------------

name = "Rahul"
print("Hello {name}")

Output:
-------
Hello {name}

- Aisa kyun? Kyunki string ke aage f nahi lagaya.

Sahi code:
----------
=> print(f"Hello {name}")

Output:
-------
Hello Rahul

==================================================================================

Question: Is code ka output kya hoga ?
--------------------------------------

name  = "Amit"
marks = 85
print(f"{name} scored {marks} marks")

o/p: Amit scored 85 marks

Bilkul sahi!
------------
=> {} ke andar variables ki values print hongi,
      kyunki string ke aage f laga hai.

- Bas itna samajh lo: f-strings ka main kaam strings ke andar 
  variables aur calculations ko easily display karna hai. Ye 
  Python 3.6 se available hain.