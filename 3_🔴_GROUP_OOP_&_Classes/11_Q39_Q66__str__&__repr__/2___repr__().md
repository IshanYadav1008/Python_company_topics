Python mein __repr__()
----------------------

* __repr__() Python ka ek special method hai, jiska use object ki 
  developer-oriented representation dene ke liye hota hai.

* Simple words mein: Jab developer kisi object ko inspect karna chahta 
                     hai, toh __repr__() object ke baare mein useful 
                     aur unambiguous information dene mein help karta 
                     hai.

=================================================================================

1. __repr__() ke bina kya hota hai ?

CODE:
-----
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

s1 = Student("Rahul", 20)
print(repr(s1))

Output kuch aisa hoga:
----------------------
<__main__.Student object at 0x...>

* Ye default representation hai. Isse object ki actual details 
  aasani se nahi dikhti.

=================================================================================

2. Ab __repr__() use karte hain:

CODE:
-----
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __repr__(self):
        return f"Student(name={self.name!r}, age={self.age!r})"

s1 = Student("Rahul", 20)
print(repr(s1))

Output:
-------
Student(name='Rahul', age=20)

* Ab representation se developer ko object ki values clearly samajh 
  aa rahi hain.

* Yahan !r ka matlab hai ki value ko repr() ke through represent 
  karo. Isliye string "Rahul" quotes ke saath dikh rahi hai.

=================================================================================

3. __repr__() automatically kab call hota hai ?

* Tum repr(object) call kar sakte ho. Python ise kuch doosri situations 
  mein bhi use karta hai.

CODE:
-----
class Student:
    def __init__(self, name):
        self.name = name

    def __repr__(self):
        return f"Student(name={self.name!r})"

s1 = Student("Rahul")
s2 = Student("Priya")
print(repr(s1))
students = [s1, s2]
print(students)

Output:
-------
Student(name='Rahul')
[Student(name='Rahul'), Student(name='Priya')]

* Dhyan do: List ko print karne par bhi Python uske objects ki 
            representation ke liye __repr__() use karta hai.

=================================================================================

4. __str__() aur __repr__() mein difference:

CODE:
-----
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name}, age {self.age}"

    def __repr__(self):
        return f"Student(name={self.name!r}, age={self.age!r})"

s1 = Student("Rahul", 20)
print(str(s1))
print(repr(s1))

Output:
-------
Rahul, age 20
Student(name='Rahul', age=20)

---------------------------------------------------------------------------------

# Ab difference dekho:

Method       | Main purpose
-------------|-----------------------------------------------
__str__()    | User-friendly, readable representation
__repr__()   | Developer-friendly, informative representation
str(obj)     | Object ki string representation leta hai
repr(obj)    | Object ki representation leta hai

=================================================================================

5. Kya __repr__() se object dobara bana sakte hain ?

* Kabhi-kabhi, haan. Agar __repr__() aisi valid Python expression return 
  kare jo object ko dobara bana sake, toh us representation ko dobara 
  evaluate kiya ja sakta hai.

* Lekin har __repr__() ka aisa hona compulsory nahi hai. Uska main goal 
  useful, unambiguous representation dena hai.

Yaad rakhna
-----------
- __str__() — user ke liye readable text.
- __repr__() — developer ke liye informative representation.
- Agar class mein __str__() define nahi hai, toh str(obj) aam taur 
  par __repr__() ka fallback use karta hai, agar woh define ho.
- Agar dono define nahi hain, toh Python default representation deta hai.