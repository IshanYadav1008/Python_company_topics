* Python Iterator aur Custom Iterator — Zero Level Se:

- Sabse pehle ek simple example se shuru karte hain. Tumne list, 
  for loop, next() aur generator padha hai. Ab in sabko connect 
  karke samjhenge ki Iterator kya hai aur Custom Iterator kaise
  banate hain.

-------------------------------------------------------------------------------

1. Sabse pehle: Iteration kya hota hai ?
----------------------------------------
* Iteration ka simple matlab hai kisi collection ki items ko 
  ek-ek karke access karna.

Example:
--------
fruits = ["Apple", "Mango", "Banana"]

for fruit in fruits:
    print(fruit)

Output:
-------
Apple
Mango
Banana

- Yahan for loop ne fruits ko ek-ek karke access kiya. Is process ko 
  iteration kehte hain.

-------------------------------------------------------------------------------

Iteration in cheezon par bhi kar sakte ho:
------------------------------------------
for number in [10, 20, 30]:
    print(number)

for letter in "CAT":
    print(letter)

for number in range(1, 4):
    print(number)

- Matlab list, string aur range jaise objects par ek-ek karke chal 
  sakte hain.

- Lekin ek sawal : Python ko kaise pata chalta hai ki agla fruit 
                   kaunsa hai? Isko samajhne ke liye iterator 
                   samjho.

===============================================================================

2. Iterator kya hota hai ?
--------------------------

* Iterator ek aisa object hai jo ek samay par agla item deta hai aur 
  apni current position ya state yaad rakhta hai.

Example:
--------
fruits = ["Apple", "Mango", "Banana"]

fruit_iterator = iter(fruits)

print(next(fruit_iterator))
print(next(fruit_iterator))
print(next(fruit_iterator))

Output:
-------
Apple
Mango
Banana

- Is code mein do naye functions hain: iter() aur next().

-------------------------------------------------------------------------------

iter() kya karta hai ?
----------------------
=> fruit_iterator = iter(fruits)

- fruits ek list hai.
- iter(fruits) us list se iterator banata hai.
- fruit_iterator ab ek-ek karke agla fruit dene ke liye ready hai.

next() kya karta hai ?
----------------------
=> print(next(fruit_iterator))

- Yeh iterator se agla item maangta hai.

-------------------------------------------------------------------------------

# Yeh iterator se agla item maangta hai.

* Iterator kaise aage badhta hai?

Items: Apple → Mango → Banana

Apple       Mango        Banana
Waiting     Waiting      Waiting

- Agla item: Abhi tak koi item nahi

- Abhi next() call nahi hua.

<---------------------------------------------------->

Apple       Mango        Banana
Current     Waiting      Waiting

- Agla item: Apple
- next() call karne par iterator agle item par badhega.

<---------------------------------------------------->

Apple       Mango        Banana
Done        Current      Waiting

- Agla item: Mango
- next() call karne par iterator agle item par badhega.

<---------------------------------------------------->

Apple       Mango        Banana
Done        Done         Current

Agla item: Banana

- Teeno items mil chuke hain. Agli call par StopIteration 
  aayega.

- Resetnext() call karo

<---------------------------------------------------->

Apple       Mango        Banana
Done        Done         Done

- Agla item: Koi item nahi — iterator khatam
- Teeno items mil chuke hain. Agli call par StopIteration 
  aayega.

<---------------------------------------------------->

* Har baar next() call karne par iterator agla item deta hai aur 
  apni position aage badhata hai.

* Jab saare items khatam ho jaate hain, agla next() StopIteration 
  exception raise karta hai.

CODE:
-----
fruits = ["Apple", "Mango"]
it     = iter(fruits)

print(next(it))  # Apple
print(next(it))  # Mango
print(next(it))  # StopIteration exception

- Yeh exception normal behavior hai. Python isi se batata hai ki 
  iterator ke paas ab aur items nahi hain.

===============================================================================

3. Iterable aur Iterator mein kya difference hai ?

* Yeh bahut important concept hai. Dono ke naam similar hain, lekin 
  dono same cheez nahi hain.

- Iterable: Aisi cheez jisse iterator banaya ja sakta hai.

- Iterator: Aisa object jo agla item de sakta hai aur apni progress 
            track karta hai.

-------------------------------------------------------------------------------

