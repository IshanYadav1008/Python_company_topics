1. Singleton Pattern kya hota hai ?
-----------------------------------

* Singleton Pattern ek aisa design pattern hai jiska purpose kisi 
  class ka sirf ek hi object maintain karna hota hai.

* Normal class mein tum jitne chaaho objects bana sakte ho. Lekin 
  Singleton Pattern mein baar-baar object banane par bhi same 
  object return karne ki koshish ki jaati hai.

==========================================================================

2. Normal class ka example:
---------------------------

class Student:
    pass

s1 = Student()
s2 = Student()

print(s1 is s2)

Output:
------
False

* Kyunki s1 aur s2 do alag objects hain.

==========================================================================

3. Singleton Pattern ka example:
--------------------------------

class Database:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)

        return cls._instance

d1 = Database()
d2 = Database()
print(d1 is d2)

Output:
-------
True

* Kyunki d1 aur d2 dono same object ko refer karte hain.

==========================================================================

4. Is code mein kya ho raha hai ?

- __new__() — Object create karne ka kaam karta hai.

- cls._instance = None — Shuru mein koi object store nahi hai.

- if cls._instance is None: — Check karta hai ki object pehle 
  se bana hai ya nahi.

- super().__new__(cls) — Pehli baar object create karta hai.

- return cls._instance — Har baar wahi stored object return 
  karta hai.

==========================================================================

5. Singleton ki zaroorat kyun hoti hai ?

* Maan lo tumhari application mein ek shared configuration object 
  chahiye. Tum chahte ho ki application ke alag-alag parts usi 
  object ko use karein, na ki har baar naya object banayein.

* Singleton is tarah ke use case mein useful ho sakta hai.

Ek important baat: Python mein Singleton hamesha zaroori nahi 
                   hota. Kabhi-kabhi ek normal shared object 
                   ko alag-alag jagah pass karna zyada simple 
                   aur behtar hota hai.

==========================================================================
--------------------------------------------------------------------------
==========================================================================

* Chalo, ab Singleton Pattern ko bilkul zero se dobara samajhte hain. Is 
  baar tumhare saare doubts ko ek-ek karke cover karenge — Singleton kya
  hai, kyun chahiye, __new__() kya karta hai, super().__new__(cls) kyun 
  likhte hain, cls._instance kya rakhta hai, aur d1 is d2 True kyun hota 
  hai.

--------------------------------------------------------------------------

1. Sabse pehle: normal class kya karti hai ?

* Maan lo hum ek Database class banate hain.

CODE:
-----
class Database:
    pass

d1 = Database()
d2 = Database()
print(d1 is d2)

Output:
-------
False

--------------------------------------------------------------------------

Aisa kyun ?
---------
* Jab bhi hum Database() likhte hain, Python ek naya object 
  banata hai.

d1 = Database()  --> Object A
d2 = Database()  --> Object B

. Object A aur Object B alag hain, isliye d1 is d2 False hai.

. Yahan "is" check karta hai ki dono variables ek hi object 
  ko refer kar rahe hain ya nahi.

==========================================================================

2. Ab Singleton ki zaroorat kyun padi ?

* Ab socho ki hum chahte hain ki Database class se chahe kitni baar 
  object maango, sirf ek hi object bane aur har baar wahi object 
  mile.

* Jaise ek application mein sab jagah same configuration object use 
  karna ho.

Normal class mein:
------------------
d1 = Database()
d2 = Database()
d3 = Database()

--> Teen alag objects ban sakte hain.

--------------------------------------------------------------------------

* Lekin Singleton mein hum chahte hain:

d1 ──┐
d2 ──┼──> Ek hi Object A
d3 ──┘

--> Isi technique ko Singleton Pattern kehte hain.

* Yaad rakho: Singleton ka matlab hai class se uski ek hi shared 
  instance banaye rakhna. Har situation mein Singleton use karna 
  zaroori nahi hota.

==========================================================================

3. Singleton ka code dekho:

CODE:
-----
class Database:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)

        return cls._instance

d1 = Database()
d2 = Database()
print(d1 is d2)

Output:
-------
True

