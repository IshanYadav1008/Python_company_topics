🔍 Binary Search Python mein
----------------------------

* Binary Search ek searching technique hai jo sorted list mein kisi 
  element ko jaldi find karti hai. Ye har step mein list ka aadha 
  hissa eliminate kar deti hai.

Python code:
------------

def binary_search(arr, target):
    low = 0
    high = len(arr) - 1

    while low <= high:
        mid = (low + high) // 2

        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1

    return -1

arr = [10, 20, 30, 40, 50, 60, 70]
target = 50

result = binary_search(arr, target)

if result != -1:
    print("Element found at index:", result)
else:
    print("Element not found")


Output:
-------
Element found at index: 4

----------------------------------------------------------------------------------

Code ko samjho
--------------
Maan lo list hai: [10, 20, 30, 40, 50, 60, 70]

Step 1
------
10     20     30     40     50     60     70

- Middle element 40 hai. Humein 50 chahiye, isliye left wala hissa 
  hata denge.

Step 2
------
50     60     70

- Middle element 60 hai. 50 chhota hai, isliye right wala hissa hata 
  denge.

Step 3
------
50 — Found!

Important points:
----------------
- low             = starting index
- high            = last index
- mid             = middle index
- //              = integer division
- return -1       = element nahi mila
- Time complexity : \(O(\log n)\)
- Condition       : List sorted honi chahiye.

==================================================================================
----------------------------------------------------------------------------------
==================================================================================

Doubt:1
-------
jab condition fullfill ho jayegi toh ye line chalegi
        if arr[mid] == target:
            return mid

kyuki yhi fullfill hogi lekin return jab hogi value toh vo jaeygi kaha 
return ho kar kyuki jaati wqaha hai jaha se funciton cal kiya ho lekin 
ye while ka retun hai or ye kaha jyega vo muje smj nhi aa rha or phir 
ye retun return -1 kyu likha hai ye bhi smj nhi aaya.

----------------------------------------------------------------------------------

Solution:
---------
* Bhai, ye Python ka bahut important concept hai. ❤️ Tumhara doubt bilkul 
  sahi hai. Chalo ekdum basic se samajhte hain ki return mid kahan jaata
  hai aur return -1 kyun likha hai.

1. Sabse pehle function ko dekho:
---------------------------------
def binary_search(arr, target):
    low = 0
    high = len(arr) - 1

    while low <= high:
        mid = (low + high) // 2

        if arr[mid] == target:
            return mid

    return -1

result = binary_search([10, 20, 30, 40, 50], 30)
print(result)

Output:
-------
2

- Ab tumhara main question: return mid ki value jaati kahan 
  hai ?

==================================================================================

2. return value ko function call wali jagah bhejta hai:
------------------------------------------------------

Ye line dekho:
--------------
=> result = binary_search([10, 20, 30, 40, 50], 30)

- Yahan binary_search() function call hua hai.

* Jab function ke andar return mid execute hota hai aur 
  mid = 2 hota hai, toh Python:

1. return mid ko execute karta hai.
2. mid ki value 2 lekar function ko turant band kar deta hai.
3. Wapas usi jagah aata hai jahan function call hua tha.
4. 2 ko result variable mein store kar deta hai.

----------------------------------------------------------------------------------

Isko aise imagine karo:
-----------------------
Function call
result = binary_search(...)
        |
        |
Function ke andar
return mid
mid = 2
        |
        |
Function se bahar
result = 2
        |
        |
print(result)
Output: 2

- Yaad rakho: return ka relation while loop se nahi, function se hota 
  hai. return loop ke andar likha ho ya if ke andar, woh poore function 
  ko terminate kar deta hai.

==================================================================================

3. Phir return -1 kyun likha hai ?
----------------------------------

Code mein dekho:
----------------
while low <= high:
    mid = (low + high) // 2

    if arr[mid] == target:
        return mid

return -1

Yahan do alag situations hain:
------------------------------
- return mid: Jab element mil jaaye, uska index return kar 
  do.

- return -1: Jab element nahi mile aur while loop khatam ho 
  jaaye, toh -1 return kar do.

Example:
--------
arr    = [10, 20, 30, 40, 50]
result = binary_search(arr, 99)
print(result)

Output:
-------
-1

* 99 list mein hai hi nahi. Isliye search karte-karte low > high ho 
  jaayega aur while loop ruk jaayega. Uske baad Python loop ke 
  neeche aayega aur return -1 execute karega.

* Ek important baat: Python mein -1 likhna compulsory nahi hai. Hum 
                     None bhi return kar sakte hain. Binary Search 
                     mein -1 ek common convention hai, jo batata hai 
                     ki element nahi mila.

==================================================================================

4. Ab khud try karo:
--------------------

* List hai [10, 20, 30, 40, 50] aur humne call kiya:

=> result = binary_search(arr, 40)

- Agar function ke andar return mid execute hota hai 
  aur mid = 3 hai, toh return mid ki value kahan 
  jaayegi ?

