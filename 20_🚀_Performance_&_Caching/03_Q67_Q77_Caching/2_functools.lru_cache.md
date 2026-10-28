* Bhai, ab tumne caching ka concept samajh liya hai, toh functools.lru_cache 
  samajhna kaafi easy hoga. Isko hum bilkul basic se, real Python examples 
  ke saath seekhenge.

1. functools.lru_cache kya hota hai ?
-------------------------------------

* functools.lru_cache Python ka built-in caching tool hai, jo function ke 
  results ko automatically save karta hai, taaki same inputs dobara aane 
  par function ko har baar execute na karna pade.

Pichhle lesson mein humne manually cache banaya tha:
----------------------------------------------------
cache = {}

def square(n):
    if n in cache:
        return cache[n]

    result = n * n
    cache[n] = result
    return result

- Har function ke liye aisa code likhna tedious ho sakta hai.

--------------------------------------------------------------------------------

* Python humein iska convenient solution deta hai: @lru_cache.

CODE:
-----
from functools import lru_cache

@lru_cache(maxsize=128)
def square(n):
    print("Calculating...")
    return n * n

print(square(5))
print(square(5))
print(square(6))

Output:
-------
Calculating...
25
25
Calculating...
36

- Notice karo, square(5) ke liye "Calculating..." sirf ek baar print hua. 
  Doosri baar cached result reuse hua.

================================================================================

2. Isko kyu use karte hain ?
----------------------------

* Maan lo tumhara function expensive kaam karta hai, jaise complex calculation 
  ya kisi data ka repeated processing.

Without caching:
----------------
- Same input aaya → function dobara chalega.
- Same calculation phir se hogi.
- Extra time lagega.

With lru_cache:
---------------
- Same input aaya → cached result mil sakta hai.
- Function ka body dobara execute nahi hota.
- Repeated work bach sakta hai.

Kaise kaam karta hai ?
----------------------

                        Function call: square(5)
                                  |
                             Cache check  
                                  |
        ---------------------------------------------------
            |                                        |
        Cache hit                                Cache miss
Saved result 25 return karo.          Function chalao aur result cache karo.

================================================================================

3. lru_cache naam ka matlab kya hai ?
-------------------------------------

* Iska full form hai Least Recently Used cache.

Naam ke teen parts samjho:
--------------------------
cache  : results save karna.

LRU    : jab cache full ho, toh jo result sabse lambe time se 
         use nahi hua, woh eviction ke liye select ho sakta 
         hai.

maxsize: cache mein maximum kitne recent call results rakhne 
         hain.

Example:
--------
from functools import lru_cache

@lru_cache(maxsize=3)
def square(n):
    print(f"Calculating {n}")
    return n * n

* Yahan maximum 3 different argument combinations ke results cache mein 
  rakhe ja sakte hain. Jab cache full ho aur naya result add karna ho, 
  toh least-recently-used entry ko hataya ja sakta hai.

* Agar maxsize=None set karoge, toh cache size par limit nahi rahegi — 
  isliye memory usage badh sakta hai.

================================================================================

4. Real project mein kahan use hota hai?
----------------------------------------

1. Expensive calculations
-------------------------
- Jaise recursive Fibonacci calculation, mathematical computations ya 
  repeated data transformations.

2. Repeated configuration processing
------------------------------------
- Jab same configuration input se baar-baar same result generate karna 
  ho.

3. Parsing ya processing
------------------------
- Jab same input string ko baar-baar parse karna costly ho aur output 
  stable ho.

Important: lru_cache har function ke liye suitable nahi hai. Function ke 
            arguments hashable hone chahiye, aur function ka result same 
            arguments ke liye safely reusable hona chahiye. Ye generally 
            pure calculations ke liye bahut useful hai.

* Aise function par caching avoid karo jo har call par current time, random 
  value, changing database state ya external side effects par depend karta 
  ho — jab tak tumne us behaviour ko carefully account na kiya ho.

================================================================================

5. lru_cache ke useful features:
--------------------------------

* Cache statistics check karna

CODE:
-----
from functools import lru_cache

@lru_cache(maxsize=128)
def square(n):
    return n * n

square(5)
square(5)
square(6)

print(square.cache_info())

Output ka format kuch aisa hoga:
--------------------------------
CacheInfo(hits=1, misses=2, maxsize=128, currsize=2)

<------------------------------------------------------------------>

* hits=1      : ek call par cached result mila.

* misses=2    : do different inputs ke liye function execute hua.

* maxsize=128 : maximum cache capacity.

* currsize=2  : abhi do entries cached hain.

<------------------------------------------------------------------>

Cache clear karna
-----------------
* Agar tum cache ke saved results clear karna chahte ho:

=> square.cache_clear()

- Ab next call par result dobara calculate hoga.

================================================================================

6. Ek important developer rule:
-------------------------------

* lru_cache use karne ka purpose sirf code ko short karna nahi, 
  balki repeated expensive work ko bachana hai.

Best workflow:
--------------
1. Identify karo ki same input baar-baar aa raha hai.

2. Check karo ki function ka result cache karna safe hai.

3. @lru_cache lagao.

4. cache_info() se dekho ki cache actually hit ho raha hai ya nahi.

5. Performance measure karke confirm karo ki improvement hui.