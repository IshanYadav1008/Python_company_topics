Python Notes: iter() aur __iter__()
-----------------------------------

1. iter() kya hai?
------------------

- Python mein iter() ek built-in function hai, jiska kaam kisi iterable 
  object se iterator lena hai.

- Simple words mein, jab humein kisi object ke items ek-ek karke access  
  karne hote hain, toh hum iter() se uska iterator le sakte hain.

Example:
--------
fruits = ["Apple", "Mango", "Banana"]

it = iter(fruits)

print(next(it))
print(next(it))
print(next(it))

Output:
-------
Apple
Mango
Banana

Yahan kya hua ?
---------------
1. fruits ek list hai.
2. iter(fruits) ne list ke liye ek iterator diya.
3. it variable mein woh iterator store hua.
4. Har next(it) ne agla fruit diya.

Yaad rakh: iter() khud next item nahi deta. Woh iterator deta hai, 
           jisse baad mein next() ke through items liye jaate hain.

==============================================================================

2. iter() aur __iter__() mein kya difference hai ? 
--------------------------------------------------

* Dono related hain, lekin ek hi cheez nahi hain.

- iter() Python ka built-in function hai, jise hum call karte hain.

- __iter__() Python ka special method hai, jise iterator provide 
  karne ke liye object ki class mein define kiya ja sakta hai.

Jab tu likhta hai:
------------------
=> it = iter(fruits)

* Python internally fruits ke iterator ko obtain karne ke liye uske 
  iteration protocol ka use karta hai. List ke case mein, uska 
  __iter__() method iterator return karta hai.

* Custom class mein bhi hum __iter__() define kar sakte hain, taaki
  Python ko pata chale ki us class ke object se iterator kaise milega.

==============================================================================

3. Teri custom class se samajh:
-------------------------------
class Numbers:
    def __init__(self):
        self.n = 10

    def __iter__(self):
        print("__iter__ chala")
        return self

    def __next__(self):
        if self.n > 30:
            raise StopIteration

        result = self.n
        self.n += 10
        return result


it = Numbers()

x = iter(it)

print(next(x))
print(next(x))
print(next(x))

Output:
-------
__iter__ chala
10
20
30

------------------------------------------------------------------------------

Dry run:
--------
1. it = Numbers()

=> Numbers ka object banta hai. __init__() chalta hai aur self.n = 10 
   set hota hai.

2. x = iter(it)

=> Python it se iterator maangta hai. Iske liye __iter__() chalta hai. 
   return self ki wajah se wahi object x mein aa jata hai.

3. next(x)

=> __next__() chalta hai, 10 return karta hai aur self.n ko 20 kar deta 
   hai.

4. Agli next(x) calls

=> Agli calls 20 aur 30 return karti hain. Uske baad self.n = 40 hone 
   par StopIteration aata hai.

- Is example mein iter(it) ne numbers generate nahi kiye. Usne sirf 
  iterator obtain kiya. Numbers __next__() ne diye.

==============================================================================

4. for loop mein iter() ka kya kaam hai ?
-----------------------------------------

* Ab isi class ko for loop mein use kar:

it = Numbers()

for number in it:
    print(number)

Output:
-------
10
20
30

Python roughly ye process follow karta hai:
-------------------------------------------

1. iter(it) se iterator leta hai.
2. __iter__() chalta hai aur self return karta hai.
3. next() ke through agla number leta hai.
4. Ye process repeat hota hai.
5. StopIteration milne par loop khatam ho jata hai.

* Isi wajah se custom iterator mein __iter__() aur __next__() dono 
  important hote hain: for loop ko iterator chahiye, aur phir us 
  iterator se items lene hote hain.

==============================================================================

5. Agar __iter__() nahi likhen toh ?

* Agar teri custom class mein __next__() toh hai, lekin __iter__() 
  nahi hai, toh:

it = Numbers()
print(next(it))

- Direct next(it) chal sakta hai, kyunki object ka __next__() method 
  available hai.

- Lekin agar us class ko for loop mein use karna hai, toh Python ko 
  us object se iterator obtain karne ka tareeka bhi chahiye. Aam taur 
  par custom iterator class mein isi liye __iter__() define kiya jata 
  hai.

==============================================================================

6. Tere important points — notes ke liye:
-----------------------------------------

iter(it)       -> iterator maangta hai
__iter__()     -> iterator deta hai
__next__()     -> agla item deta hai
for loop       -> in methods ko use karke items par chalta hai

In points ko is tarah samajh:
-----------------------------

Code	                 Matlab
-----------------------------------------------------------------------
iter(obj)	             Object se iterator obtain karna
-----------------------------------------------------------------------
obj.__iter__()	         Iterator dene wala special method
-----------------------------------------------------------------------
next(it)	             Iterator se agla item lena
-----------------------------------------------------------------------
it.__next__()	         Agla item dene wala special method
-----------------------------------------------------------------------
return self	             Wahi object iterator ke roop mein return karna
-----------------------------------------------------------------------
raise StopIteration	     Batana ki ab aur items nahi hain
-----------------------------------------------------------------------

==============================================================================

7. Ek aur important baat:
-------------------------

* iter() har baar naya iterator banaye, ye zaroori nahi hai.

- List                : iter(fruits) aam taur par list se ek alag iterator  
                        object deta hai.

- Tera Numbers object : iter(it) wahi object return karta hai, kyunki
                       __iter__() mein return self hai.

* Isliye iter(it) ke baad x = iter(it) likhne par x aur it same object ho 
  sakte hain. Tere example mein dono same hain.


Final revision: poora concept ek nazar mein
-------------------------------------------

* Iteration ka flow

iter(object)
Iterator obtain karo
    |
    |
__iter__()
Iterator provide karo
    |
    |
next(iterator) → __next__()
Agla item lo; repeat karo
    |
    |
StopIteration
Items khatam — for loop band

* Sabse zaroori baat: iter() iterator obtain karne ka function hai. __iter__() 
                      batata hai ki object se iterator kaise milega. __next__() 
                      actual mein agla item deta hai. for loop in sab ko automatically manage karta hai, isliye tujhe har item ke liye manually next() nahi likhna padta.