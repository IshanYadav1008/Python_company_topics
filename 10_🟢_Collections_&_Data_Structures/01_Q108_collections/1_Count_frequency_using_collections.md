Is topic ko samajhne ke liye hum 4 steps follow karenge:
--------------------------------------------------------

1. list kya hoti hai ?
2. Frequency counting kya hoti hai ?
3. dict se frequency count kaise karte hain ?
4. collections.Counter se wahi kaam aasani se kaise karte hain ?

--------------------------------------------------------------------------------

1. Sabse pehle samjho: Frequency kya hoti hai ?
-----------------------------------------------

* Frequency ka simple meaning hai — koi item kitni baar repeat 
  ho raha hai.

Maan lo tumhare paas ye list hai:
---------------------------------
numbers = [1, 2, 1, 3, 2, 1, 4]

Ab count karo:
--------------
- 1 kitni baar aaya? → 3 baar
- 2 kitni baar aaya? → 2 baar
- 3 kitni baar aaya? → 1 baar
- 4 kitni baar aaya? → 1 baar

* Isko frequency counting kehte hain.

================================================================================

2. Python list ka role:
-----------------------

* List ek collection hai jisme hum multiple values store kar 
  sakte hain.

fruits = ["apple", "banana", "apple", "mango", "banana", "apple"]
print(fruits)

Output:
-------
['apple', 'banana', 'apple', 'mango', 'banana', 'apple']

- Yahan apple 3 baar, banana 2 baar aur mango 1 baar hai.

- Lekin Python list khud frequency nahi batati. Frequency 
  nikalne ke liye hum counting logic likh sakte hain ya 
  Counter ka use kar sakte hain.

================================================================================

3. dict se frequency count karna:
---------------------------------

* Pehle collections module use kiye bina frequency count karte 
  hain. Isse tumhe samajh aayega ki Counter andar se kis tarah 
  ka kaam aasaan banata hai.

CODE:
-----
numbers = [1, 2, 1, 3, 2, 1, 4]
freq = {}

for num in numbers:
    if num in freq:
        freq[num] += 1
    else:
        freq[num] = 1

print(freq)

Output:
-------
{1: 3, 2: 2, 3: 1, 4: 1}

* Ab is code ko line-by-line samjho.

--------------------------------------------------------------------------------

Step 1: Empty dictionary
------------------------
=> freq = {}   // Shuru mein dictionary khaali hai.

--------------------------------------------------------------------------------

Step 2: List ke items par loop
------------------------------
=> for num in numbers:   // num ek-ek karke list ki values 
                            lega: 1, 2, 1, 3 aur aage.

--------------------------------------------------------------------------------

Step 3: Check karo item pehle se hai ya nahi:
---------------------------------------------
if num in freq:
    freq[num] += 1
else:
    freq[num] = 1

. Agar item dictionary mein pehle se hai, uski counting 1 se 
  badha do.

. Agar item pehli baar aaya hai, uski counting 1 se shuru karo.

--------------------------------------------------------------------------------

# Chalo loop ko shuru ke kuch steps mein dekhte hain:

Current num      Kya hua?	           freq
----------------------------------------------------------
1	             Pehli baar aaya	   {1: 1}
2	             Pehli baar aaya	   {1: 1, 2: 1}
1	             Dobara aaya	       {1: 2, 2: 1}
3	             Pehli baar aaya	   {1: 2, 2: 1, 3: 1}
2	             Dobara aaya	       {1: 2, 2: 2, 3: 1}
1	             Dobara aaya	       {1: 3, 2: 2, 3: 1}
----------------------------------------------------------

- Aakhir mein 4 bhi add hota hai aur final dictionary milti hai.

* Yahan ek important concept: Dictionary mein item key hota hai 
  aur uski frequency value hoti hai.

=> {1: 3, 2: 2, 3: 1, 4: 1}

- Matlab 1 ki frequency 3 hai, 2 ki frequency 2 hai.