* Ab is code ki har important line ka matlab samajhte hain.

==========================================================================

4. _instance = None ka kya matlab hai ?

_instance = None

* Ye class variable hai. Hum ise pehle object ka reference save 
  karne ke liye use kar rahe hain.

* None ka matlab hai ki abhi is variable mein koi object save 
  nahi hai. 

--------------------------------------------------------------------------

Shuru mein:
-----------
_instance = None

* Jab pehla object banega, toh uska reference yahan save ho jayega:

_instance ──> Object A

--> Naam ke aage _ lagana Python mein ek convention hai jo batata 
    hai ki ye variable class ke internal use ke liye hai. Ye apne 
    aap variable ko private nahi banata.

==========================================================================

5. __new__(cls) kyun likha ?

=> def __new__(cls):

* Isko samajhne ke liye object banne ka process dekho.

Jab tum likhte ho:
------------------
=> d1 = Database()

Python internally ye kaam karta hai:
------------------------------------
1. __new__() se object banwata hai.
2. Uske baad __init__() se object ko initialize karta hai.
3. Jo object mila, uska reference d1 mein rakhta hai.

* Agar tumne apna __new__() nahi likha, toh Python default 
  object-creation mechanism use karega.

--------------------------------------------------------------------------

Lekin Singleton mein humein decide karna hai:

- Kya naya object banana chahiye ?
- Ya pehle se bana object hi return karna chahiye ?

* Isliye hum __new__() ko customize karte hain.

--------------------------------------------------------------------------

cls kya hai?
------------
* Is method mein cls ka matlab hai woh class jiska object ban raha hai. 
  Yahan cls ka reference Database class ko hai.

- self aam taur par already bane object ko refer karta hai.
- cls class ko refer karta hai.

__new__() ko object banne se pehle decision lena hai, isliye yahan class 
          cls ka use hota hai.

==========================================================================

6. Ab tumhara sabse important doubt: super().__new__(cls) kyun?

=> cls._instance = super().__new__(cls)

Tumhara sawaal tha: "Database() object create kar hi raha hai, toh phir 
                     super().__new__(cls) kyun likhna?"

Jawab: Database() object lene ki request hai. Hamara customized __new__() 
       decide karta hai ki request ko kaise poora karna hai.

* Jab humein sach mein naya object banana hota hai, tab super().__new__(cls) 
  Python ke normal object-creation mechanism ko use karta hai.

* Yahan super().__new__(cls) ka matlab hai: "Python, Database class ka ek 
                                             naya object bana do."

* Aur us object ka reference cls._instance mein save ho jata hai.

--------------------------------------------------------------------------

# Dono ka role alag hai:

Database()
    ↓
Hamare customized __new__() ko call karta hai
    ↓
super().__new__(cls)
    ↓
Sirf zaroorat padne par naya object banata hai

* Database() pehle koi extra object nahi banata jise super().__new__(cls) 
  dobara bana raha ho. Object creation ka process __new__() ke andar hi 
  control hota hai.

==========================================================================

7. if cls._instance is None kya kar raha hai ??

if cls._instance is None:
    cls._instance = super().__new__(cls)

Iska seedha matlab hai:
-----------------------
* "Agar abhi tak object save nahi hua hai, tabhi naya object banao."

* Pehli baar _instance ki value None hai, toh condition true hogi aur 
  object banega.

* Doosri baar _instance mein pehle se object ka reference hoga, toh 
  condition false hogi aur naya object nahi banega.

==========================================================================

8. return cls._instance ka kya kaam hai ?

=> return cls._instance

Iska matlab hai: "Jo object _instance mein saved hai, wahi caller 
                  ko wapas de do."

Jab tum likhte ho:
------------------
=> d1 = Database()

* Python tumhare __new__() se jo object return hota hai, uska reference d1 
  mein rakh deta hai.

Doosri baar:
------------
=> d2 = Database()

* __new__() wahi saved object return karta hai, isliye d2 bhi usi object 
            ko refer karta hai.

* return koi naya object nahi banata. Ye bas maujood object ka reference 
  wapas deta hai.

==========================================================================

