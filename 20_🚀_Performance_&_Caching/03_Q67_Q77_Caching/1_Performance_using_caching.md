1. Caching kya hoti hai ?
-------------------------

* Caching ka matlab hai kisi kaam ka result temporarily save kar lena, 
  taaki jab wahi result dobara chahiye ho toh kaam phir se na karna 
  pade.

* Maan lo tum ek shopping website bana rahe ho. Website par product ki 
  details baar-baar fetch karni padti hain.

Bina caching ke:
----------------
1. User product page open karta hai.
2. Application database se product details fetch karti hai.
3. Doosri baar wahi page open hota hai.
4. Application phir se database se wahi details fetch karti hai.

- Caching ke saath, agar saved data abhi bhi valid hai, toh application 
  us result ko reuse kar sakti hai.

--------------------------------------------------------------------------------

Bina caching vs caching
-----------------------

Bina caching
------------
- Har request par database se data fetch karna pad sakta hai.

Caching ke saath
----------------
- Result cache mein mil jaaye toh dobara fetch karne ki zaroorat 
  nahi.

================================================================================

2. Ek simple Python example:
----------------------------

* Maan lo tumhe kisi product ki price calculate karni hai.

CODE:
-----
def calculate_price(price, tax):
    print("Calculating price...")
    return price + (price * tax)

print(calculate_price(1000, 0.18))
print(calculate_price(1000, 0.18))

Output:
-------
Calculating price...
1180.0
Calculating price...
1180.0

- Dekho, same inputs hone ke baad bhi calculation dono baar hui.

- Ab imagine karo ki calculation bahut expensive hai — jaise 
  complex report banana ya kisi API se data fetch karna. Same 
  kaam baar-baar karna time waste kar sakta hai.

- Caching isi problem ko solve karne mein help karti hai.

================================================================================

3. Cache hit aur cache miss kya hain ?
--------------------------------------

* Ye caching ke do important terms hain.

Cache Hit
---------
- Required result cache mein mil gaya, toh saved result reuse kar liya.
- Usually faster

Cache Miss
----------
- Required result cache mein nahi mila, toh actual calculation ya data 
  fetch karna padega. Zaroorat ke hisaab se result cache mein save bhi 
  kiya ja sakta hai.

================================================================================

4. Real Python example: Caching manually
----------------------------------------

* Abhi lru_cache use nahi karenge. Pehle caching ka logic khud samjho.

CODE:
-----
cache = {}

def calculate_price(price, tax):
    key = (price, tax)

    if key in cache:
        print("Cache hit!")
        return cache[key]

    print("Cache miss! Calculating...")

    result = price + (price * tax)
    cache[key] = result

    return result

print(calculate_price(1000, 0.18))
print(calculate_price(1000, 0.18))
print(calculate_price(2000, 0.18))

Output:
-------
Cache miss! Calculating...
1180.0
Cache hit!
1180.0
Cache miss! Calculating...
2360.0

--------------------------------------------------------------------------------

Chalo samajhte hain:
--------------------
1. cache = {} ek empty dictionary hai jahan results store honge.

2. key   = (price, tax) inputs ko ek key mein combine karta hai.

3. Agar key cache mein hai, toh saved result return hota hai.

4. Agar key nahi hai, toh calculation hoti hai aur result cache 
   mein save hota hai.

* Dhyan do: yahan inputs tuple hain, kyunki dictionary ki key hashable honi 
            chahiye. Ye simple example hai; real applications mein cache 
            expiration, memory limits aur data freshness bhi handle karni 
            pad sakti hai.

================================================================================

5. Caching hamesha beneficial hoti hai kya ?
--------------------------------------------

* Nahi bhai. Ye important developer concept hai.

Situation	                                    Caching useful ?
--------------------------------------------------------------------------------
Same expensive calculation baar-baar karni ho	Haan, often
--------------------------------------------------------------------------------
Database se frequently requested data aata ho	Haan, agar data freshness manage 
                                                kar sako.
--------------------------------------------------------------------------------
Har baar inputs alag hon	                    Benefit kam ho sakta hai
--------------------------------------------------------------------------------
Data har second change hota ho	                Cache stale ho sakta hai
--------------------------------------------------------------------------------
Bahut saare unique results store ho rahe hon	Memory usage badh sakta hai
--------------------------------------------------------------------------------

* Ek aur important baat : cache ka result tabhi safely reuse karo jab tum sure ho 
                          ki same inputs ke liye result reuse karna valid hai. 
                          Agar function current time, changing database data ya 
                          kisi external state par depend karta hai, toh extra 
                          care chahiye.

================================================================================

6. Chhota practice question:
----------------------------

Question: Tumhari application ek complex report generate karti hai. Same 
          report ke liye same inputs baar-baar aa rahe hain, aur report 
          ka data is beech change nahi hua.

          Caching ka main benefit kya hoga?

ANS) Saved report result ko reuse karke time bachana.

     Bilkul sahi! Valid cached result ko reuse karne se expensive work 
     dobara karne ki zaroorat nahi pad sakti.

Aaj ka takeaway: Caching mein hum result ko save karke future mein reuse 
                 karte hain. Isse repeated expensive operations kam ho 
                 sakte hain aur application faster ho sakti hai — bas 
                 cache ki validity aur memory usage ka dhyan rakhna hai.