ANS) result variable mein, function call wali jagah par.

Bilkul sahi!
------------
- return 3 ki value function call wali jagah par jaayegi aur 
  result = 3 ho jaayega.

==================================================================================

📘 Python Notes: Binary Search ka Concept:
------------------------------------------

1. Binary Search kya hai ?
--------------------------
* Binary Search ek searching technique hai jismein hum sorted list ke 
  middle element ko check karte hain aur har step mein search area ko 
  aadha kar dete hain.

Example: Humein list mein 50 find karna hai.
--------------------------------------------
[10, 20, 30, 40, 50, 60, 70]

- List sorted honi chahiye, yaani elements ascending ya descending order 
  mein arranged hon.

----------------------------------------------------------------------------------

2. Binary Search ki zaroorat kyun hai ?
---------------------------------------

Do tarike samjho:
-----------------
- Linear Search : Ek-ek element check karta hai.
- Binary Search : Middle element check karta hai aur decide 
                  karta hai ki target left side mein hai ya 
                  right side mein.

* Isliye Binary Search badi sorted lists mein zyada efficient hoti hai.

----------------------------------------------------------------------------------

3. Binary Search ka logic kaise sochna hai ? 
--------------------------------------------

* Har step par khud se 3 questions poochho:

1. Middle element kaunsa hai?
2. Target middle se chhota hai, bada hai, ya equal hai?
3. Agli baar search kis hisse mein karna hai?

Case 1: Middle element target ke equal hai

=> arr[mid] == target

-  Element mil gaya. return mid se uska index return kar do.

<------------------------------------------------------------->

Case 2: Middle element target se chhota hai

=> arr[mid] < target

- Target right side mein hoga. low = mid + 1 karke left side 
  ko ignore kar do.

<------------------------------------------------------------->

Case 3: Middle element target se bada hai

arr[mid] > target

Target left side mein hoga. high = mid - 1 karke right side 
ko ignore kar do.

----------------------------------------------------------------------------------

4. Har variable ka kaam:
------------------------

Variable	 Meaning
--------------------------------------------
arr	         Jis list mein search karna hai
target	     Jo element find karna hai
low	         Search area ka starting index
high	     Search area ka ending index
mid	         Search area ka middle index
--------------------------------------------

* low aur high kaise initialize hote hain ?

low  = 0
high = len(arr) - 1

low  = 0 kyunki list ka pehla index 0 hai.
high = len(arr) - 1 kyunki list ka last index, 
       total elements se ek kam hota hai.

Middle index kaise nikalte hain ?
---------------------------------
=> mid = (low + high) // 2

- low aur high ka sum karke 2 se integer division karte 
  hain, taaki middle index mil sake.

----------------------------------------------------------------------------------

5. Poora Python code:
---------------------

def binary_search(arr, target):
    low = 0
    high = len(arr) - 1

    while low <= high:
        mid = (low + high) // 2

        if arr[mid] == target:
            return mid

        elif arr[mid] < target:
            low = mid + 1

        else:
            high = mid - 1

    return -1

arr    = [10, 20, 30, 40, 50, 60, 70]
result = binary_search(arr, 50)
print(result)

Output:
-------
4

----------------------------------------------------------------------------------

6. Code likhne ke peeche ka reason:
-----------------------------------

Code	                   Kyun likha ?
------------------------------------------------------------------------
low = 0        	           Search first index se start karna hai
high = len(arr) - 1	       Search last index tak karna hai
while low <= high	       Jab tak search area bacha hai, search chalao
mid = (low + high) // 2	   Middle element find karo
if arr[mid] == target	   Check karo ki target mil gaya ya nahi
low = mid + 1	           Target right side mein hai
high = mid - 1	           Target left side mein hai
return -1	               Target nahi mila
------------------------------------------------------------------------

----------------------------------------------------------------------------------

7. return mid aur return -1 mein difference:
--------------------------------------------

- return mid : Element milne par uska index function call wali jagah 
               return hota hai.

- return -1  : Jab while loop khatam ho jaaye aur element na mile, 
               toh -1 return hota hai.

* Important: return poore function ko end karta hai, sirf if ya while 
             ko nahi.

----------------------------------------------------------------------------------

8. Binary Search ki complexity:
-------------------------------

- Time complexity: \(O(\log n)\)

- Space complexity: \(O(1)\) — is iterative implementation mein extra 
                               space constant rehti hai.

----------------------------------------------------------------------------------

Final revision
--------------

* Binary Search likhne se pehle ye sequence yaad rakho:

1. Search area ki boundaries set karo.
2. Jab tak valid search area hai, loop chalao.
3. Middle index calculate karo.
4. Target mil jaaye toh index return karo.
5. Target bada ho toh right side mein jao.
6. Target chhota ho toh left side mein jao.
7. Search area khatam ho jaaye toh -1 return karo.

* Core concept: Binary Search mein hum poori list ko baar-baar check nahi 
                karte. Hum sirf low aur high update karke decide karte 
                hain ki agla search kis half mein hoga.