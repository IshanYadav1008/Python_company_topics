1. Web Scraping kya hoti hai ?
------------------------------

* Web Scraping ek technique hai jisme hum website se automatically data 
  collect karte hain, Python code ki help se.

- Maan lo tumhe kisi shopping website se 100 products ke naam aur prices 
  collect karne hain.

* Agar manually karoge, toh har product ko open karke naam aur price copy 
  karna padega. Lekin Web Scraping se Python ye kaam automatically kar 
  sakta hai.


Step 1: Website
---------------
Website par products, names aur prices hain.
        |
        |
Step 2: Python scraper
----------------------
Code website se HTML leta hai aur required data nikalta hai.
        |
        |
Step 3: Collected data
----------------------
Product names aur prices ko list, CSV ya database mein save 
kar sakte ho.

Web Scraping kahan use hoti hai ?
---------------------------------
- E-commerce websites se product prices collect karne mein.

- Public news websites se headlines collect karne mein.

- Job websites par available job listings gather karne mein.

- Research aur data analysis ke liye public information collect 
  karne mein.

* Dhyan rahe: website ki terms, access restrictions aur rate limits 
              follow karni chahiye.

=================================================================================

2. Simple Web Scraper kya hota hai ?
------------------------------------

* Simple Web Scraper ek basic Python program hota hai jo kisi webpage 
  se specific information nikalta hai.

- Example ke liye, hum ek webpage se uska title extract karenge.

Pehle required libraries install karo:
--------------------------------------
=> pip install requests beautifulsoup4

Ab Python code:
---------------
import requests
from bs4 import BeautifulSoup

url = "https://example.com"

response = requests.get(url, timeout=10)
response.raise_for_status()

soup = BeautifulSoup(response.text, "html.parser")

print(soup.title.get_text(strip=True))

Output:
-------
Example Domain

---------------------------------------------------------------------------------

# Code ko simple language mein samjho:

Code	                                     Kya karta hai ?
---------------------------------------------------------------------------------
import requests             	             Website se response lene ke liye 
                                             library.
---------------------------------------------------------------------------------
from bs4 import BeautifulSoup	             HTML ko parse karne ke liye library.
---------------------------------------------------------------------------------
requests.get(url)	                         Website ka page request karta hai.
---------------------------------------------------------------------------------
response.raise_for_status()	                 HTTP error hone par exception raise 
                                             karta hai.
---------------------------------------------------------------------------------
BeautifulSoup(response.text, "html.parser")	 HTML ko parse karta hai.
---------------------------------------------------------------------------------
soup.title.get_text(strip=True)	             Page ka title nikalta hai.
---------------------------------------------------------------------------------

- Is example mein example.com ek demo website hai. Real website par page ka 
  content aur response alag ho sakta hai.

=================================================================================

3. Web Scraping aur Simple Web Scraper mein difference
------------------------------------------------------

- Web Scraping       : Data collect karne ki technique ya process.
- Simple Web Scraper : Us process ko perform karne wala basic program.

Ek example se yaad rakho : cooking ek process hai aur khana banane 
                           wala recipe/program us process ko perform 
                           karta hai.

=================================================================================

4. Company job ke liye tumhe kya samajhna chahiye ?
---------------------------------------------------

* Sabse pehle ye 4 cheezein clear karo:

1. requests              — website se data kaise lana hai.
2. BeautifulSoup         — HTML se data kaise nikalna hai.
3. find() aur find_all() — specific elements kaise dhoondhne hain.
4. CSV                   — collected data ko file mein kaise save karna hai.