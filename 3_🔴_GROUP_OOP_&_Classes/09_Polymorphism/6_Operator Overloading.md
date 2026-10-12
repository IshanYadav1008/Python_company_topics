# Operator Overloading kya hoti hai ?

* Operator Overloading ka matlab hai ek hi operator ka alag-alag 
  data types ke saath alag kaam karna.

* Pehle samjho, operators kya hote hain: +, -, *, / etc.

--> Inmein se + operator ka example dekhte hain.

=================================================================================

1. + operator numbers ke saath:
-------------------------------

a = 10
b = 20
print(a + b)

Output:
-------
30

// Yahan + ka kaam numbers ko add karna hai.

=================================================================================

2. + operator strings ke saath:
-------------------------------

a = "Hello"
b = "World"
print(a + b)

Output:
-------
HelloWorld

* Yahan + ka kaam strings ko jodna hai. Is process ko concatenation 
  kehte hain.

=================================================================================

3. + operator lists ke saath:
-----------------------------

a = [1, 2]
b = [3, 4]
print(a + b)

Output:
-------
[1, 2, 3, 4]

* Yahan + dono lists ke items ko jod kar ek nayi list banata hai.

=================================================================================

# Teeno examples mein kya difference hai?

Data Type | Code              | + Operator ka Kaam
----------|-------------------|---------------------------
Numbers   | 10 + 20           | Addition: 30
Strings   | "Hello" + "World" | Concatenation: HelloWorld
Lists     | [1, 2] + [3, 4]   | Lists ko jodna

Dhyan do: Har baar operator + hi hai, lekin uska kaam data type ke 
          hisaab se badal raha hai. Ye Polymorphism se related hai.

=================================================================================
---------------------------------------------------------------------------------
=================================================================================

# Python mein Operator Overloading kaise hoti hai ?

* Python mein operators ke behavior ko special methods ke through 
  define kiya ja sakta hai. Jaise + operator ke liye __add__() 
  method use hota hai.

Example:
--------
class Number:
    def __init__(self, value):
        self.value = value

    def __add__(self, other):
        return self.value + other.value

a = Number(10)
b = Number(20)
print(a + b)

Output:
-------
30

---------------------------------------------------------------------------------

* Yahan humne apni class Number ke liye define kiya ki jab do Number 
  objects ko + se joda jaye, toh unki value add ho.

* Important difference: Built-in types jaise int, str aur list ke liye
  + ka behavior Python mein pehle se defined hai. Apni classes ke liye 
  hum __add__() jaise special methods define karke operator ka behavior 
  customize kar sakte hain.

* Yaad rakho: Operator Overloading mein ek hi operator ko alag types ya 
              apni classes ke objects ke liye alag behavior diya ja sakta 
              hai.

=================================================================================
---------------------------------------------------------------------------------
=================================================================================

Q) Tumhara question bilkul sahi hai. Tumne __init__() ka kaam sahi samjha hai. 
   Confusion bas ye hai ki other.value mein 20 kaise aa raha hai, jabki 
   __init__() dono objects ke liye alag-alag chalta hai ? 

---------------------------------------------------------------------------------

ANS) Chalo step-by-step samajhte hain:

1. Sabse pehle dono objects bante hain

a = Number(10)
b = Number(20)

Jab a = Number(10) chalta hai:
------------------------------
- __init__() call hota hai.
- self ko object a refer karta hai.
- value = 10 hota hai.
- Isliye a.value = 10 ho jata hai.

Jab b = Number(20) chalta hai:
------------------------------
- __init__() dobara call hota hai.
- self ko object b refer karta hai.
- value = 20 hota hai.
- Isliye b.value = 20 ho jata hai.

---------------------------------------------------------------------------------

* Ab dono objects ke paas apni-apni value hai.

Object a --> a.value --> 10
Object b --> b.value --> 20

=================================================================================

2. Ab print(a + b) chalta hai:

* Yahan important baat hai: jab Python a + b dekhta hai, toh woh a object 
                            ke __add__() method ko call karta hai aur b 
                            object ko argument ke roop mein pass karta hai.

Conceptually, ise aise samjho:
------------------------------
=> a.__add__(b)

---------------------------------------------------------------------------------

* Ab ye method chalta hai:

def __add__(self, other):
    return self.value + other.value

---------------------------------------------------------------------------------

Is call mein:
-------------
- self → object a hai.
- other → object b hai.

Isliye:
-------------
- self.value → a.value → 10
- other.value → b.value → 20

Calculation:
------------
=> return 10 + 20

Output:
-------
30

=================================================================================

3. Sabse important difference:

Variable | Kis object ko refer karta hai | value
---------|-------------------------------|------
self     | Object a                      | 10
other    | Object b                      | 20

* Tum sahi keh rahe ho ki __init__() dono objects ko initialize karta hai. 
  Lekin other ka kaam initialization karna nahi hai.

* __init__() object ki value set karta hai, aur __add__() ko call karte waqt 
  Python decide karta hai ki self aur other kis object ko refer karenge.

* Ek line mein yaad rakho: a + b mein a pehla object hai, isliye self; aur 
  b doosra object hai, isliye other.