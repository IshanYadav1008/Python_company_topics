* Yaar, ab with statement samjhte hain. Ye file handling mein close() 
  manually likhne ki zaroorat kam kar deta hai.

1. with open() kya hai ?
------------------------
* Normally hum file aise open karte hain:

CODE:
-----
file = open("data.txt", "w")
file.write("Hello Rahul")
file.close()

- Yahan close() humein khud likhna padta hai.

--------------------------------------------------------------------------------

Lekin with use karne par:
-------------------------
with open("data.txt", "w") as file:
    file.write("Hello Rahul")

* Python with ke andar ka kaam khatam hone par file automatically 
  close kar deta hai.

================================================================================

2. Ye kaise kaam karta hai ?
----------------------------

1. with open(...)   // File open hoti hai.


2. as file          // File ko file naam ke variable se access karte hain.


3. Indented code    // File par read ya write ka kaam hota hai.


4. Block khatam     // Python file ko automatically close kar deta hai, 
                       exception aane par bhi.

================================================================================

3. with se file read kaise karein ?
-----------------------------------

CODE:
-----
with open("data.txt", "r") as file:
    content = file.read()
    print(content)

--> "r"         — file read karne ke liye.
--> as file     — file ko variable ka naam diya.
--> file.read() — file ka data padha.
--> Block khatam hote hi file automatically close ho gayi.

================================================================================

4. Ek important baat:
---------------------

- with ke block ke bahar file ka use karne ki koshish karoge, toh 
  closed file par operations karne se ValueError aa sakta hai.

- Exam ke liye definition: The with statement is used to manage 
  resources such as files and ensures that they are properly 
  closed after the block finishes, even if an exception occurs.

* Abhi bas ye yaad rakho: with open() = file open karo, kaam karo, 
  aur automatically close kar do.

================================================================================
--------------------------------------------------------------------------------
================================================================================