10. Ek zaroori baat: __init__() ka kya hoga ?

* Is example mein humne __init__() nahi likha. Lekin agar 
  likhte, toh dhyan dena:

CODE:
-----
class Database:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance

    def __init__(self):
        print("Initializing Database")

* Database() ko do baar call karne par __init__() bhi do baar chal sakta 
  hai, bhale hi object ek hi ho.

* Isliye real Singleton implementation mein kabhi-kabhi initialization ko 
  bhi control karna padta hai. Lekin pehle __new__() aur shared object ka 
  concept achhe se samajhna zyada important hai.

==========================================================================

# Bas ye 5 baatein pakki kar lo:

1. Singleton            : baar-baar call karne par bhi ek hi shared object  
                          milta hai.

2. __new__(cls)         : object creation ko control karne ke liye customize 
                          kiya.

3. super().__new__(cls) : jab pehli baar zaroorat ho, tab naya object banata 
                          hai.

4. cls._instance: bane hue object ka reference save karta hai.

5. return cls._instance : saved object ko har call se wapas deta hai.

--> Aur isi wajah se d1 is d2 ka result True aata hai.

==========================================================================
--------------------------------------------------------------------------
==========================================================================

Doubt:
------
Jab tum likhte ho:

=> d1 = Database()

Python internally ye kaam karta hai:
1. __new__() se object banwata hai.
2. Uske baad __init__() se object ko initialize karta hai.
3. Jo object mila, uska reference d1 mein rakhta hai.

ye new se jo object banta hai vo dikhta kaisa hai ?
__init__() kaise object ko initialize karta hai, mtlb dikhne mai 
kaisa hota hai ?

or jo object mila uska reference d1 mein rakhta hai. lekin kyu ? 
object h kyu nhi rakhta

tmne ye bhi bola tha upr ki Doosri baar _instance mein pehle se object 
ka reference hoga, yaha par bhi reference toh ye object jab ban raha 
hai toh memory mai banraha hoga toh vo khud kyu save nhi hota kahi ? 
uska reference hi har koi liye jaa raha hai

or ek baat muje new se object kaise create hota hai vo batana or init 
object ko initialize karta hai iska kya mtkb hai vo bhi samjhana.

==========================================================================

Bahut achhe questions hain. Tum ab Singleton se bhi zyada basic aur 
important cheez pooch rahe ho: Python mein object asal mein hota kya 
hai, memory mein kaise banta hai, aur variables object ke bajaye uska 
reference kyun rakhte hain?

Agar ye samajh aa gaya, toh __new__(), __init__() aur Singleton teeno 
kaafi clear ho jayenge. Chalo ekdum shuru se samajhte hain.

==========================================================================

1. Sabse pehle: object dikhta kaisa hai ?

Maan lo humne ye class banayi:
------------------------------
class Student:
    pass

s1 = Student()

* Tum pooch rahe ho ki Student() se jo object bana, woh dikhta kaisa 
  hai?

* Abhi Student class ke andar kuch nahi hai. Toh Python ek aisa object 
  banata hai jo Student class ka hai, lekin uske andar abhi koi student-
  specific data nahi hai.

Isko aise imagine karo:
-----------------------
Memory mein ek object (conceptual drawing)
                |
          Student object
          Class: Student
                |
    Abhi koi name ya age set nahi hai

. Ye samjhane ke liye drawing hai. Memory mein object literally aise box 
  ke roop mein nahi dikhta.

--------------------------------------------------------------------------

* Object koi screen par dikhne wali cheez nahi hota. Ye memory mein bani 
  hui ek entity hai, jise Python manage karta hai.

Agar hum likhein:
-----------------
=> print(s1)

Toh output kuch aisa ho sakta hai:
----------------------------------
<__main__.Student object at 0x...>

* Ye object ki actual tasveer nahi hai. Ye Python ka text representation 
  hai jo object ki information deta hai.

==========================================================================

2. Object ke andar data kaise aata hai ?

* Ab class ko thoda useful banate hain:

CODE:
-----
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

s1 = Student("Rahul", 20)

--> Ab s1 jis object ko refer karta hai, us object mein name aur 
    age ki values set ho chuki hain.


