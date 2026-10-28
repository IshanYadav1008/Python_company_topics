* Bhai, ab hum Performance using Profiling seekhenge. Ye Python optimization 
  ka bahut important topic hai. Isse tumhe pata chalega ki tumhare code mein 
  exactly kaunsa part slow hai aur kahan improvement karni chahiye.

Lesson 3: Performance using Profiling
-------------------------------------

1. Profiling kya hoti hai?

- Maan lo tumne ek Python application banayi hai, lekin woh slow chal rahi 
  hai.

Tumhare code mein 3 functions hain:
-----------------------------------
- fetch_users()     — users ka data laata hai.
- calculate_total() — total amount calculate karta hai.
- send_email()      — emails bhejta hai.

* Tumhe nahi pata ki inmein se kaunsa function sabse zyada time le raha hai.

* Profiling ek technique hai jo measure karne mein help karti hai ki program 
  ke kaunse functions kitni baar call hue aur unmein kitna time laga.

----------------------------------------------------------------------------------

Example: Application ka time breakdown
--------------------------------------

* Maan lo profiler ne ye results diye:

fetch_users()
-------------
0.2s

calculate_total()
-----------------
0.1s

send_email()
------------
0.7s


Total: 1 second

* send_email() sabse zyada time le raha hai. Ab hum investigate 
  kar sakte hain ki ise improve karna possible hai ya nahi.

- Ye numbers sirf example ke liye hain, actual measurement nahi.

==================================================================================

2. Profiling aur normal timing mein kya difference hai ?
--------------------------------------------------------

- Timing    : Poore code ya kisi ek operation ko kitna time laga?

- Profiling : Program ke alag-alag functions mein time kahan spend ho raha hai?

Example     : Stopwatch tumhe batata hai ki race 10 seconds mein khatam hui. 
              Profiler tumhe batane mein help karta hai ki race ke alag-alag 
              sections mein kitna time laga.

==================================================================================

3. Python mein profiling kaise karte hain ?
-------------------------------------------

* Python mein built-in module hai cProfile. Isse tum apne program ke functions 
  ka performance analyze kar sakte ho.

- Chalo ek simple example dekhte hain.

Step 1: Ek program banao
------------------------
def calculate_total():
    total = 0

    for number in range(1_000_000):
        total += number

    return total

def greet_users():
    for _ in range(1000):
        message = "Hello user"

def main():
    calculate_total()
    greet_users()

main()

- Abhi hum nahi jaante ki calculate_total() aur greet_users() mein se 
  kaunsa zyada time le raha hai.

----------------------------------------------------------------------------------

Step 2: cProfile se profiling karo
----------------------------------

* Upar wale code ko app.py naam ki file mein save karo. Phir terminal 
  mein run karo:

=> python -m cProfile -s cumtime app.py

* Python program run karega aur profiling report dikhayega.

Report mein kuch important columns milenge:
-------------------------------------------

Column	  Simple meaning
-------------------------------------------------------------------
ncalls	  Function kitni baar call hua
-------------------------------------------------------------------
tottime	  Function ke apne code mein kitna time laga, 
          uske dusre function calls ka time chhodkar
-------------------------------------------------------------------
cumtime	  Function aur uske andar call hue functions ka total time
-------------------------------------------------------------------
percall	  Per call average time
-------------------------------------------------------------------

- Important: tottime aur cumtime alag hain. Agar function doosre 
             functions call karta hai, toh cumtime mein unka time 
             bhi include hota hai.

==================================================================================

4. Profiling se optimization kaise karte hain ?
-----------------------------------------------

* Maan lo profiling report mein pata chala ki calculate_total() sabse 
  zyada time le raha hai.

* Ab tum us function ko investigate karoge, phir improvement karne ke 
  baad dobara profiling karoge.

Step 1: Profile
---------------------
- Pata lagao ki slow function kaunsa hai.

Step 2: Optimize
---------------------
- Slow function ke algorithm, data structures ya unnecessary work ko 
  improve karo.

Step 3: Profile again
---------------------
- Check karo ki improvement se actual performance better hui ya nahi.

* Har baar slow function ko rewrite karna zaroori nahi. Ho sakta hai 
  slow function kisi external API ya database ka wait kar raha ho; 
  aise case mein solution alag hoga.

==================================================================================

5. time.perf_counter() aur cProfile kab use karein ?
----------------------------------------------------

Tool	             Kab use karna hai
------------------------------------------------------------
time.perf_counter()	 Kisi operation ka elapsed time measure 
                     karna ho.
------------------------------------------------------------
cProfile	         Pata lagana ho ki program ke andar time 
                     kahan spend ho raha hai.
------------------------------------------------------------

Example:
--------
import time

start  = time.perf_counter()
result = sum(range(1_000_000))
end    = time.perf_counter()
print("Time taken:", end - start, "seconds")

- Ye batayega ki calculation mein kitna elapsed time laga. cProfile 
  use karoge toh function-level details bhi mil sakti hain.

==================================================================================

6. Ab tumhari practice:
-----------------------

Question: Tumhari Python application slow hai. Usmein 20 functions hain 
          aur tumhe nahi pata ki kaunsa function sabse zyada time le raha 
          hai.

          Sabse useful next step kya hai?

ANS) cProfile run karke bottleneck identify karna.

- Correct! Pehle bottleneck identify karo, phir usko optimize karke dobara 
  measure karo.

**IMP**
* Yaad rakhna, bhai: Profiling ka purpose code ko automatically optimize 
                     karna nahi hai. Iska purpose hai tumhe evidence dena 
                     ki performance improve karne ke liye sabse pehle kahan 
                     kaam karna chahiye.