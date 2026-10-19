1. File Handling kya hai ?

- File Handling ka matlab hai Python ki help se file ko create karna, 
  usme data likhna, data read karna aur file ko manage karna.

- Jaise tumhare computer mein data.txt naam ki file hai. Python se tum 
  us file mein text likh sakte ho aur baad mein us text ko read bhi kar 
  sakte ho.

===============================================================================

2. open() kya hai ?

- open() Python ka function hai jo file ko kholne ke liye use hota 
  hai.

=> file = open("data.txt", "r")

- "data.txt" — file ka naam.
- "r"        — file ko read karne ke liye open karna.
- file       — file object, jiske through hum file par operations 
               karte hain.

===============================================================================

3. File Modes (r, w, a):

- File mode batata hai ki file ke saath kya kaam karna hai.

Mode	Meaning	   Kaam
-------------------------------------------------------------
"r"	    Read	   File ka data padhna
-------------------------------------------------------------
"w"	    Write	   Data likhna; purana content overwrite ho 
                   sakta hai
-------------------------------------------------------------
"a"	    Append	   File ke end mein naya data jodna
-------------------------------------------------------------

* Yaad rakho: "r" mode mein file exist nahi karti, toh FileNotFoundError 
  aa sakta hai. "w" aur "a" mode mein file nahi hai, toh Python aam taur 
  par nayi file bana deta hai.

===============================================================================

4. read(), write(), close() kya hain ?

write() — Data likhna
---------------------
file = open("data.txt", "w")
file.write("Hello Python")
file.close()

- File mein Hello Python likh dega.

--------------------------------------------------------

read() — Data padhna
--------------------
file = open("data.txt", "r")
print(file.read())
file.close()

- File ka content screen par print karega.

--------------------------------------------------------

close() — File band karna
-------------------------
=> file.close()

- File ka kaam hone ke baad use close karta hai, taaki 
  resource release ho sake.

===============================================================================

5. Ek complete example:

- Is code ko dekho. Isme pehle data likha jaayega aur phir 
  wahi data read hoga.

CODE:
-----
# File mein data likhna
file = open("data.txt", "w")
file.write("My name is Rahul")
file.close()

# File se data padhna
file = open("data.txt", "r")
print(file.read())
file.close()

Output:
-------
My name is Rahul


Abhi bas ye 4 baatein yaad rakho:
---------------------------------
- File Handling    : File ke saath kaam karna.
- open()           : File kholna.
- read() / write() : Data padhna / likhna.
- close()          : File band karna.

* Pehle inhe achhe se samajh lo. Uske baad hum with padhenge, 
  jo file ko automatically close kar deta hai.

===============================================================================
-------------------------------------------------------------------------------
===============================================================================

Q) muje ye batao ki isme
file = open("data.txt", "w")
file.write("My name is Rahul")

- w or write dono ka exactly kya kaam hai ? or ye kaise file ko write 
  karne ke liye helpful hai ?

-------------------------------------------------------------------------------

Yaar, dono ka kaam alag hai. Ekdum simple example se samjho.

file = open("data.txt", "w")
file.write("My name is Rahul")

===============================================================================

1. "w" ka kya kaam hai ?

- "w" ka full form write mode hai. Ye open() ko batata hai ki file 
  ko likhne ke liye kholna hai.

=> file = open("data.txt", "w")

Is line mein Python:
--------------------
- data.txt file ko kholta hai.
- Agar file exist nahi karti, toh use create karta hai.
- Agar file pehle se hai, toh uska purana content hata 
  kar naya content likhne ke liye ready karta hai.

* Matlab "w" file ko write karne ke liye ready karta hai.

===============================================================================

2. write() ka kya kaam hai ?

=> file.write("My name is Rahul")

- write() file ke andar actual data likhta hai.
- Yahan "My name is Rahul" woh text hai jo file 
  mein save hoga.
- Matlab write() actual text file mein likhta hai.

===============================================================================

3. Dono milkar kaise kaam karte hain ?

Step 1: open("data.txt", "w")
File khulti hai aur writing ke liye ready hoti hai.
            |
            |
Step 2: write("My name is Rahul")
Text file mein likha jaata hai.
            |
            |
        data.txt
     My name is Rahul

- Ek important baat: file ko properly close karna chahiye taaki 
                     pending data save ho sake.

* file = open("data.txt", "w")
  file.write("My name is Rahul")
  file.close()

- Bas ye difference yaad rakho: "w" batata hai kis mode mein file 
  kholni hai, aur write() batata hai file mein kya likhna hai.

===============================================================================

* "r" ka matlab sirf read karna hai. Isliye file.write() karne par Python       UnsupportedOperation exception dega.

Result: File mein text write nahi hoga.

* "w" ka matlab write karna hai, read karna nahi. Isliye file.read() par 
  bhi UnsupportedOperation exception aayegi.

* Ek aur zaroori baat: "w" mode file ko open karte hi uska purana content 
                       mita deta hai.