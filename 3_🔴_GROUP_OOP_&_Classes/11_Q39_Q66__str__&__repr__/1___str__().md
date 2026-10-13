Python mein __str__()
---------------------

* __str__() Python ka ek special method hai, jiska use kisi object ko 
  readable aur user-friendly string mein represent karne ke liye hota 
  hai.

* Simple words mein: Jab tum apne class ke object ko print() karte ho, 
                     toh __str__() define karke decide kar sakte ho ki 
                     object screen par kaise dikhna chahiye.

================================================================================

1. __str__() ke bina kya hota hai ?

CODE:
-----
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

s1 = Student("Rahul", 20)
print(s1)

Output kuch aisa hoga:
----------------------
<__main__.Student object at 0x...>

* Yahan Python object ki default representation dikha raha hai. 
  Isse student ka naam aur age directly pata nahi chalta.

================================================================================

2. Ab __str__() use karte hain:

CODE:
-----
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"Name: {self.name}, Age: {self.age}"

s1 = Student("Rahul", 20)
print(s1)

Output:
-------
Name: Rahul, Age: 20

* Ab object print karne par humein readable information milti hai.

================================================================================

3. Ye kaise kaam karta hai ?

Jab tum likhte ho:
------------------
=> print(s1)

* Python internally object ki string representation nikalne ke liye 
  str(s1) call karta hai, jo s1.__str__() ko use karta hai.

Isliye ye dono conceptually same result denge:
----------------------------------------------
=> print(s1)
=> print(str(s1))

Dono ka output:
---------------
Name: Rahul, Age: 20

* Dhyan do: __str__() method ko string return karni chahiye, print() 
  nahi karna chahiye.

--------------------------------------------------------------------------------

Galat example:
--------------
def __str__(self):
    print(self.name)

--------------------------------------------------------------------------------

Sahi example:
-------------
def __str__(self):
    return self.name

================================================================================

4. Kya __str__() khud call karna padta hai ?

* Nahi. Aam taur par tum print(object) ya str(object) use karte ho, 
  aur Python __str__() ko automatically call karta hai.

CODE:
-----
class Mobile:
    def __init__(self, brand):
        self.brand = brand

    def __str__(self):
        return f"Mobile brand: {self.brand}"

m1 = Mobile("Samsung")
print(m1)
print(str(m1))
print(type(m1))
print(type(str(m1)))

Output:
-------
Mobile brand: Samsung
Mobile brand: Samsung
<class '__main__.Mobile'>
<class 'str'>WW

================================================================================

5. __str__() ke baare mein important points:

- Ye Python ka special method hai, jise dunder method bhi kehte hain.
- Iska naam double underscore se shuru aur khatam hota hai.
- Iska use object ko readable string mein dikhane ke liye hota hai.
- print(object) aur str(object) ise automatically use karte hain.
- Is method ko string return karni chahiye.

Ek line mein yaad rakho : __str__() decide karta hai ki object ko 
                          user-friendly text ke roop mein kaise 
                          dikhaya jaye.