================================================================================

4. Ab collections.Counter seekho:
---------------------------------

* Python mein frequency counting ke liye ek ready-made tool 
  hai: Counter.

Ise use karne ke liye:
----------------------
=> from collections import Counter

Ab wahi list dekho:
-------------------
from collections import Counter
numbers = [1, 2, 1, 3, 2, 1, 4]
freq    = Counter(numbers)
print(freq)

Output:
-------
Counter({1: 3, 2: 2, 3: 1, 4: 1})

- Bas! Itne se code mein frequency count ho gayi.

- Counter(numbers) list ke har unique item ko count karta hai aur 
  ek Counter object return karta hai, jo dictionary jaisa behave 
  karta hai.

--------------------------------------------------------------------------------

Kisi ek item ki frequency kaise nikaalein ?
-------------------------------------------
from collections import Counter
fruits = ["apple", "banana", "apple", "mango", "banana", "apple"]
freq   = Counter(fruits)

print(freq["apple"])
print(freq["banana"])
print(freq["mango"])

Output:
-------
3
2
1

Yahan:
------
- freq["apple"]  → 3
- freq["banana"] → 2
- freq["mango"]  → 1

--------------------------------------------------------------------------------

* Counter ke kuch useful methods:
---------------------------------
from collections import Counter
numbers = [1, 2, 1, 3, 2, 1, 4]
freq    = Counter(numbers)

print(freq.most_common(2))
print(freq.total())

Output:
-------
[(1, 3), (2, 2)]
7

- most_common(2) → sabse zyada baar aane wale top 2 items aur unki 
                   frequencies.

- total()        → saari frequencies ka sum, yani total items ki 
                   sankhya. Python 3.10+ mein available hai.

================================================================================

5. Real-life example: Word frequency
------------------------------------

* Maan lo tumhe kisi sentence mein har word ki frequency count 
  karni hai.

CODE:
-----
from collections import Counter

sentence = "python is easy and python is powerful"
words    = sentence.split()
freq     = Counter(words)
print(freq)

Output:
-------
Counter({'python': 2, 'is': 2, 'easy': 1, 'and': 1, 'powerful': 1})

- Yahan split() sentence ko words ki list mein convert karta hai. 
  Phir Counter har word ko count karta hai.

- Dhyan rahe: Is simple example mein uppercase aur lowercase words 
              ko alag maana jayega, aur punctuation remove nahi 
              hota.

================================================================================

6. Ab tumhari practice:
-----------------------

* Ye 3 chhote questions solve karke dekho. Isse pata chalega ki 
  concept clear hua ya nahi.

Q1. Is list mein 5 ki frequency kitni hai ?

nums = [5, 2, 5, 3, 5, 2]

o/p: 3

<---------------------------------------------------->

Q2. Counter use karne ke liye kaunsa import sahi hai ?

o/p: from collections import Counter

<---------------------------------------------------->

Q3. Counter(["a", "b", "a"])["a"] ka result kya hoga ?

o/p: 2

================================================================================
--------------------------------------------------------------------------------
================================================================================

1. Program:
-----------
numbers = [1, 2, 1, 3, 2, 1, 4]
freq = {}

for num in numbers:
    if num in freq:
        freq[num] += 1
    else:
        freq[num] = 1

print(freq)

================================================================================

2. Program ka logic samjho:
---------------------------

- numbers            — numbers ki list hai.

- freq = {}          — ek empty dictionary hai, jisme har number ki 
                       counting store hogi.

- for num in numbers — list se ek-ek number num mein aayega.

- if num in freq     — check karega ki number dictionary mein pehle 
                       se hai ya nahi.

- freq[num] += 1     — number pehle se hai, toh uski counting 1 badha 
                       do.

- freq[num] = 1      — number pehli baar aaya hai, toh uski counting 
                       1 se shuru karo.

- print(freq)        — final dictionary print karega.

================================================================================

