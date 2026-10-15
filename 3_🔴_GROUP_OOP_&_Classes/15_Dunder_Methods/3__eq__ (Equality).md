* Isme sabse important cheez ye samajhna hai ki == likhne par Python 
  kya karta hai aur __eq__() ko kaun call karta hai.

1. __eq__ hota kya hai ?

* __eq__ Python ka ek special Dunder Method hai jo define karta hai 
  ki do objects ko == se compare karne par unhe equal maana jaana 
  chahiye ya nahi.

Jaise normal Python mein:
-------------------------
a = 10
b = 10
print(a == b)

Output:
-------
True

* Kyunki dono numbers ki value 10 hai.

---------------------------------------------------------------------------------

Ek aur example:
---------------
a = 10
b = 20
print(a == b)

Output:
-------
False

* Yahan Python ko numbers compare karna pehle se aata hai.

* Lekin jab hum apni khud ki class banate hain, toh Python ko 
  hamesha ye nahi pata hota ki hamare objects ko kis basis par 
  equal maana jaana chahiye. Isliye hum __eq__ define kar sakte 
  hain.

=================================================================================

2. Ek simple example lete hain:

* Maan lo hum students ki class banate hain:

CODE:
-----
class Student:
    def __init__(self, name):
        self.name = name

s1 = Student("Rahul")
s2 = Student("Rahul")
print(s1 == s2)

- Ab tum kya sochoge? Dono students ka naam Rahul hai, toh output 
  True aana chahiye.

- Lekin is code mein aam taur par output False aayega.

- Kyun? Kyunki humne abhi Python ko bataya hi nahi ki do Student 
  objects ko kis basis par equal maana jaye. Default behavior 
  mein ye alag-alag objects equal nahi maane jaate.

---------------------------------------------------------------------------------

Dhyan do: s1 aur s2 do alag objects hain, bhale hi unka name same ho.

     Object s1                               Object s2 
     name = "Rahul"                          name = "Rahul"
            |                                |
            |                                |
          Naam same hai, lekin objects alag hain.
          s1 == s2 → default behavior mein False

=================================================================================

3. Ab __eq__ se apna rule banate hain:

Hum Python ko batayenge:
------------------------
- Do students equal tab maane jayenge, jab unka naam same ho.

Code dekho:
-----------
class Student:
    def __init__(self, name):
        self.name = name

    def __eq__(self, other):
        return self.name == other.name

s1 = Student("Rahul")
s2 = Student("Rahul")
print(s1 == s2)

Output:
-------
True

* Ab samjhte hain ki andar kya hua.

---------------------------------------------------------------------------------

Step 1: Do objects bante hain:
------------------------------
s1 = Student("Rahul")
s2 = Student("Rahul")

- s1 ek Student object ko refer karta hai.
- s2 doosre Student object ko refer karta hai.
- Dono objects ka name "Rahul" hai.

---------------------------------------------------------------------------------

Step 2: Tum comparison karte ho:
--------------------------------
print(s1 == s2)

- Python s1 aur s2 ko == se compare karta hai. Iske liye woh 
  __eq__() method ko use karta hai.

* Conceptually, is call ko aise samajh sakte ho:

s1.__eq__(s2)

Yahan:
------
- self  → s1 object
- other → s2 object

---------------------------------------------------------------------------------

Step 3: Method ke andar comparison hota hai:
--------------------------------------------
=> return self.name == other.name

- Ab ise values ke saath dekho:
=> return "Rahul" == "Rahul"

. Dono strings same hain, isliye result True aata hai.

---------------------------------------------------------------------------------

Step 4: Result wapas milta hai:
-------------------------------

* __eq__() True return karta hai. Phir print() us result ko 
  screen par dikha deta hai.

=================================================================================

4. Poora flow diagram:
----------------------

Tum likhte ho
print(s1 == s2)
      |
Python __eq__() ko use karta hai
s1.__eq__(s2)
      |
Method ka rule
self.name == other.name
      |
Result: True
Phir print() result dikhata hai.

=================================================================================

5. self aur other ka matlab:

* Ye point bahut important hai:

def __eq__(self, other):    
return self.name == other.name

Jab tum likhte ho:
------------------
s1 == s2


Toh method ke andar:
--------------------

Method ka naam	               Kya refer karta hai?
-----------------------------------------------------
self	                       s1 object
other	                       s2 object
self.name	                   s1.name, yaani "Rahul"
other.name	                   s2.name, yaani "Rahul"
-----------------------------------------------------

---------------------------------------------------------------------------------

# Copy karne ke liye:

s1 == s2
    |
    v
s1.__eq__(s2)
    |
    +-- self  = s1
    +-- other = s2
    |
    v
self.name == other.name
    |
    v
"Rahul" == "Rahul"
    |
    v
True

* Ye ek conceptual explanation hai. Python comparison ke liye 
  special-method dispatch ke additional rules bhi follow karta 
  hai, lekin abhi ke example mein ye samajhna kaafi hai.

=================================================================================

6. Ek aur example: alag naam:

s1 = Student("Rahul")
s2 = Student("Amit")
print(s1 == s2)

Output:
-------
False

* Kyunki method ke andar comparison banega:
"Rahul" == "Amit"

* Dono naam alag hain, isliye False return hoga.

Comparison	                            Result
----------------------------------------------
Student("Rahul") == Student("Rahul")	True
Student("Rahul") == Student("Amit")	    False
----------------------------------------------

* Ye result hamare banaye hue rule ki wajah se hai: students 
  ke naam same honge, tabhi woh equal honge.

=================================================================================

7. Ek zaroori baat: == aur is alag hain:

In dono ko mix mat karna.
-------------------------
- == poochta hai  : Kya ye dono equal hain, hamare equality rules 
                    ke hisaab se ?

- is poochta hai  : Kya ye dono references bilkul usi ek object ko 
                    point karte hain?

Example:
--------
s1 = Student("Rahul")
s2 = Student("Rahul")

print(s1 == s2)  # True
print(s1 is s2)  # False

- == True hai kyunki humne naam compare karne ka rule banaya hai. 
  is False hai kyunki s1 aur s2 alag objects ko refer karte hain.

=================================================================================

8. Ab tum khud try karo:

* Maan lo hamari Student class mein __eq__ method naam compare karta 
  hai.

s1 = Student("Rahul")
s2 = Student("Amit")
print(s1 == s2)

Bilkul sahi!
------------
"Rahul" == "Amit" ka result False hai. Isi result ko __eq__() return 
 karega.

* Ek line mein yaad rakho : __eq__ tumhari class ke objects ke liye == ka behavior 
                            define karta hai. Tum decide karte ho ki objects ko 
                            equal maanne ke liye kaunsi values compare honi chahiye.