s1
Object ka reference
      |
Student object
--------------
name  : "Rahul"
age   :   20

* Ye samajhna zaroori hai: class ek blueprint hai, object us blueprint 
                           se bana actual instance hai, aur name/age 
                           us object ka data hain.

==========================================================================

3. __new__() object kaise banata hai?

Pehle ye code dekho:
--------------------
class Student:
    def __new__(cls):
        print("Object banane ki process")

        obj = super().__new__(cls)

        print("Object mil gaya")
        return obj

s1 = Student()

Output:
-------
Object banane ki process
Object mil gaya

--------------------------------------------------------------------------

Ab line-by-line samjho:
-----------------------

Step 1
------
def __new__(cls):

* Hum Python ke object banane wale process mein apna method laga rahe 
  hain, taaki hum dekh sakein ki object kab create ho raha hai.

--------------------------------------------------------------------------

Step 2
------
obj = super().__new__(cls)

Yahan Python ka default object-creation mechanism ek naya Student object 
banata hai.

- super() humein parent class ke method tak pahunchata hai.
- Is simple example mein woh default method object.__new__() hai.
- cls batata hai ki kis class ka object banana hai — yahan Student.

* Is line ke baad obj mein naye object ka reference aa jaata hai.

* Dhyan do: object create karna aur us object ko variable mein refer 
            karna related hain, lekin ek hi cheez nahi hain.

--------------------------------------------------------------------------

Step 3
------
return obj

* Hum Python ko batate hain: "Ye raha woh object jo maine banaya."

* Phir Python us object par __init__() chalata hai, agar applicable 
  ho, aur Student() expression ka result caller ko milta hai.

* Ek important baat: Normal classes mein tumhe khud __new__() likhne 
                     ki zaroorat nahi hoti. Python default wala use 
                     karta hai. Humne ise sirf process samajhne ke 
                     liye customize kiya hai.

==========================================================================

4. Ab __init__() object ko initialize kaise karta hai ?

* Initialize karne ka simple matlab hai: bane hue object ko uski shuruaati 
                                         values dena ya uski shuruaati state 
                                         set karna.

Example:
--------
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

s1 = Student("Rahul", 20)

--------------------------------------------------------------------------

Object banne ke baad Python __init__() ko call karta hai. Us waqt:

- self us naye object ko refer karta hai.
- name ki value "Rahul" hai.
- age ki value 20 hai.

Ab ye lines dekho:
------------------
self.name = name
self.age = age

Inka matlab:
------------
- Is object ke andar name naam ka attribute banao/set karo aur usmein 
  "Rahul" rakho.

- Is object ke andar age naam ka attribute banao/set karo aur usmein 
  20 rakho.

Pehle object kuch aisa tha:
---------------------------
__init__() se pehle
        
Student object
Student-specific values abhi set nahi hui
         |
__init__("Rahul", 20) chalta hai
         |
__init__() ke baad
name
"Rahul"

age
20

* Yahan object ki koi physical appearance nahi badal rahi. Us object 
  ke saath judi hui information set ho rahi hai.

* __init__() khud object create nahi karta. Woh already ban chuke 
  object ko initialize karta hai.

==========================================================================

5. Tumhara agla doubt: "Object ko d1 mein kyun rakhte hain? Object hi 
   kyun nahi rakh sakte?"

Python mein jab tum likhte ho:
------------------------------
d1 = Student("Rahul", 20)

* Toh right side ka Student("Rahul", 20) ek object banata hai aur us 
  object ka reference return karta hai. Phir assignment = us reference 
  ko d1 naam se associate kar deta hai.

--------------------------------------------------------------------------

# Isko aise socho:

d1 variable
Object ko dhoondhne ka reference
       |
Student object
name = "Rahul", age = 20

* Tum d1 ko object ka naam samajh sakte ho, lekin technically d1 ek 
  variable hai jo object ko refer karta hai.

--------------------------------------------------------------------------

* Agar tum d1 na banao, tab bhi object create ho sakta hai:

=> Student("Rahul", 20)

