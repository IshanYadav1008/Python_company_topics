* Context manager banane ke liye class mein __enter__() aur __exit__() 
  methods likhte hain.

CODE:
-----
class MyContext:
    def __enter__(self):
        print("Start")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("End")
        return False

with MyContext() as obj:
    print("Working")

Output:
-------
Start
Working
End

* __enter__()  — with block shuru hone par chalta hai.

* return self  — object ko obj variable mein deta hai.

* __exit__()   — block khatam hone par chalta hai, chahe 
                 error aaye ya na aaye.

* return False — agar error aaya, toh use suppress nahi 
                 karega; error aage propagate hoga.

===============================================================================

Haan, meri wording galat thi. Context manager ek mechanism hai, aur 
MyContext class us mechanism ko implement karne ka tareeka hai. Dono 
ko mix karke samjhaya, isliye confusion hua.

- Chalo, simple example se samajhte hain.

1. Pehle context manager ke bina:
---------------------------------
print("Kaam shuru")
print("Kaam ho raha hai")
print("Kaam khatam")

- Yahan teeno lines normal order mein chalti hain.

- Ab maan lo tum chahte ho ki Python khud kaam shuru hone aur khatam 
  hone par specific methods chalaye. Iske liye context manager use 
  kar sakte ho

===============================================================================

2. Context manager banate kaise hain ?
--------------------------------------

class MyContext:
    def __enter__(self):
        print("Kaam shuru")

    def __exit__(self, *args):
        print("Kaam khatam")

* Abhi humne sirf MyContext naam ki class define ki hai. 
  Iske andar do methods likhe hain:

- __enter__() — kaam shuru hone par kya karna hai.
- __exit__() — kaam khatam hone par kya karna hai.

--> Sirf class define karne se ye methods nahi chalte.

===============================================================================

3. Ab ise chalate kaise hain ?

with MyContext():
    print("Main kaam kar raha hoon")

Output:
-------
Kaam shuru
Main kaam kar raha hoon
Kaam khatam

Ab dhyan se:
------------
1. with Python ko batata hai ki is block ko context manager ke 
   rules ke according chalana hai.

2. MyContext() class ka ek object banata hai. Object class se 
   banta hai; context manager mechanism ka object nahi banta.

3. Python us object ke __enter__() method ko call karta hai.

4. Phir block ke andar ka code chalta hai.

5. Block khatam hone par Python __exit__() call karta hai.

===============================================================================

4. Toh self kya hai ?

Is example mein:
----------------
class MyContext:
    def __enter__(self):
        print("Kaam shuru")

- self us particular object ko refer karta hai jis par method 
  chal raha hai.

Jaise:
------
class MyContext:
    def hello(self):
        print("Hello")

x = MyContext()
x.hello()

* Yahan x ek object hai. Jab x.hello() chalta hai, Python us object 
  ko method ke andar self ke naam se available karata hai.

Bas yaad rakho:
---------------
- MyContext                  = class

- MyContext()                = class se bana object

- with                       = context manager mechanism ko use karne 
                               ka tareeka

- self                       = method ke andar us object ko refer karne  
                               wala naam

- __enter__() aur __exit__() = woh methods jinhe with sahi waqt par call 
                               karta hai
 

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Doubt:
------
Bhai, tera main doubt ye hai: __enter__() aur __exit__() ka class se 
relation banta kaise hai, aur Python ko kaise pata chalta hai ki inhe 
kab chalana hai? Pehle ye clear karte hain, phir poora code dry run 
karenge.

-------------------------------------------------------------------------------

1. __enter__() aur __exit__() ka class se relation kaise hai?

Maan le tum apni class banate ho:
---------------------------------
class Add:
    def calculate(self):
        print(2 + 3)

- Yahan calculate() method Add class ke andar define hai. Isliye woh 
  Add class ka method hai.

-------------------------------------------------------------------------------

Bilkul isi tarah:
-----------------
class MyContext:
    def __enter__(self):
        print("Start")

    def __exit__(self, exc_type, exc_value, traceback):
        print("End")

- __enter__() aur __exit__() bhi MyContext class ke andar define hain. 
  Isliye ye us class ke methods hain.

-------------------------------------------------------------------------------

Ab important sawaal: Python ko kaise pata chalta hai ki in dono methods 
                     ko kab chalana hai?

