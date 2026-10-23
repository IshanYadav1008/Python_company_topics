1. re module kya hota hai ?
---------------------------

* Python ka re ek built-in module hai, jo Regular Expressions (Regex) 
  ki help se text ko search, match, extract aur replace karne ke kaam 
  aata hai.

Maan lo tumhare paas ye text hai:
---------------------------------
=> text = "My age is 25 and my score is 90"

* Tumhe ismein se saare numbers nikaalne hain. Tab re module use kar 
  sakte ho:

import re

text   = "My age is 25 and my score is 90"
result = re.findall(r"\d+", text)
print(result)

Output:
-------
['25', '90']

Samjho ismein kya hua:
----------------------
- import re → Regex use karne ke liye module import kiya.
- findall() → Saare matching results dhoondhe.
- r"\d+"    → Ek ya zyada digits ka pattern.
- text      → Jis text mein search karna hai.

=============================================================================

2. re module ke important functions:
------------------------------------

* Ye functions tumhe sabse pehle seekhne chahiye.

Function	    Kya karta hai ?
-----------------------------------------------------------------------------
re.search()	    Text mein kahin bhi pehla match dhoondhta hai.
-----------------------------------------------------------------------------
re.match()	    Sirf string ki shuruaat se match check karta hai.
-----------------------------------------------------------------------------
re.fullmatch()	Puri string pattern se match karti hai ya nahi, 
                check karta hai.
-----------------------------------------------------------------------------
re.findall()	Saare matches ki list deta hai
-----------------------------------------------------------------------------
re.finditer()	Matches ko iterator ke roop mein deta hai
-----------------------------------------------------------------------------
re.sub()	    Matching text ko replace karta hai
-----------------------------------------------------------------------------
re.split()	    Pattern ke basis par text ko split karta hai
-----------------------------------------------------------------------------
re.compile()	Pattern ko reusable Regex object mein banata hai
-----------------------------------------------------------------------------

* Ab ek-ek karke examples samjhte hain.

=============================================================================

3. re.search() — Text mein search karna:
----------------------------------------

import re

text   = "Hello Python 123"
result = re.search(r"\d+", text)
print(result.group())

Output:
-------
123

Kaise kaam kiya ?
-----------------
* \d+ numbers ko search karta hai. search() poore text mein pehla 
   match dhoondhta hai, aur .group() matched text deta hai.

* Agar match nahi milta, toh search() None return karta hai.

=============================================================================

4. re.match() — Shuruaat se check karna:
----------------------------------------

import re

text   = "Python 123"
result = re.match(r"\w+", text)
print(result.group())

Output:
-------
Python

- Yahan \w+ starting mein aane wale word characters ko match 
  karta hai.

- Dhyan do: match() string ki shuruaat se matching karta hai.

CODE:
-----
text   = "123 Python"
result = re.match(r"Python", text)
print(result)

Output:
-------
None

- Kyunki string 123 se shuru hoti hai, Python se nahi.

=============================================================================

5. re.fullmatch() — Puri string validate karna:
-----------------------------------------------

* Maan lo tumhe check karna hai ki PIN exactly 6 digits 
  ka hai ya nahi.

CODE:
-----
import re

pin = "452001"

if re.fullmatch(r"\d{6}", pin):
    print("Valid PIN format")
else:
    print("Invalid PIN format")

Output:
-------
Valid PIN format

Yahan:
------
- \d          = digit
- {6}         = exactly 6 baar
- fullmatch() = poori string match honi chahiye

* Agar PIN "45200a" hoga, toh output Invalid PIN format aayega.

* Yaad rakho: ye sirf format check karta hai, PIN asli ya authorized 
              hai ya nahi, ye nahi.

=============================================================================

6. re.findall() — Saare matches nikaalna:
-----------------------------------------

import re

text   = "I have 12 apples and 5 mangoes"
result = re.findall(r"\d+", text)
print(result)

Output:
-------
['12', '5']

* Ye matching numbers ki list deta hai. Jab tumhe text se saare
  numbers, dates ya matching words extract karne hon, toh ye 
  bahut useful hai.

=============================================================================

7. re.sub() — Text replace karna:
---------------------------------

import re

text   = "I like Python. Python is easy."
result = re.sub(r"Python", "Java", text)
print(result)

Output:
-------
I like Java. Java is easy.

* sub() ka matlab substitution ya replacement hai. Ye matching 
  text ko replace karta hai aur updated string return karta hai.

=============================================================================

8. re.split() — Text ko parts mein todna:
-----------------------------------------

import re