--> Lekin uska reference kahin save nahi kiya, toh tum use baad mein aasani 
    se access nahi kar paoge. Agar koi aur reference bhi us object ko hold 
    nahi karta, toh Python us object ko baad mein memory se hata sakta hai.

--> Isliye variable mein reference rakhna useful hai: taaki hum object ko 
    baad mein use kar sakein.

Example:
--------
print(d1.name)print(d1.age)

Output:
-------
Rahul
20

==========================================================================

6. "Object memory mein hai, toh uska reference hi kyun? Object khud save 
    kyun nahi hota?"

Ye sabse important concept hai.
-------------------------------
* Object memory mein hota hi hai. Reference koi doosra object nahi hai; 
  woh object tak pahunchne ka tareeka hai.

* Maan lo memory mein ek Student object bana hua hai. Python ko pata hai 
  woh object kahan hai. Variable d1 us object ko refer karta hai.

Ek simple analogy:
------------------
- Object      = ghar
- Reference   = ghar ka address
- Variable d1 = woh jagah jahan tumne address likh rakha hai.

Ghar ek hi hai. Tum uska address kai logon ko de sakte ho.

--------------------------------------------------------------------------

Isi tarah Python mein:
---------------------
d1 = Student("Rahul", 20)
d2 = d1

* Ab d1 aur d2 dono same object ko refer karte hain. Naya Student 
  object nahi bana.

d1                    d2
------------------------
Same Student object
name = "Rahul", age = 20

Isliye:
-------
print(d1 is d2)

Output:
-------
True

--> Kyunki dono ek hi object ko refer kar rahe hain.

==========================================================================

7. Toh Singleton mein _instance ka reference kyun save hota hai?

* Ab hum tumhare pehle wale doubt par wapas aate hain.

CODE:
-----
class Database:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)

        return cls._instance

Tum pooch rahe the: "Jab object memory mein ban gaya, toh uska 
                     reference _instance mein save karne ki 
                     zaroorat kyun hai?"

Kyunki Singleton ko agli baar check karna hai ki object pehle se 
bana hai ya nahi, aur agar bana hai toh usi object ko return karna 
hai.

--------------------------------------------------------------------------

Pehli baar:
-----------
cls._instance = super().__new__(cls)

- Naya Database object banta hai.
- Uska reference _instance mein save hota hai.

Doosri baar:
------------
if cls._instance is None:

- _instance mein pehle se reference hai.
- Isliye naya object nahi banta.

Phir:
-----
return cls._instance

- Wahi pehle wala object return hota hai.

* Agar hum _instance mein reference save hi na karein, toh class ke paas 
  us pehle object ko yaad rakhne ka ye tareeka nahi rahega. Har baar code 
  ko lagega ki object abhi tak bana hi nahi, aur woh naya object bana 
  sakta hai.

==========================================================================

8. Poore process ka short recap:

CODE:
-----
class Database:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance

d1 = Database()
d2 = Database()
print(d1 is d2)  # True

* Database() Python ko object lene ki request deta hai.

* __new__() decide karta hai ki naya object banana hai ya 
            existing object return karna hai.

* super().__new__(cls) naya object create karta hai, lekin 
  is code mein sirf pehli baar.

* _instance us object ka reference save karta hai, taaki 
  class use dobara de sake.

* return cls._instance wohi object return karta hai.

* d1 aur d2 dono usi object ko refer karte hain.

Ek final distinction yaad rakho: __new__() object create karta hai, __init__() 
                                 us object ki initial values set karta hai, aur 
                                 variable jaise d1 us object ko access karne ke 
                                 liye reference rakhta hai.

==========================================================================
--------------------------------------------------------------------------
==========================================================================

Doubt:
------
tmne bola ki `Database()` Python ko object lene ki request deta hai.
lekin ye \
d1 = Database() toh object banane ki request hai naa toh lene ki 
request ka kya mtlb hua ?

--------------------------------------------------------------------------

Ab ek chhota sa difference samjho.

=> d1 = Database()

Is line mein do cheezein ho rahi hain:
--------------------------------------
1. Database() — Python se Database ka object banane ko kaha ja raha hai.
2. d1 =       — jo object Database() se return hoga, uska reference d1 
                mein store hoga.

