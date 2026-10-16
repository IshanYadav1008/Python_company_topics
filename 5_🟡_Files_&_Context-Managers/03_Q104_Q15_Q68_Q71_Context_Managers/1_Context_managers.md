# Context Manager kya hota hai ?

* Context Manager Python ka ek mechanism hai jo kisi kaam ko shuru 
  karne se lekar khatam karne tak resource ko manage karta hai.

Jaise file ke case mein:
------------------------
1. File open karna.
2. File mein data likhna ya read karna.
3. Kaam khatam hone par file close karna.

- Context Manager ye process manage karta hai, taaki tumhe cleanup 
  manually karne ki zaroorat na pade.

-------------------------------------------------------------------------------

# Example dekho

Bina Context Manager ke:
------------------------
file = open("data.txt", "w")
file.write("Hello Rahul")
file.close()

- Yahan file ko khud close karna padta hai.

-------------------------------------------------------------------------------

Context Manager ke saath:
-------------------------
with open("data.txt", "w") as file:
    file.write("Hello Rahul")

- Yahan Python file ko automatically close kar deta hai.

===============================================================================

Real-life example
-----------------
* Socho tum ek room mein jaate ho:

- Room ka darwaza kholna                  = resource ready karna.
- Room mein kaam karna                    = resource use karna.
- Kaam khatam hone par darwaza band karna = cleanup.

* Context Manager bhi isi tarah resource ke use ko manage karta hai.

-------------------------------------------------------------------------------

* Context Manager kaise kaam karta hai ?

__enter__()
Kaam shuru karne ki preparation
       |
with block
Apna actual kaam karo
       |
__exit__()
Kaam khatam hone par cleanup

* Ye methods context manager ke through with statement par automatically 
  call hote hain.

Bas ek line yaad rakho: Context Manager kisi resource ko use karne aur 
                        kaam khatam hone par use properly release karne 
                        ka process manage karta hai.