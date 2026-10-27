1. Unit Testing kya hota hai ?
------------------------------

* Unit Testing ek process hai jisme hum program ke chhote-chhote parts 
  (functions ya methods) ko alag se test karte hain, taaki pata chale 
  ki woh sahi kaam kar rahe hain ya nahi.

* Simple example : Maan lo tumne do numbers ko add karne ke liye function 
                   banaya. Ab tum check karoge ki 2 + 3 ka result 5 aa 
                   raha hai ya nahi. Isi ko Unit Testing kehte hain.

CODE:
-----
def add(a, b):
    return a + b

print(add(2, 3))

Output:
-------
5

- Yahan humne function ka result check kiya. Ye manual checking hai; ise 
  automated test se bhi check kar sakte hain.

Advantages of Unit Testing:
---------------------------
- Program mein errors (bugs) find karne mein help karta hai.
- Code sahi kaam kar raha hai ya nahi, ye check karta hai.
- Code ko modify karne ke baad dobara test karna easy hota hai.
- Software ki quality improve hoti hai.

===============================================================================

2. Unit Testing using unittest kya hota hai ?
---------------------------------------------

* Python mein unittest ek built-in module hai, jiska use automated tests 
  likhne aur run karne ke liye kiya jata hai.

* Matlab, har baar manually output check karne ki jagah Python khud check 
  kar sakta hai ki expected result aur actual result same hain ya nahi.

Example:
--------
import unittest

def add(a, b):
    return a + b

class TestAddition(unittest.TestCase):

    def test_add(self):
        self.assertEqual(add(2, 3), 5)

if __name__ == "__main__":
    unittest.main()

Output:
-------
Ran 1 test
OK

-------------------------------------------------------------------------------

Is code ko simple way mein samjho
---------------------------------

Code            	                    Meaning
-------------------------------------------------------------------------------
import unittest	                        Testing module import karta hai.
-------------------------------------------------------------------------------
def add(a, b)	                        Do numbers ko add karta hai.
-------------------------------------------------------------------------------
class TestAddition(unittest.TestCase)	Testing ke liye class banata hai.
-------------------------------------------------------------------------------
def test_add(self)	                    Test function define karta hai.
-------------------------------------------------------------------------------
self.assertEqual(add(2, 3), 5)	        Check karta hai ki result 5 hai ya nahi.
-------------------------------------------------------------------------------
unittest.main()	                        Test ko run karta hai.
-------------------------------------------------------------------------------

- Yaad rakho : assertEqual(expected, actual) dono values ko compare karta hai. 
               Agar values same hain, test pass hota hai; warna fail hota hai.

===============================================================================

3. Dono mein difference kya hai ?
---------------------------------

Unit Testing	                        unittest
------------------------------------------------------------------------------
Testing karne ka concept hai.	        Python ka testing module hai.
------------------------------------------------------------------------------
Manual ya automated ho sakti hai.	    Automated tests likhne aur run karne 
                                        ke kaam aata hai.
------------------------------------------------------------------------------
Function ya method ko test karte hain.	Function ya method test karne ke liye 
                                        tools deta hai.
------------------------------------------------------------------------------