3. Complete dry run
-------------------

Starting condition:
-------------------
numbers = [1, 2, 1, 3, 2, 1, 4]
freq = {}

- Har loop mein sirf ek number process hoga. if-else complete 
  hone ke baad hi agla number aayega.

--------------------------------------------------------------------------------

Copyable dry-run table
----------------------
* Table ko copy karne ke liye neeche Copy button use karo.

Loop | num | Kya num freq mein hai? | Executed statement | freq after loop
-----------------------------------------------------------------------------------
1    | 1   | No                     | freq[1] = 1        | {1: 1}
2    | 2   | No                     | freq[2] = 1        | {1: 1, 2: 1}
3    | 1   | Yes                    | freq[1] = 1 + 1    | {1: 2, 2: 1}
4    | 3   | No                     | freq[3] = 1        | {1: 2, 2: 1, 3: 1}
5    | 2   | Yes                    | freq[2] = 1 + 1    | {1: 2, 2: 2, 3: 1}
6    | 1   | Yes                    | freq[1] = 2 + 1    | {1: 3, 2: 2, 3: 1}
7    | 4   | No                     | freq[4] = 1        | {1: 3, 2: 2, 3: 1, 4: 1}
-----------------------------------------------------------------------------------

================================================================================

4. Har loop ki detailed explanation:
------------------------------------

Loop 1
------
num = 1
freq = {}

Check: 1 dictionary mein nahi hai.

Isliye else chalega:
--------------------
freq[1] = 1

Result:
-------
{1: 1}

--------------------------------------------------------------------------------

Loop 2
------
num = 2

Check: 2 dictionary mein nahi hai.

Isliye:
-------
freq[2] = 1

Result:
-------
{1: 1, 2: 1}

* Dhyan do: purana 1 delete nahi hota. Dictionary mein nayi 
            key 2 add hoti hai.

--------------------------------------------------------------------------------

Loop 3
------
num = 1

Check: 1 dictionary mein pehle se hai, aur uski value 1 hai.

Isliye if chalega:
------------------
freq[1] = freq[1] + 1freq[1] = 1 + 1

Result:
-------
{1: 2, 2: 1}

--------------------------------------------------------------------------------

Loop 4
------
num = 3

Check: 3 dictionary mein nahi hai.

freq[3] = 1


Result:
-------
{1: 2, 2: 1, 3: 1}

--------------------------------------------------------------------------------

Loop 5
------
num = 2

Check: 2 dictionary mein hai, uski value 1 hai.


freq[2] = 1 + 1

Result:
-------
{1: 2, 2: 2, 3: 1}

--------------------------------------------------------------------------------

Loop 6
------
num = 1

Check: 1 dictionary mein hai, uski value ab 2 hai.

freq[1] = 2 + 1

Result:
-------
{1: 3, 2: 2, 3: 1}

--------------------------------------------------------------------------------

Loop 7
------
num = 4

Check: 4 dictionary mein nahi hai.

freq[4] = 1

Result:
-------
{1: 3, 2: 2, 3: 1, 4: 1}

================================================================================

5. Final output kaise bana ? 
----------------------------

* Loop 7 complete hone ke baad freq dictionary mein ye data hai:

{1: 3, 2: 2, 3: 1, 4: 1}

Isliye:
-------
print(freq)

Output:
{1: 3, 2: 2, 3: 1, 4: 1}

Is output ka meaning:
---------------------
1 ki frequency = 3
2 ki frequency = 2
3 ki frequency = 1
4 ki frequency = 1

--------------------------------------------------------------------------------

Notes ke liye sabse important concept:
--------------------------------------
- Dictionary mein key number ko represent karti hai.
- Dictionary mein value us number ki frequency batati hai.
- if tab chalta hai jab number pehle se dictionary mein ho.
- else tab chalta hai jab number pehli baar aaye.
- Ek loop complete hone ke baad hi agla number num mein aata hai.