Lekin Singleton mein ek twist hai.

Pehli baar:
-----------
d1 = Database()

--> Object abhi nahi hai, toh Python naya object banata hai aur d1 mein 
    uska reference store ho jata hai.

Doosri baar:
------------
d2 = Database()

--------------------------------------------------------------------------

* Yahan bhi hum object banane ki request kar rahe hain, lekin hamara 
  customized __new__() check karta hai ki object pehle se bana hai 
  ya nahi. Agar bana hua hai, toh naya object banane ke bajaye wahi 
  purana object return kar deta hai.

Isliye:
-------
=> print(d1 is d2)  # True

* Bas ye difference yaad rakho: Database() object banane ki request karta 
                                hai, lekin Singleton ka __new__() decide 
                                karta hai ki naya object banana hai ya 
                                pehle se bana object hi return karna hai.

==========================================================================
--------------------------------------------------------------------------
==========================================================================

Doubt:
------
def __new__(cls):

* Isko samajhne ke liye object banne ka process dekho.

Jab tum likhte ho:
------------------
=> d1 = Database()

Python internally ye kaam karta hai:
------------------------------------
1. __new__() se object banwata hai.
2. Uske baad __init__() se object ko initialize karta hai.
3. Jo object mila, uska reference d1 mein rakhta hai.


tmne bola ki __new__() se object banwata hai lekin object 
toh isse ban raha hai naa super().__new__(cls), 2-2 jagah
se object kaise ban raha hai ?

--------------------------------------------------------------------------

ANS)
----

* Haan! Tumhara doubt bilkul sahi jagah par hai. Confusion isliye ho raha 
  hai kyunki maine bola tha __new__() object banata hai, aur phir code 
  mein super().__new__(cls) bhi likha hai. Toh lagta hai ki do jagah 
  object ban raha hai.

Lekin aisa nahi hai. Chalo samajhte hain.

==========================================================================

1. Pehle ye code dekho:

CODE:
-----
class Database:
    def __new__(cls):
        obj = super().__new__(cls)
        return obj

d1 = Database()

--> Is code mein object sirf ek baar ban raha hai.

Dono lines ka role alag hai:
----------------------------
- def __new__(cls) — ye ek method define karta hai. Khud object nahi 
  banata.

- super().__new__(cls) — ye actual mein naya object create karta hai.

* Jab Python Database() dekhta hai, toh woh tumhara __new__() method 
  call karta hai. Us method ke andar super().__new__(cls) execute hota 
  hai aur object create karta hai.

==========================================================================

2. Poora process aise chalta hai:

Code                          | Kya hota hai?
------------------------------|--------------------------------------
d1 = Database()               | Object banane ki request
__new__(cls)                  | Customized method call hota hai
super().__new__(cls)          | Naya object create hota hai
return obj                    | Wahi object return hota hai
d1                            | Object ka reference store karta hai

==========================================================================

3. Toh phir __new__() object banata hai bolne ka kya matlab tha?

* Woh meri explanation mein shortcut tha. Zyada accurate baat ye hai:

* __new__() object creation ko handle karta hai. Jab hum ise customize 
  karte hain, toh iske andar super().__new__(cls) call karke actual naya 
  object banwa sakte hain.

Jaise:
------
def __new__(cls):
    obj = super().__new__(cls)
    return obj

* Yahan __new__() poora process control kar raha hai, lekin actual 
  object creation super().__new__(cls) kar raha hai.

--------------------------------------------------------------------------

Aur jab hum Singleton mein likhte hain:
---------------------------------------
def __new__(cls):
    if cls._instance is None:
        cls._instance = super().__new__(cls)

    return cls._instance

==========================================================================

* Toh super().__new__(cls) sirf pehli baar chalta hai. Agli baar __new__() 
  phir call hota hai, lekin pehle se bana object return kar diya jaata hai.

Ek line mein: Database() request karta hai, __new__() us request ko handle 
              karta hai, aur super().__new__(cls) actual naya object banata 
              hai — isliye do objects nahi bante.