text   = "apple,banana;orange mango"
result = re.split(r"[,; ]+", text)
print(result)

Output:
-------
['apple', 'banana', 'orange', 'mango']

* Yahan [,; ]+ comma, semicolon ya space ko separator ke 
  roop mein use karta hai.

=============================================================================

9. re.compile() — Pattern ko baar-baar use karna:
-------------------------------------------------

import re

pattern = re.compile(r"\d+")

print(pattern.findall("Age 25"))
print(pattern.findall("Score 90"))

Output:
-------
['25']
['90']

- Jab ek hi Regex pattern ko baar-baar use karna ho, toh compile() 
  se uska reusable pattern object bana sakte ho.

=============================================================================

10. Sabhi functions ka quick revision:
--------------------------------------

* Neeche poora table ek hi code block mein hai, jiske top-right 
  par Copy icon milega.

+------------------+----------------------------------------------+
| Function         | Use                                          |
+------------------+----------------------------------------------+
| re.search()      | Kahin bhi pehla match dhoondhna              |
| re.match()       | Shuruaat se match karna                      |
| re.fullmatch()   | Puri string validate karna                   |
| re.findall()     | Saare matches ki list nikaalna               |
| re.finditer()    | Matches ka iterator paana                    |
| re.sub()         | Matching text replace karna                  |
| re.split()       | Pattern ke basis par text todna              |
| re.compile()     | Pattern ko reusable object banana            |
+------------------+----------------------------------------------+

=============================================================================

11. Ab tumhari practice:
------------------------

Question 1: Agar text mein se saare numbers ki list nikaalni ho, 
            toh kaunsa function use karoge?

=> text = "Age 20, score 95"

o/p: re.findall()

Bilkul sahi! ✓
--------------
re.findall(r"\d+", text) output dega ['20', '95'].

=============================================================================
-----------------------------------------------------------------------------
=============================================================================

Bhai, bahut achha question hai! ❤️ Tumhe bas ye samajhna hai ki 
re.match() kis cheez ko match karta hai aur \w+ kya dhoondh 
raha hai. Chalo step-by-step dekhte hain.

Example 1: \w+ kya match kar raha hai ?
---------------------------------------
import re

text   = "Python 123"
result = re.match(r"\w+", text)
print(result.group())

Output:
-------
Python

Ismein 3 cheezein samjho:
-------------------------
- re.match() → String ki shuruaat se matching check karta hai.

- \w         → Letter, digit ya underscore mein se kisi ek 
               character ko match karta hai.

- +          → Ek ya zyada consecutive matching characters ko 
               match karta hai.

=============================================================================

Ab string ko dekho:
-------------------
* String ka breakdown

P  y  t  h  o  n  ␠  1  2  3

* Python — match ho gaya, kyunki saare letters \w se match hote 
           hain.

* Space  — \w space ko match nahi karta, isliye matching yahin 
           ruk jaati hai.

* 123    — digits \w se match ho sakte hain, lekin match() starting 
           se match karta hai. Space ke baad dobara search nahi karta.

- Isliye output Python aaya, Python 123 nahi.

=============================================================================

Example 2: r"Python" kya match kar raha hai ?
---------------------------------------------

text   = "123 Python"
result = re.match(r"Python", text)
print(result)

Output:
-------
None

- Yahan r"Python" ka matlab hai ki Regex ko shuruaat mein 
  exact Python word chahiye.

* Lekin string ki shuruaat hai:

123 Python
^^^

- Pehle 1 hai, P nahi. Isliye match fail ho jaata hai aur 
  None milta hai.

Agar tum ye likho:
------------------
result = re.match(r"\d+", "123 Python")
print(result.group())

Output:
-------
123

* Kyunki ab pattern \d+ hai, aur string ki shuruaat mein 
  123 digits hain.

=============================================================================

Ek line mein difference yaad rakho:
-----------------------------------

Code	                               Kya match hoga ?
--------------------------------------------------------
re.match(r"\w+", "Python 123")	       Python
--------------------------------------------------------
re.match(r"Python", "Python 123")	   Python
--------------------------------------------------------
re.match(r"Python", "123 Python")	   None
--------------------------------------------------------
re.match(r"\d+", "123 Python")	       123
--------------------------------------------------------

* Golden rule : re.match() string ki shuruaat se check karta hai. 
                Pattern batata hai ki wahan kis tarah ke characters
                hone chahiye.

* Agar tum chahte ho ki Python poori string mein kahin bhi Python 
  dhoondhe, toh re.search(r"Python", "123 Python") use karo. Iska 
  result Python ko match karega.