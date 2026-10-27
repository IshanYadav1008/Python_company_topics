Step 2 — Ubuntu terminal open karo
----------------------------------

* Ubuntu mein "Ctrl + Alt + T" press karo. Terminal open ho jayega.

* Sabse pehle check karte hain ki Python installed hai ya nahi.

* Terminal mein ye command likho:

Pehle ye command check karo:
----------------------------
=> python3 --version

Phir system tools install karo:
-------------------------------
=> sudo apt update

=> sudo apt install python3-venv python3-pip curl

==============================================================================

Step-2 - Ab hum flask se basic python project bana rhe hai:
-----------------------------------------------------------

* Ye hum bana rhe hai apne python folder mai:

: Project ka folder banao
-------------------------
Desktop --> Python --> new_folder --> flask_employee_api

=> cd flask_employee_api

------------------------------------------------------------------------------

Ab project folder ke andar Python 3.11.9 set karo:
--------------------------------------------------
=> pyenv local 3.11.9

------------------------------------------------------------------------------

Check karo:
-----------
=> python --version

Expected output:
----------------
Python 3.11.9

------------------------------------------------------------------------------

# Virtual environment banao:

Ye command chalao:
------------------
=> python -m venv .venv

Ab environment activate karo:
-----------------------------
=> source .venv/bin/activate

* Activate hone ke baad terminal ke start mein (.venv) dikhna chahiye.

------------------------------------------------------------------------------

Check karo:
-----------
=> python --version

Aur:
----
=> which python

Expected path kuch aisa hoga:
-----------------------------
/home/lenovo/Desktop/Python/flask_employee_api/.venv/bin/python

==============================================================================

Step 4: Flask install karo
--------------------------

* Terminal mein ye command chalao:

=> python -m pip install Flask

or 
---

=> python -m pip install Flask --default-timeout=120 --retries=5

Is command mein:
----------------
- --default-timeout=120 download ko zyada samay deta hai.
- --retries=5 download fail hone par dobara try karta hai.

------------------------------------------------------------------------------

* Installation complete hone ke baad Flask ka version check karo:

=> python -m flask --version

* Output mein Flask aur Python ke versions dikhne chahiye.

==============================================================================

app.py file banao
-----------------

* Tumhare terminal mein abhi ye project folder active hai:

~/Desktop/Python/flask_employee_api

Ye command chalao:
------------------
=> nano app.py

------------------------------------------------------------------------------

* GNU nano 4.8 mein hi code likhna hai. Tum sahi jagah par ho.

Step 1: Nano editor mein code paste karo:
-----------------------------------------

from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello! My first Flask API is running."

if __name__ == "__main__":
    app.run(debug=True)


<----------------------------------------------------->

Step 2: File save karo
----------------------

* Nano ke andar hi ye karo:

1. Ctrl + O dabao.
2. Neeche filename app.py dikhega. Enter dabao.
3. Ctrl + X dabao.

- Ab tum terminal par wapas aa jaoge.

------------------------------------------------------------------------------

Code ko samjho
--------------

- Flask(__name__)     — Flask application banata hai.
- @app.route("/")     — browser ke home URL / ko define karta hai.
- def home()          — request aane par function chalata hai.
- return              — browser ko response bhejta hai.
- app.run(debug=True) — development server start karta hai.

------------------------------------------------------------------------------

Step 3: Flask application run karo:
-----------------------------------

* Terminal mein ye command likho:

=> python app.py


Agar sab sahi raha, toh ye dikhega:

 * Running on http://127.0.0.1:5000

------------------------------------------------------------------------------

Step 4: Browser mein kholo
--------------------------

http://127.0.0.1:5000  

- Browser mein Hello! My first Flask API is running. dikhna chahiye.

* Dhyan rahe: Server band karne ke liye terminal mein Ctrl + C dabana.

------------------------------------------------------------------------------

# Abhi ek baat samjho:

- Abhi humne sirf ek route banaya hai:

@app.route("/")
def home():
    return "Hello! My first Flask API is running."

- / URL ka path hai.
- home() function request aane par execute hota hai.
- return browser ko response bhejta hai.

==============================================================================
------------------------------------------------------------------------------
==============================================================================

Tumhare output ka matlab:
-------------------------

- Running on http://127.0.0.1:5000 — server start ho gaya hai.

- GET / HTTP/1.1" 200              — browser ko successful response mila.

- GET /favicon.ico ... 404         — browser ne tab icon maanga, lekin abhi 
                                     woh file nahi hai. Isko ignore kar sakte 
                                     ho; ye koi serious error nahi hai.

* Ab hum tumhari pehli actual REST API banayenge: Employee Management API.

------------------------------------------------------------------------------

Step 1: Server ko stop karo
---------------------------
* Jis terminal mein Flask chal raha hai, usmein Ctrl + C dabao.

------------------------------------------------------------------------------

Step 2: app.py dobara kholo
---------------------------
=> nano app.py

------------------------------------------------------------------------------

Purana code hata kar neeche wala poora code paste karo:
-------------------------------------------------------

from flask import Flask, jsonify

app = Flask(__name__)

employees = [
    {"id": 1, "name": "Rahul", "department": "IT"},
    {"id": 2, "name": "Priya", "department": "HR"},
    {"id": 3, "name": "Amit", "department": "Finance"}
]

@app.route("/")
def home():
    return "Employee Management API is running!"

@app.route("/employees", methods=["GET"])
def get_employees():
    return jsonify(employees)

if __name__ == "__main__":
    app.run(debug=True)

------------------------------------------------------------------------------

Step 3: File save karo
----------------------

* Nano mein:

1. Ctrl + O dabao.
2. Enter dabao.
3. Ctrl + X dabao.

------------------------------------------------------------------------------

Step 4: Application phir se run karo
------------------------------------
=> python app.py

------------------------------------------------------------------------------

Step 5: Apni pehli GET API test karo
------------------------------------

* Browser mein ye URL kholo:

http://127.0.0.1:5000/employees

* Tumhe JSON format mein employees ki list dikhni chahiye, kuch is tarah:


[
  {
    "department": "IT",
    "id": 1,
    "name": "Rahul"
  },
  {
    "department": "HR",
    "id": 2,
    "name": "Priya"
  },
  {
    "department": "Finance",
    "id": 3,
    "name": "Amit"
  }
]

Samjho humne kya banaya
-----------------------
- @app.route("/employees", methods=["GET"]) — /employees endpoint ko GET 
  request ke liye register karta hai.

- get_employees()    — employees ki list return karta hai.

- jsonify(employees) — Python data ko JSON HTTP response mein convert karta 
                       hai.

- 200 OK             — request successful hone par response status hota hai.

* Abhi employees memory mein store hain; server restart karoge toh code mein 
  di hui original list phir se load hogi.

------------------------------------------------------------------------------

* Pehle /employees URL test karo aur batao ki employees ki list dikh rahi hai 
  ya nahi. Uske baad hum GET /employees/1 banayenge, jo sirf ek employee ka 
  data return karega.

NOTE: Hum ab apni application ko as framework baad mai direct fastAPI banana 
      seekhenge.