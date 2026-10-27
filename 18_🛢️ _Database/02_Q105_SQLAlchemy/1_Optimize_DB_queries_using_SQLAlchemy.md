# 1. SQLAlchemy kya hota hai ?
# ----------------------------

* SQLAlchemy Python ki ek library hai jo Python application ko database 
  ke saath kaam karne mein help karti hai. Ye SQL queries likhne aur 
  execute karne ke tools bhi deti hai, aur Python objects ke through 
  database data manage karne ka tareeka bhi.

Abhi tumne ye 3 concepts seekhe hain:
-------------------------------------
- SQLite / MySQL / PostgreSQL : database systems.
- SQL                         : database se baat karne ki language.
- SQLAlchemy                  : Python aur database ke beech kaam karne 
                                wali library.

- Maan lo tum Flask mein Employee Management API bana rahe ho. Tumhe 
  employees ko add, update, delete aur read karna hai. SQLAlchemy is 
  kaam ko Python se manage karna aasaan bana sakta hai.

===================================================================================

2. SQLAlchemy kaise kaam karta hai ?
------------------------------------

* SQLAlchemy ke do important approaches hain.

SQLAlchemy Core
---------------
- Ismein tum SQL statements ko Python ke tools se construct aur execute 
  kar sakte ho. Tumhe SQL ka knowledge useful rahega.

SQLAlchemy ORM
--------------
- ORM ka full form hai Object-Relational Mapper. Ismein tum database 
  tables ko Python classes ke roop mein represent kar sakte ho aur 
  Python objects ke through data manage kar sakte ho.

-----------------------------------------------------------------------------------

Ek chhota conceptual example:
-----------------------------

* Direct SQL mein tum likhte ho:

=> SELECT * FROM employees;

* SQLAlchemy ORM mein tum Python ke through kuch aisa likh sakte ho:

employees = session.scalars(
    select(Employee)
).all()

- Yahan Employee ek Python class hai jo database table ko represent karti hai. 
  SQLAlchemy is Python statement ko database ke liye suitable SQL mein convert 
  karta hai aur result Python objects ke form mein de sakta hai.

- Important: SQLAlchemy database ka replacement nahi hai. Data phir bhi SQLite, 
             MySQL ya PostgreSQL mein store hota hai.

===================================================================================

3. “Optimize DB queries using SQLAlchemy” ka matlab kya hai ?
-------------------------------------------------------------

* Iska matlab hai database se data fetch ya update karne ke tareeke ko aisa
  banana ki unnecessary queries kam chalein, kam data transfer ho aur 
  application efficient rahe.

* Maan lo tumhare paas 100 employees hain aur har employee ka department bhi 
  database mein alag table mein stored hai.

Ek inefficient approach mein:
-----------------------------
- Pehli query: 100 employees fetch karo.
- Phir har employee ke department ke liye alag query chalao.
- Total lagbhag 101 queries chal sakti hain.


* Is problem ko N+1 query problem kehte hain. SQLAlchemy ki official documentation 
  mein ise avoid karne ke liye selectinload() aur joinedload() jaise options bataye 
  gaye hain. 

* Optimized approach mein related data ko suitable loading strategy se kam queries 
  mein fetch kiya ja sakta hai.

-----------------------------------------------------------------------------------

Optimization ke common tareeke
------------------------------

Technique	                                Simple meaning
----------------------------------------------------------------------------------
N+1 problem avoid karna	                    Har record ke liye alag query 
                                            chalane se bachna.
----------------------------------------------------------------------------------
Sirf required columns lena	                Unnecessary data fetch na karna
----------------------------------------------------------------------------------
Filtering database mein karna	            WHERE se required records hi mangwana
----------------------------------------------------------------------------------
Indexes use karna	                        Kuch searches ko faster banana
----------------------------------------------------------------------------------
Query count aur execution time check karna	Actual bottleneck identify karna.
----------------------------------------------------------------------------------

* Har optimization ka benefit data aur query par depend karta hai. Sirf 
  queries ki count kam karna hamesha fastest solution ki guarantee nahi 
  hoti.

===================================================================================

4. Tumhe kis order mein seekhna chahiye ?
-----------------------------------------

Meri recommendation:
--------------------

1. SQL basics         — SELECT, WHERE, INSERT, UPDATE, DELETE, JOIN.
2. SQLite basics      — database, tables aur queries.
3. SQLAlchemy basics  — connection, models, sessions aur CRUD operations.
4. Query optimization — N+1 problem, eager loading, indexes aur query performance.

* Abhi SQLAlchemy ko project mein implement karne ki zaroorat nahi. Pehle iska 
  concept clear karna bilkul sahi approach hai.

* Ek line mein yaad rakho : SQL database ki language hai, SQLite database engine 
                            hai, aur SQLAlchemy Python ki library hai jo tumhe 
                            database ke saath efficiently kaam karne mein help 
                            karti hai.