Chalo, ab __str__() vs __repr__() ko simple example se samajhte hain.

1. Dono mein difference kya hai ?
---------------------------------
- __str__()  — Object ko insaan ke liye readable aur simple form mein 
               dikhata hai.

- __repr__() — Object ki informative representation dikhata hai, jo 
               debugging mein useful hoti hai.

================================================================================

2. Example:
-----------

class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"My name is {self.name}"

    def __repr__(self):
        return f"Student(name={self.name!r}, age={self.age!r})"

s1 = Student("Rahul", 20)

print(s1)
print(str(s1))
print(repr(s1))
print([s1])

Output:
-------
My name is Rahul
My name is Rahul
Student(name='Rahul', age=20)
[Student(name='Rahul', age=20)]

Samjho kya hua:
---------------
1. print(s1)   → __str__() call hua.
2. str(s1)     → __str__() call hua.
3. repr(s1)    → __repr__() call hua.
4. print([s1]) → List ke andar object hai, isliye uski __repr__() 
                 representation use hui.

================================================================================

3. Quick comparison:

__str__()   -> User-friendly representation
__repr__()  -> Developer-friendly representation

print(obj)  -> Pehle __str__()
str(obj)    -> Pehle __str__()
repr(obj)   -> __repr__()
[obj]       -> Andar ke object ke liye __repr__()

* Agar __str__() define nahi hai, to str(obj) zaroorat padne par __repr__() 
  ka use kar sakta hai. Lekin repr(obj) __str__() par fallback nahi karta.

* Yaad rakhne ka easy tareeka: __str__() user ko dikhane ke liye, aur 
  __repr__() developer ko object samajhne aur debug karne ke liye.

================================================================================
--------------------------------------------------------------------------------
================================================================================

Doubt:
------
tmne bola tha ki repr(obj) __str__() par fallback nahi karta.

lekin iska output 
-----------------
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name}, age {self.age}"

s1 = Student("Rahul", 20)

print(repr(s1))
print(type(repr(s1)))

aise aa rha hai:
----------------
<__main__.Student object at 0x7fcd80d92510>
<class 'str'>

================================================================================

* Tumhara output actually meri baat ko hi confirm karta hai. Bas ek 
  important difference samjho.

* Tumhari class mein __str__() defined hai, lekin __repr__() defined 
  nahi hai.

CODE:
-----
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"{self.name}, age {self.age}"

s1 = Student("Rahul", 20)
print(repr(s1))
print(type(repr(s1)))

Output:
-------
<__main__.Student object at 0x7fcd80d92510>
<class 'str'>

--------------------------------------------------------------------------------

Aisa kyun hua ?
---------------
1. repr(s1) ko __repr__() use karna hota hai.

2. Tumne __repr__() define nahi kiya, isliye Python default 
   __repr__() use karta hai.

3. Python __str__() ko fallback ke roop mein use nahi karta.

4. repr(s1) ka result string hota hai, isliye type(repr(s1)) 
   ka output <class 'str'> hai.

--------------------------------------------------------------------------------

Ab ye example dekho:
--------------------
print(str(s1))
print(repr(s1))

Output:
-------
Rahul, age 20
<__main__.Student object at 0x7fcd80d92510>

* Yahan str(s1) tumhara __str__() use karta hai, jabki repr(s1) 
  default __repr__() use karta hai.

--------------------------------------------------------------------------------

Ek line mein yaad rakho:
------------------------
- str() ko __str__() na mile, to woh __repr__() par fallback kar sakta hai.

- repr() ko __repr__() na mile, to woh default representation use karta hai;
  __str__() par fallback nahi karta.