* Iska jawab hai: with statement ke special rules ki wajah se.

- Python mein __enter__ aur __exit__ special methods hain. Jab with ko 
  kisi object ke saath use karte ho, Python in methods ko automatically 
  call karta hai.

- Jaise Add class ke calculate() method ko Python apne aap nahi chalata, 
  waise hi MyContext ke __enter__() ko bhi sirf class define karne se 
  nahi chalata.

-------------------------------------------------------------------------------

# Difference dekho:

x = Add()
x.calculate()        # Hum khud method call kar rahe hain

with MyContext():    # with enter aur exit ko call karwata hai
    print("Working")

* Ab ye relation clear hua : class methods rakhti hai, aur with unmein 
                             se special methods ko sahi waqt par call 
                             karta hai.

===============================================================================

2. Ab poore code ko samjho:
---------------------------

class MyContext:
    def __enter__(self):
        print("Start")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("End")
        return False

with MyContext() as obj:
    print("Working")

-------------------------------------------------------------------------------

Step 1: Class define hoti hai:
-----------------------------
=> class MyContext:

* Python class banata hai. Ab us class mein do methods defined 
  hain:

- __enter__()
- __exit__()

. Abhi inke andar ka code nahi chala.

-------------------------------------------------------------------------------

Step 2: MyContext() kya karta hai ?
-----------------------------------
=> with MyContext() as obj:

- MyContext class ka naam hai. () lagane se us class ka ek object 
  banta hai.

* Samajhne ke liye maan lo Python ne object banaya aur hum use O1 
  naam de rahe hain. O1 sirf samjhane ke liye naam hai; code mein 
  tumne ye naam nahi likha.

-------------------------------------------------------------------------------

Step 3: with __enter__() chalata hai:
-------------------------------------

* Python ab O1 object ke __enter__() method ko call karta hai.

def __enter__(self):
    print("Start")
    return self

Yahan:
------
- self ka matlab hai woh O1 object jis par method call hua.
- print("Start") se Start print hota hai.
- return self se wahi O1 object wapas milta hai.

* Dhyan do: MyContext dobara execute nahi hoti. Class pehle hi 
            define ho chuki thi. Ab us class se bane object ka 
            method chal raha hai.

-------------------------------------------------------------------------------

Step 4: as obj ka kya matlab hai ?
----------------------------------

* as obj ka matlab hai: __enter__() ne jo value return ki, use 
  obj naam ke variable mein rakh do.

* Hamare code mein return self hai. Aur self mein O1 object hai.

Isliye:
-------
with MyContext() as obj:

- ke baad obj usi O1 object ko refer karta hai.

- Agar __enter__() mein return 100 likha hota, toh obj ki value 
  100 hoti.

-------------------------------------------------------------------------------

Step 5: Ab Working kaise print hota hai ?
-----------------------------------------

* __enter__() complete ho gaya. Ab Python with block ke andar 
  aata hai:

=> print("Working")

- Output mein Working print hota hai.

-------------------------------------------------------------------------------

Step 6: __exit__() apne aap kaise chalta hai ? 
----------------------------------------------

* Jaise hi with block khatam hota hai, Python context manager ke 
  rules ke mutabik __exit__() call karta hai.

def __exit__(self, exc_type, exc_value, traceback):
    print("End")
    return False

- self wahi O1 object hai.

- exc_type, exc_value, traceback error hone par uski details 
  dete hain.

- print("End") se End print hota hai.

- return False ka matlab hai agar block mein exception aaye, 
  toh use suppress mat karo.

===============================================================================

3. Poora flow ek jagah:
-----------------------

Class define hoti hai
MyContext ke methods ready hain
        |
        |
MyContext()
Ek object banta hai: O1
        |
        |
__enter__()
Start print, self return
        |
        |
as obj
obj ko returned object milta hai
        |
        |
With block
Working print hota hai
        |
        |
__exit__()
End print hota hai

Final output:
-------------
Start
Working
End

-------------------------------------------------------------------------------

* Sabse zaroori baat: MyContext class ka naam hai; MyContext() us class ka 
                      object banata hai; with us object ke __enter__() aur 
                      __exit__() ko call karta hai. as obj mein __enter__() 
                      ki returned value aati hai. return self wahi object 
                      wapas deta hai.

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Doubt:
------
Bhai, tere doubt ka main point hai: return self karke object ko obj mein 
lene ki zaroorat hi kyun hai? Aur uske baad Working print hone ke baad 
__exit__() kaise chalta hai ?