Example:
--------
fruits = ["Apple", "Mango", "Banana"]
it     = iter(fruits)

Yahan:
------
- fruits = iterable (list)
- it     = iterator

* Ek iterable se alag-alag iterators banaye ja sakte hain.

CODE:
-----
fruits = ["Apple", "Mango", "Banana"]
it1    = iter(fruits)
it2    = iter(fruits)

print(next(it1))  # Apple
print(next(it1))  # Mango
print(next(it2))  # Apple

- it1 aur it2 ki positions alag hain. it1 Mango tak pahunch 
  gaya, lekin it2 abhi Apple se shuru hua.

-------------------------------------------------------------------------------

# Copy-friendly comparison table:

+-------------------+-------------------------+-------------------------+
| Point             | Iterable                | Iterator                |
+-------------------+-------------------------+-------------------------+
| Meaning           | Jisse iterator ban sake | Jo agla item de sake    |
+-------------------+-------------------------+-------------------------+
| Example           | List, string, range     | iter(list) ka result    |
+-------------------+-------------------------+-------------------------+
| iter()            | Iterator banane ke liye | Khud ko iterator deta   |
|                   | use hota hai            | hai                     |
+-------------------+-------------------------+-------------------------+
| next()            | Directly usually nahi   | Agla item deta hai      |
+-------------------+-------------------------+-------------------------+
| Position          | Zaroori nahi ki state   | Apni progress track     |
|                   | rakhe                   | karta hai               |
+-------------------+-------------------------+-------------------------+

- Iterator ke liye ek useful rule: Python mein iterator ko iter() aur 
  next() support karna chahiye. Technically, iter(iterator) wahi iterator 
  return karta hai.

===============================================================================

4. for loop ke peeche kya hota hai?

* Ab tumne iterator samajh liya, toh ek important baat: Python ka 
  for loop bhi iterable se iterator lekar items ko ek-ek karke 
  access karta hai.

Tum likhte ho:
--------------
fruits = ["Apple", "Mango", "Banana"]

for fruit in fruits:
    print(fruit)

Conceptually, Python ise is tarah handle karta hai:
---------------------------------------------------
fruits = ["Apple", "Mango", "Banana"]

it = iter(fruits)

while True:
    try:
        fruit = next(it)
        print(fruit)
    except StopIteration:
        break

Dono ka output same hai:
------------------------
Apple
Mango
Banana

- Doosra example iterator ka mechanism samjhane ke liye hai. Real 
  code mein aam taur par simple for loop hi likhna chahiye.

===============================================================================

5. Ab Custom Iterator kya hai?

* Ab tak hum built-in list se iterator bana rahe the:

numbers = [10, 20, 30]
it      = iter(numbers)

- Lekin socho, tum ek aisa object banana chahte ho jo khud decide 
  kare ki kaunsa number agla dena hai.

Example: ek custom counter jo 1, 2, 3, 4, 5 de.

-------------------------------------------------------------------------------

* Custom Iterator ka matlab hai apna khud ka iterator banana, jisme 
  hum define karte hain ki iterator ka state kya hoga aur har baar 
  agla item kaise milega.

* Python mein custom iterator banane ke liye aam taur par do special 
  methods use hote hain:

- __iter__() — iterator return karta hai; iterator khud ho toh aam 
               taur par self return karta hai.

- __next__() — agla item return karta hai. Items khatam hone par 
               StopIteration raise karta hai.

- In special methods ke naam ke dono taraf double underscores hain. 
  Inhe Python mein dunder methods bhi kehte hain.

===============================================================================

6. Pehla Custom Iterator banao:

CODE:
-----
class MyNumbers:
    def __init__(self):
        self.num = 1

    def __iter__(self):
        return self

    def __next__(self):
        if self.num <= 5:
            result = self.num
            self.num += 1
            return result
        else:
            raise StopIteration


numbers = MyNumbers()

for number in numbers:
    print(number)

Output:
-------
1
2
3
4
5

- Ab is code ko bilkul basic level se samjho.

-------------------------------------------------------------------------------

Step 1: class MyNumbers
-----------------------
class MyNumbers:

* class se hum apna custom type banate hain. Yahan MyNumbers ek aisa 
  type hai jiske objects numbers generate karenge.

-------------------------------------------------------------------------------

Step 2: __init__()
------------------
def __init__(self):    
self.num = 1

