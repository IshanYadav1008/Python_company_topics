* Pehle simple baat: Beautiful Soup ek Python library hai jo HTML ko parse 
                     karke usmein se required data nikalne mein help karti 
                     hai. Website se HTML download karne ke liye hum aksar 
                     requests library use karte hain.

1. Real-world example samjho
----------------------------
* Maan lo kisi website par products ki list hai:

Website ka HTML
---------------
<div class="product">
  <h2>Laptop</h2>
  <p class="price">₹50,000</p>
</div>
<div class="product">
  <h2>Keyboard</h2>
  <p class="price">₹1,500</p>
</div>

Beautiful Soup se extracted data
--------------------------------
Laptop    : ₹50,000
Keyboard  : ₹1,500

- Beautiful Soup HTML ke tags aur attributes ko use karke data 
  dhoondhti hai.

===================================================================================

2. Step 1 — Libraries install karo
----------------------------------

Terminal mein:
--------------
=> pip install requests beautifulsoup4


- requests       — webpage ka HTML download karta hai.
- beautifulsoup4 — HTML ko parse karke data nikalta hai.

===================================================================================

3. Step 2 — Web scraper ka code likho
-------------------------------------
* Hum ek public practice website se product names aur prices extract 
  karenge. Books to Scrape scraping practice ke liye banayi gayi 
  website hai.

CODE:
-----
import requests
from bs4 import BeautifulSoup

url = "https://books.toscrape.com/"

response = requests.get(url, timeout=10)
response.raise_for_status()

soup = BeautifulSoup(response.text, "html.parser")

books = soup.find_all("article", class_="product_pod")

for book in books:
    title = book.h3.a["title"]
    price = book.find("p", class_="price_color").get_text(strip=True)

    print("Book:", title)
    print("Price:", price)
    print("-" * 30)

* Ye code practice website ke pehle page se books ke titles aur prices 
  nikalta hai.

===================================================================================

4. Code kaise kaam karta hai ?
------------------------------

1. requests.get()
-----------------
=> response = requests.get(url, timeout=10)

- Website se HTTP response laata hai, jisme HTML ho sakta hai.

-----------------------------------------------------------------------------------

2. BeautifulSoup()
------------------
=> soup = BeautifulSoup(response.text, "html.parser")

- HTML ko parse karta hai, taaki tags ko search kar sakein.

-----------------------------------------------------------------------------------

3. find_all()
-------------
=> books = soup.find_all("article", class_="product_pod")

- Page par sabhi matching book elements ki list deta hai.

-----------------------------------------------------------------------------------

4. Title aur price extract karna
--------------------------------
title = book.h3.a["title"]
price = book.find("p", class_="price_color").get_text(strip=True)

- Har book ka title aur price nikalta hai.

===================================================================================

5. Beautiful Soup ke important functions:
-----------------------------------------

Function	    Use
---------------------------------------------------------------
find()	        Pehla matching element dhoondhta hai.
---------------------------------------------------------------
find_all()	    Saare matching elements dhoondhta hai.
---------------------------------------------------------------
select()	    CSS selectors se elements dhoondhta hai.
---------------------------------------------------------------
get_text()	    Element ke andar ka text nikalta hai.
---------------------------------------------------------------
get()	        Attribute ki value safely access kar sakta hai.
---------------------------------------------------------------

Example:
--------
# Pehla matching element
book = soup.find("article", class_="product_pod")

# Saare matching elements
books = soup.find_all("article", class_="product_pod")

# CSS selector se saare product elements
books = soup.select("article.product_pod")

* Ek important difference: find() ek element ya None return karta hai, 
  jabki find_all() matching elements ki list deta hai.

===================================================================================

6. Company projects mein iska use kaise hota hai ?
--------------------------------------------------

- Product price comparison
- Public job listings collect karna
- News headlines extract karna
- Public catalog data ko CSV mein save karna
- Research aur data analysis ke liye data collect karna

* Real projects mein network errors, missing HTML elements, pagination 
  aur website ke access rules ko bhi handle karna padta hai. Beautiful 
  Soup JavaScript se baad mein load hone wale content ko khud execute 
  nahi karta.

