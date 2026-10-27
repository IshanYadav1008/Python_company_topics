# 1. SQLite kya hai ?
# -------------------

* SQLite ek database hai jisme hum data ko permanently store kar sakte 
  hain.

* Maan lo tum ek company mein kaam karte ho. Company ke paas 500 employees 
  hain. Har employee ka naam, ID, department aur salary store karni hai.

* Agar tum data Python ki simple list mein rakhoge, toh program band hone 
  par changes lose ho sakte hain.

--------------------------------------------------------------------------------

* Is problem ko solve karne ke liye hum database use karte hain.

Normal variable ya list
-----------------------
- Program ke andar data rakhna; data automatically permanent nahi 
  hota.

SQLite database
---------------
- Data ko disk par database file mein save karna, taaki program 
  band hone ke baad bhi woh rahe.

* SQLite ka ek important feature hai: ise use karne ke liye alag 
  database server chalana nahi padta. Database ek file mein store 
  ho sakta hai, jaise company.db.

================================================================================

2. Database ke andar data kaisa dikhta hai ?
--------------------------------------------

* Maan lo company ke employees ka database hai.

Database : company.db
Table    : employees

----------------------------------------
| company.db                           |
----------------------------------------
| employees table                      |
----------------------------------------
| id	name	department             | 
----------------------------------------
| 1	    Rahul	IT                     |  
| 2	    Priya	HR                     | 
| 3	    Amit	Finance                |   
----------------------------------------

* Is example mein chaar terms samajhna bahut zaroori hai:

- Database : Data store karne ki jagah, jaise company.db.

- Table    : Ek particular type ka data rakhne ki jagah, 
             jaise employees.

- Column   : Data ki property, jaise name ya department.

- Row      : Ek employee ka complete record.

- Example: Rahul wali row ek employee ka record hai.

================================================================================

3. SQLite mein SQL kya hota hai ?
---------------------------------

* SQL ka full form hai Structured Query Language.

- Ye ek language hai jisse hum database ko instructions dete hain.

Jaise database se kehna:
------------------------
- Naya employee add karo.
- Saare employees dikhao.
- Rahul ka department badlo.
- Kisi employee ka record delete karo.

* Ye instructions SQL commands se di jaati hain.

================================================================================

4. SQL ki 4 important operations — CRUD
---------------------------------------

* Inhe dhyan se samjho, kyunki database seekhne ka ye sabse important 
  foundation hai.

--------------------------------------------------------------------------------

1. CREATE / INSERT — Naya record add karna:
-------------------------------------------

* Company mein naya employee join hua, toh uska record database mein 
  add karna.

SQL:
----
INSERT INTO employees (id, name, department)
VALUES (4, 'Neha', 'Sales');

--------------------------------------------------------------------------------

2. READ / SELECT — Data dekhna
------------------------------

* Database se employees ki list nikalna.

=> SELECT * FROM employees;

- Yahan * ka matlab hai sabhi columns.

--------------------------------------------------------------------------------

3. UPDATE — Existing record badalna
-----------------------------------

* Rahul ka department IT se Engineering karna.

UPDATE employees
SET department = 'Engineering'
WHERE id = 1;

- WHERE id = 1 batata hai ki kis employee ka record badalna hai.

--------------------------------------------------------------------------------

4. DELETE — Record hatana
-------------------------

* Employee ID 2 ka record delete karna.

DELETE FROM employees
WHERE id = 2;

--------------------------------------------------------------------------------

* Ek important clarification: SQL mein table banane ke liye CREATE TABLE 
  command bhi hoti hai. Lekin CRUD ka C aam taur par Create kehta hai, 
  aur SQL mein naya record add karne ke liye INSERT use hota hai.

================================================================================

5. SQLite aur MySQL mein kya difference hai ?
---------------------------------------------

* Dono databases hain, lekin kaam karne ka tareeka alag hai.

Feature	          SQLite	                     MySQL
-----------------------------------------------------------------------------
Database server	  Alag server ki zaroorat nahi	 Aam taur par server chahiye
-----------------------------------------------------------------------------
Data storage	  Ek database file	             Server-managed storage
-----------------------------------------------------------------------------
Setup	          Bahut simple	                 Comparatively zyada setup
-----------------------------------------------------------------------------
Common use	      Learning, local apps,        	 Multi-user applications aur 
                  small-to-medium workloads      server-based systems
-----------------------------------------------------------------------------

* SQLite chhota ya simple hone ke kaaran bekaar database nahi hai. Ye bahut 
  saari real applications mein use hota hai. Kaunsa database best hai, ye 
  application ki requirements par depend karta hai.

================================================================================

6. SQLite aur Python ka kya relation hai ?
------------------------------------------

* Abhi tumhe bas ye distinction yaad rakhna hai:

- SQLite database engine hai.
- SQL database se baat karne ki language hai.
- Python ek programming language hai.
- sqlite3 Python ka built-in module hai jo Python code ko 
  SQLite database ke saath kaam karne deta hai.

--------------------------------------------------------------------------------

Inka relation kuch aisa hai:
----------------------------

Python application
      ↕️
sqlite3 module
Python aur database ke beech connection
      ↕️
SQLite database file
Data permanently store hota hai

- Abhi hum is process ko implement nahi kar rahe; sirf concepts 
  samajh rahe hain.