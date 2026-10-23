
1. Regular Expression (Regex) kya hota hai ?
--------------------------------------------

* Regex ek pattern hota hai, jiska use hum text ke andar kisi specific 
  cheez ko search, check, extract ya replace karne ke liye karte hain.

Maan lo tumhare paas ye text hai:
---------------------------------
My phone number is 9876543210.
My age is 22.
My pin code is 452001.

* Ab tumhe is text mein se sirf numbers find karne hain.

* Bina Regex ke tumhe text ko manually check karna pad sakta hai. 
  Regex se tum ek pattern bana sakte ho jo numbers ko identify 
  kar de.

Example:
--------
import re

text   = "My age is 22 and my pin code is 452001"
result = re.findall(r"\d+", text)
print(result)

Output:
-------
['22', '452001']

* Yahan Regex ne text mein se numbers ke groups nikaal diye.

- re        = Python ka module jo Regex operations perform karta hai.
- \d        = kisi bhi digit (0–9) ko represent karta hai.
- +         = ek ya usse zyada baar aane ko represent karta hai.
- findall() = pattern se match hone wali sabhi values ki list deta hai.

Dhyan do: Regex khud Python ka function nahi hai. Regex pattern banane 
          ka tarika hai, aur Python mein re module us pattern ko use 
          karta hai.

=====================================================================================

2. Regex ki zaroorat kyu hoti hai ?
-----------------------------------

* Socho tum ek website bana rahe ho jahan users apna naam, email aur 
  phone number enter karte hain.

Tumhe check karna hai:
----------------------
- Email mein @ hai ya nahi.
- Text mein phone number hai ya nahi.
- Password mein digits hain ya nahi.
- Sentence mein koi specific word hai ya nahi.

* Har possible text ko manually check karna mushkil ho sakta hai. 
  Regex se tum rules define kar sakte ho aur un rules ke according 
  text check kar sakte ho.

Search
------
- Text mein kisi pattern ko dhoondhna.

Extract
-------
- Text mein se numbers, dates ya email addresses nikaalna.

Validate
--------
- Check karna ki input kisi expected pattern ko follow karta hai ya nahi.

Replace
-------
- Text ke kisi matching part ko doosre text se badalna.

=====================================================================================

3. Regex kaisa hota hai ?
-------------------------

* Regex mein hum kuch special symbols ka use karke pattern banate hain.

+---------+------------------------------------------+------------------+
| Pattern | Meaning                                  | Example match    |
+---------+------------------------------------------+------------------+
| \d      | Koi bhi digit (0–9)                      | 7                |
| \w      | Letter, digit ya underscore              | A, 7, _          |
| \s      | Whitespace, jaise space                  | " "              |
| +       | Ek ya zyada repetitions                  | 123              |
| *       | Zero ya zyada repetitions                | abc, 123         |
| ?       | Zero ya ek repetition                    | color, colour    |
| [abc]   | a, b ya c mein se koi ek                 | b                |
| ^       | String ki shuruaat                       | ^Hello           |
| $       | String ka end                            | end$             |
| .       | Koi ek character, newline ko chhodkar    | a.c → abc        |
+---------+------------------------------------------+------------------+

* In sabhi symbols ko ek saath use karke powerful patterns bana sakte ho. 
  Abhi saare symbols yaad karne ki zaroorat nahi hai; pehle basic examples 
  samjho.

=================================================================================

4. Regex practically kaha use hota hai ?
----------------------------------------

* Chalo real-life examples dekhte hain.

Use Case 1: Text mein numbers find karna
----------------------------------------
import re
text = "I have 25 apples and 10 mangoes"
print(re.findall(r"\d+", text))

Output:
-------
['25', '10']

- Kaha use hoga? Invoices, bills, documents aur text files 
  se numbers nikaalne mein.

---------------------------------------------------------------------------------

Use Case 2: Email addresses extract karna
-----------------------------------------
import re
text    = "Contact us at help@example.com"
pattern = r"[\w.-]+@[\w.-]+\.\w+"
print(re.findall(pattern, text))

Output:
-------
['help@example.com']

- Kaha use hoga? Documents ya messages mein se email addresses 
  collect karne mein.

- Note: Ye ek basic email pattern hai; har valid email format 
        ko cover nahi karta.

---------------------------------------------------------------------------------

Use Case 3: Input check karna
-----------------------------

* Maan lo user ko 6-digit PIN enter karna hai.

CODE:
-----
import re

pin = "452001"

if re.fullmatch(r"\d{6}", pin):
    print("Valid PIN format")
else:
    print("Invalid PIN format")

Output:
-------
Valid PIN format

