1. Performance kya hoti hai ?
-----------------------------

* Performance ka matlab hai ki tumhara Python program apna kaam kitni 
  jaldi aur kitne resources use karke complete karta hai.

* Maan lo tumhe 10,000 users ke records process karne hain.

- Program A: 10 seconds leta hai.
- Program B: 2 seconds leta hai.

* Agar dono correct result dete hain aur similar conditions mein test 
  hue hain, toh Program B ki performance better hai.

===============================================================================

2. Optimization kya hoti hai ?
------------------------------

* Optimization ka matlab hai code ko improve karna, taaki woh kam time 
  ya kam memory use karke wahi kaam sahi tarike se kare.

Example: Maan lo tumhe check karna hai ki koi number list mein hai ya 
         nahi.

Method 1: List use karna
------------------------
users = [101, 205, 310, 450, 520]
print(450 in users)  # True

- Python list mein elements ko ek-ek karke check kar sakta hai.

-------------------------------------------------------------------------------

Method 2: Set use karna
-----------------------
users = {101, 205, 310, 450, 520}
print(450 in users)  # True

- Set mein membership checking average case mein generally O(1) 
  hoti hai, jabki list mein O(n) hoti hai.

- Agar tumhe baar-baar check karna hai ki user ID exist karti 
  hai ya nahi, toh set useful ho sakta hai.

===============================================================================

3. Python script optimize karne ke common ways
----------------------------------------------

1. Unnecessary work kam karo
----------------------------
* Agar ek hi calculation baar-baar kar rahe ho, toh uska result save 
  karke reuse kar sakte ho.

2. Sahi data structure choose karo
----------------------------------
* Fast lookup ke liye set ya dict list se zyada suitable ho sakte hain.

3. Memory ka dhyan rakho
------------------------
* Bahut bada data ek saath load karne ke bajaye kabhi-kabhi data ko 
  chunks mein process karna better hota hai.

4. Pehle measure karo
---------------------
* Sirf dekhkar assume mat karo ki code slow hai. Execution time measure 
  karo aur phir improve karo.

===============================================================================

4. Chhota practical example:
----------------------------

* Maan lo tumhe list mein se sirf even numbers nikalne hain.

Normal code:
------------
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = []

for number in numbers:
    if number % 2 == 0:
        even_numbers.append(number)

print(even_numbers)

Output:
-------
[2, 4, 6]

-------------------------------------------------------------------------------

Shorter version:
----------------
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = [
    number for number in numbers
    if number % 2 == 0
]

print(even_numbers)

Output wahi hai: 
----------------
[2, 4, 6].

Dhyan do: shorter code ka matlab automatically faster code nahi hota. 
          List comprehension yahan concise hai, lekin performance ka 
          decision actual measurement aur use case ke basis par karna 
          chahiye.

===============================================================================

5. Ab tumhara chhota test
-------------------------

Question: Maan lo tumhe 1 lakh user IDs mein baar-baar check karna hai 
          ki koi ID exist karti hai ya nahi. Kaunsa option generally 
          better rahega?

B. Set mein IDs store karke search karna

Bilkul sahi!
------------
- set membership checking ke liye generally efficient hota hai, especially 
  jab baar-baar lookups karne hon.

* Aaj ka main takeaway: Optimization ka matlab sirf code ko chhota banana 
                        nahi hai. Matlab hai same correct kaam ko zaroorat 
                        ke hisaab se kam time aur resources mein karna.

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

* Ab next lesson mein samajhte hain ki optimization actually kaise kaam 
  karti hai, aur kab list ki jagah set use karna chahiye.

Lesson 2: List vs Set — Python code ko fast kaise banayein ?
------------------------------------------------------------

1. Ek real developer situation
------------------------------
- Maan lo tum ek e-commerce application bana rahe ho. Tumhare paas 1 lakh 
  registered user IDs hain aur har request par check karna hai ki user 
  registered hai ya nahi.

=> user_ids = [101, 102, 103, 104, 105]

Ab tumhe check karna hai:
-------------------------
=> print(104 in user_ids)

Output:
-------
True

- Ye bilkul sahi hai. Lekin Python list mein search karte waqt elements ko 
  ek-ek karke check kar sakta hai.

- Maan lo ID list ke bilkul end mein hai. Python ko kaafi elements check 
  karne pad sakte hain.

===============================================================================

2. Ab optimization karte hain
-----------------------------

* Isi data ko set mein store karo:

user_ids = {101, 102, 103, 104, 105}
print(104 in user_ids)

Output phir bhi:
----------------
True

-------------------------------------------------------------------------------

Lekin difference ye hai:
------------------------

List — list
-----------
- Membership check ka time aam taur par data ke size ke saath 
  badhta hai.

- O(n)

Set — set
---------
- Membership check average case mein bahut efficient hota hai.
- O(1) average

* Yahan n ka matlab hai collection mein kitne elements hain.

* O(1) ka matlab har situation mein exactly same time nahi hai. 
  Matlab average case mein lookup ka time collection ke size ke 
  saath proportionally nahi badhta.

===============================================================================

3. Practical example: Dono ko compare karo
------------------------------------------

# List
user_ids_list = [101, 102, 103, 104, 105]

if 105 in user_ids_list:
    print("User registered")

<-------------------------------------------------->

# Set
user_ids_set = {101, 102, 103, 104, 105}

if 105 in user_ids_set:
    print("User registered")


Dono ka output:
---------------
User registered

-------------------------------------------------------------------------------

Toh kaunsa use karna chahiye ?
------------------------------

- Agar order important hai, duplicates rakhne hain, ya index se access 
  karna hai — list useful hai.

- Agar unique values rakhni hain aur baar-baar membership check karna 
  hai — set useful hai.
  
* Ek important baat: agar tumhare paas pehle se list hai aur tum use set 
                     mein convert karte ho, toh conversion mein bhi time 
                     aur memory lagti hai. Bahut saare lookups karne par 
                     ye cost aksar worthwhile ho sakti hai.

===============================================================================

4. Khud run karke dekho:
------------------------

* Mini practice: User ID lookup

- User IDs ki quantity choose karo:
=> 1,000 users

- Kaunsi ID search karni hai ?
=> 1000

Generated data
--------------
1 se {count} tak user IDs

List result: User found
Set result : User found

Dono results same hain, kyunki dono same data search kar rahe hain. 
Performance ka difference samajhne ke liye bahut saare lookups par 
time measure karna padega.

===============================================================================

5. Next developer rule
-----------------------

* Code optimize karte waqt ye 3 questions poochho:

1. Kya main unnecessary kaam kar raha hoon?
2. Kya main is kaam ke liye sahi data structure use kar raha hoon?
3. Kya maine performance measure ki hai, ya sirf guess kar raha hoon?