- Jab hum MyNumbers() banate hain, tab __init__() chalta hai.

- self.num = 1 ka matlab hai ki object apni current value 1 se 
               shuru karega.

- self.num ko object ki memory mein rakhi hui state samjho. Isi 
           se object ko yaad rahega ki ab kaunsa number dena hai.

-------------------------------------------------------------------------------

Step 3: __iter__()
------------------

def __iter__(self):
    return self

- Yeh object ko iterator ke roop mein return karta hai.

- Yahan self ka matlab hai wahi current object. Isliye 
  iter(numbers) call karne par numbers object khud return 
  hota hai.

-------------------------------------------------------------------------------

Step 4: __next__()
------------------
def __next__(self):
    if self.num <= 5:
        result = self.num
        self.num += 1
        return result
    else:
        raise StopIteration

- Yahi custom iterator ka main logic hai.

Maan lo self.num = 1 hai:
-------------------------
1. self.num <= 5 check hoga — condition true.
2. result = self.num        — result mein 1 aayega.
3. self.num += 1            — ab object ka number 2 ho jayega.
4. return result            — is call se 1 milega.

* Agli next() call par object ki state 2 hai, isliye woh 2 dega. 
  Isi tarah 5 tak chalega.

* Jab self.num 6 ho jayega, condition false hogi aur StopIteration 
  raise hoga.

* Ek important detail: result mein current value save karne ke baad 
                       self.num badhaya gaya hai. Agar pehle self.num 
                       increment kar dete, toh pehla number 2 hota aur 
                       1 skip ho jata.

===============================================================================

7. Custom Iterator ko manually chala kar dekho:

numbers = MyNumbers()

print(next(numbers))  # 1
print(next(numbers))  # 2
print(next(numbers))  # 3

- Yahan for loop use nahi kiya. Humne next() manually call kiya, aur 
  har baar custom iterator ka __next__() method chala.

- Iska fayda hai ki tum control kar sakte ho ki agla item kab lena hai.

===============================================================================

8. Generator vs Custom Iterator:

* Dono ek-ek karke values de sakte hain, lekin implementation alag hai.

+--------------------+--------------------------+--------------------------+
| Point              | Generator                | Custom Iterator          |
+--------------------+--------------------------+--------------------------+
| Banane ka tareeka  | yield wali function      | Class aur methods        |
+--------------------+--------------------------+--------------------------+
| State management   | Python automatically     | Aksar khud manage karte  |
|                    | preserve karta hai       | hain                     |
+--------------------+--------------------------+--------------------------+
| Code               | Aam taur par chhota      | Aam taur par zyada       |
|                    | aur simple               | detailed                 |
+--------------------+--------------------------+--------------------------+
| Agli value         | yield se milti hai       | __next__() se milti hai  |
+--------------------+--------------------------+--------------------------+
| Kab use karein     | Simple sequence ya       | Custom iteration rules   |
|                    | stream generate karna    | aur object behavior      |
+--------------------+--------------------------+--------------------------+

-------------------------------------------------------------------------------

* Same counter ko generator se bhi likh sakte ho:

CODE:
-----
def my_numbers():
    num = 1

    while num <= 5:
        yield num
        num += 1

for number in my_numbers():
    print(number)

* Output phir se 1 se 5 tak hoga.

* Generator mein Python khud pause/resume aur local state sambhalta hai. 
  Custom iterator mein tum explicitly define karte ho ki state kaise 
  badlegi aur StopIteration kab aayega.

===============================================================================

9. Ek chhota test

Question: Custom iterator mein __next__() ka main kaam kya hai?

ANS) Agla item dena aur items khatam hone par StopIteration raise 
     karna.

Bilkul sahi!
------------
* __next__() agla item deta hai. Jab items khatam ho jaate hain, 
             toh StopIteration raise karke batata hai ki iterator 
             complete ho gaya.

===============================================================================

Final recap:
------------
Iteration       = Items ko ek-ek karke access karna.
Iterable        = Jisse iterator ban sakta hai.
Iterator        = Jo next item deta hai aur progress track karta hai.
iter(obj)       = Iterator hasil karna.
next(it)        = Agla item lena.
Custom Iterator = Class se apna iterator banana.
__iter__()      = Iterator return karna.
__next__()      = Agla item dena.
StopIteration   = Iterator ke items khatam ho gaye.