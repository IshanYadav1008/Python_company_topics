* Yaar, File Exception ka matlab hai file ke saath kaam karte 
  waqt aane wali exception — jaise file na milna ya file ko 
  access na kar paana.

1. Common File Exceptions:
--------------------------

Exception	           Kab aati hai?
--------------------------------------------------------------------
FileNotFoundError	   Jab file nahi milti
--------------------------------------------------------------------
PermissionError	       Jab file access karne ki permission nahi hoti
--------------------------------------------------------------------
IsADirectoryError	   Jab file ki jagah directory ko file ki tarah 
                       open karte hain.
--------------------------------------------------------------------
OSError	               Jab file ya operating system se related koi 
                       problem hoti hai.
--------------------------------------------------------------------

============================================================================

2. Example — FileNotFoundError:

* Maan lo data.txt naam ki file exist nahi karti.

CODE:
-----
try:
    file = open("data.txt", "r")
    print(file.read())

except FileNotFoundError:
    print("File nahi mili!")

Kya hoga ?
----------
1. Python data.txt ko open karne ki koshish karega.
2. File nahi mili, toh FileNotFoundError raise hogi.
3. except us exception ko handle karega.
4. Output hoga: File nahi mili!

============================================================================

3. File Exceptions handle karna kyun zaroori hai ?

* Agar exception handle nahi karoge, toh program error ke saath 
  ruk sakta hai. try-except se hum error ko handle karke program 
  ko aage chalne ka mauka de sakte hain.

============================================================================

4. Best practice:

* File open karne ke liye with open() use karna achha hota hai:

CODE:
-----
try:
    with open("data.txt", "r") as file:
        print(file.read())

except FileNotFoundError:
    print("File nahi mili!")

except PermissionError:
    print("File access karne ki permission nahi hai!")

* with ka fayda          : file ka kaam complete hone par file automatically 
                           close ho jaati hai.
                           
Exam ke liye definition  : File exceptions are exceptions that occur while 
                           performing file operations, such as opening, reading, 
                           or writing a file. They can be handled using try-except 
                           blocks.