- Chalo, ek example se samajhte hain.

-------------------------------------------------------------------------------

1. Pehle return self hata kar dekho:
------------------------------------
class MyContext:
    def __enter__(self):
        print("Start")

    def __exit__(self, exc_type, exc_value, traceback):
        print("End")

with MyContext() as obj:
    print("Working")
    print(obj)

Output:
-------
Start
Working
None
End

- obj ki value None hai, kyunki __enter__() ne kuch return nahi kiya.

- Lekin dhyan do: Working aur End phir bhi chal gaye!

- Isse ek important baat pata chali: return self likhna __exit__() chalane 
                                     ke liye zaroori nahi hai. with khud 
                                     block khatam hone par __exit__() 
                                     chalata hai.

===============================================================================

2. Phir return self kyun likhte hain ?

Ab ye code dekho:
-----------------
class MyContext:
    def __enter__(self):
        print("Start")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("End")

with MyContext() as obj:
    print("Working")
    print(obj)

* Ab obj mein None ki jagah MyContext ka object aayega.

Kyun ?
------
- self current object ko refer karta hai.
- return self wahi object wapas deta hai.
- as obj us returned object ko obj mein rakh deta hai.

- Iska faayda tab hai jab tum with ke andar us object ke 
  methods ya data use karna chahte ho.

-------------------------------------------------------------------------------

Example jahan iska actual use hai:
----------------------------------
class MyContext:
    def __enter__(self):
        self.name = "Rahul"
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("Kaam khatam")

with MyContext() as obj:
    print(obj.name)

Output:
-------
Rahul
Kaam khatam

- Yahan return self ki wajah se obj usi object ko refer karta hai 
  jisme name = "Rahul" store hai. Isliye obj.name access kar paate 
  hain.

- Agar return self hata doge, toh obj ki value None hogi aur obj.name 
  par error aayega.

===============================================================================

3. Working ke baad __exit__() wapas kaise chalta hai ?

* Iske liye return self responsible nahi hai. Ye with ka rule 
  hai.

* Python internally roughly is tarah ka flow follow karta hai:

1. Object banao.
2. __enter__() call karo.
3. Uski returned value obj mein rakho.
4. with block ke andar ka code chalao.
5. Block se bahar nikalte waqt __exit__() call karo.

* Chahe block normally khatam ho ya uske andar exception aaye, 
  __exit__() call hota hai. Exception ko suppress karna hai ya 
  nahi, woh __exit__() ke return par depend karta hai.

Bas ye difference yaad rakho:
-----------------------------
- return self → with ke andar obj ko context manager ka object dene ke liye.
- __exit__()  → with block se bahar nikalte waqt cleanup karne ke liye.
- with        → __enter__() aur __exit__() ko sahi waqt par chalane ke liye.

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Doubt:
------
tmne bola....

return self → with ke andar obj ko context manager ka object dene ke liye.

ye context manager ka object kya hai ?

-------------------------------------------------------------------------------

* Bhai, simple baat: context manager ka object matlab woh object jo humne 
                     apni class se banaya hai aur jise with mein use kar 
                     rahe hain.
                    
===============================================================================

Example:
--------
class MyContext:
    def __enter__(self):
        print("Start")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("End")

with MyContext() as obj:
    print("Working")

Ab dekho:
---------
1. MyContext   — hamari banayi hui class hai.

2. MyContext() — us class se ek object banata hai.

3. with us object ko use karke __enter__() aur __exit__() chalata 
   hai. Isliye woh context manager ka object hai.

4. self usi object ko refer karta hai.

5. return self us object ko return karta hai, aur as obj us returned 
   object ko obj mein rakhta hai.

-------------------------------------------------------------------------------

# Aise samjho:

MyContext
Class
   |
MyContext()
Object banta hai
   |
return self
Wahi object return hota hai
   |
obj
Usi object ko refer karta hai

* Ek zaroori baat: return self likhna har context manager mein zaroori nahi 
                   hai. Agar with ke andar object ko obj ke through use karna 
                   hai, tab us object ko return karna useful hota hai.