- Yahan \d{6} ka matlab hai exactly 6 digits.

- fullmatch() check karta hai ki poori string 
  pattern se match karti hai ya nahi.

---------------------------------------------------------------------------------

Use Case 4: Text mein word replace karna
----------------------------------------
import re

text   = "Python is easy. Python is powerful."
result = re.sub(r"Python", "Java", text)
print(result)

Output:
-------
Java is easy. Java is powerful.

* Kaha use hoga? Text cleaning, formatting aur unwanted words 
                 ko replace karne mein.
                
---------------------------------------------------------------------------------

Use Case 5: Extra spaces hatana
-------------------------------
import re

text   = "Hello     World"
result = re.sub(r"\s+", " ", text)
print(result)

Output:
-------
Hello World

- Yahan \s+ ek ya zyada whitespace characters ko match karta hai.

- Kaha use hoga? Data cleaning aur messy text ko clean karne mein.

=================================================================================

5. Regex + Use Cases — Interview mein kaise batana hai ? 
--------------------------------------------------------

* Agar interviewer poochhe, "What is Regular Expression and 
  what are its use cases?", toh tum is tarah answer de sakte 
  ho:

Interview answer (simple English)
---------------------------------
* "Regular Expression, or Regex, is a sequence of characters 
   used to define a search pattern. It helps us search, match, 
   extract, validate, and replace text.

* In Python, we use the re module to work with regular expressions.

* Common use cases include extracting email addresses, finding 
  numbers, validating input formats, cleaning text, and replacing 
  specific patterns."

=================================================================================

6. Regex aur Python re module mein kya difference hai ?
-------------------------------------------------------

* Ye difference samajhna important hai, kyunki tumhare  
  syllabus mein dono topics hain.

Regex	                             re module
------------------------------------------------------------------------------
Pattern banane ka tarika	         Python ki built-in library
------------------------------------------------------------------------------
Example: r"\d+"	                     Example: re.findall()
------------------------------------------------------------------------------
Batata hai kya search karna hai	     Batata hai pattern ko kaise use karna hai
------------------------------------------------------------------------------

Example:
--------
import re

text    = "Age 25"
pattern = r"\d+"
result  = re.findall(pattern, text)
print(result)

Output:
-------
['25']

- Is code mein r"\d+" Regex pattern hai, jabki re.findall() 
  Python ka function hai.

* Sabse important baat: Regex ka use tab karo jab text mein kisi 
                        pattern ko identify ya manipulate karna 
                        ho. Har string operation ke liye Regex 
                        zaroori nahi hai.

=================================================================================

# Ab samjho r"\d+" mein r kya hai ??

Example code:
-------------
import re

text   = "My age is 25"
result = re.findall(r"\d+", text)
print(result)

Output:
-------
['25']

Is ek line ko 4 parts mein samjho:
----------------------------------
=> re.findall(r"\d+", text)

① re
-----
--> Python ka built-in module hai jo Regex ke saath kaam karta hai.

② findall()
-----------
--> Text mein pattern ke saare matches dhoondhkar list mein deta hai.

③ r"\d+"
--------
--> Ye Regex pattern hai. Ismein r ka matlab hai raw string.

④ text
-------
--> Woh actual string jismein pattern search karna hai.

---------------------------------------------------------------------------------

Raw string r ka kaam kya hai ?
------------------------------
* Python mein r string ke aage lagane se backslash \ ko aam taur par 
  raw character ki tarah treat kiya jaata hai, taaki Python usse pehle 
  escape sequence samajhne ki koshish na kare.

Example:
--------
=> print("\n")

- Yahan \n ka matlab newline hai, isliye output mein line break aata 
  hai.

Lekin:
------
=> print(r"\n")

Output:
-------
\n

- Raw string mein \n literal backslash aur n rehta hai.

---------------------------------------------------------------------------------

Regex mein r kyu use karte hain ?
---------------------------------
* Kyunki Regex mein \d, \w, \s jaise patterns mein backslash ka special 
  meaning hota hai. r likhne se in patterns ko likhna aur samajhna 
  aasaan ho jaata hai.

r"\d+"    # Recommended
"\\d+"    # Iska equivalent normal Python string

--> Dono yahan same Regex pattern dete hain.

Aur \d+ ka matlab ?
-------------------
- \d = koi bhi digit, jaise 0 se 9.
- +  = ek ya zyada digits/characters ke matches.

* Isliye "My age is 25" mein \d+ ko 25 milta hai.

Final shortcut yaad rakho:
--------------------------
r         = raw string, 
\d+       = ek ya zyada digits, 
findall() = saare matches ki list.