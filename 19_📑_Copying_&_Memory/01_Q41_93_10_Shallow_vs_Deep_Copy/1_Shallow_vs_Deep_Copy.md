* Shallow Copy ko samajhne mein confusion isliye hota hai kyunki outer
  list copy hoti hai, lekin uske andar ke nested objects copy nahi hote.

1. Sabse pehle: Copy hoti kya hai ?
-----------------------------------

Maan lo aapke paas ek list hai:
-------------------------------
employee1 = ["Rahul", 25, "Developer"]

- Ab aap chahte ho ki is employee ka data copy karke ek nayi list bana 
  lo.

=> employee2 = employee1.copy()

                    Ab dono lists alag hain.
                    ------------------------
      employee1                                employee2
          |                                        |
["Rahul", 25, "Developer"]     -->      ["Rahul", 25, "Developer"]

- Dono lists mein abhi same values hain, lekin dono alag list objects 
  hain.

----------------------------------------------------------------------------------

Isko verify karo:
-----------------
employee1 = ["Rahul", 25, "Developer"]
employee2 = employee1.copy()

employee2[0] = "Amit"

print(employee1)
# ['Rahul', 25, 'Developer']

print(employee2)
# ['Amit', 25, 'Developer']

- Kyun? Kyunki yahan simple list copy hui hai. employee2 mein change karne 
  se employee1 change nahi hui.

Abhi tak easy hai, hai na ?
-=-------------------------
- Actual confusion tab shuru hota hai jab list ke andar doosri list ho. Isi 
  se shallow aur deep copy ka concept clear hoga.

==================================================================================

2. Shallow Copy — sabse simple example:
---------------------------------------

* Maan lo ek company mein employee ki profile store hai:

employee1 = {
    "name": "Rahul",
    "skills": ["Python", "SQL"]
}

Ab Rahul ki profile copy karte hain:
------------------------------------
employee2 = employee1.copy()

- Yahan employee2 ek naya dictionary hai. Lekin uske andar skills wali 
  list ki separate copy nahi bani.

----------------------------------------------------------------------------------

Memory mein actually kya ho raha hai ?
--------------------------------------

employee1 dictionary
name   → "Rahul"
skills → reference
       |
       |
Shared skills list
["Python", "SQL"]
       |
       |
employee2 dictionary
name   → "Rahul"
skills → same reference

- Dono dictionaries alag hain, lekin skills list shared hai.

----------------------------------------------------------------------------------

Ab ye code dekho:
-----------------
employee1 = {
    "name": "Rahul",
    "skills": ["Python", "SQL"]
}

employee2 = employee1.copy()

employee2["skills"].append("Django")

print(employee1)
print(employee2)

Output:
-------
{'name': 'Rahul', 'skills': ['Python', 'SQL', 'Django']}
{'name': 'Rahul', 'skills': ['Python', 'SQL', 'Django']}

- Sabse important baat: Humne employee2 mein change kiya, lekin employee1 
  bhi change ho gaya!

- Kyun? Kyunki dono dictionaries ke andar skills ek hi list ko refer kar 
  raha hai.

----------------------------------------------------------------------------------

Lekin agar aap ye karo:
-----------------------
employee2["name"] = "Amit"

print(employee1["name"])  # Rahul
print(employee2["name"])  # Amit

- Toh employee1["name"] change nahi hoga, kyunki dono dictionaries alag 
  hain aur yahan humne dictionary ki key ko nayi value assign ki hai.

- Yahi hai Shallow Copy: outer container naya, lekin nested objects ke 
  references shared.

==================================================================================

3. Deep Copy — ab iska solution dekho:
--------------------------------------

* Agar hum chahte hain ki Rahul ki profile copy karne ke baad uske 
  skills bhi independently copy hon, toh Deep Copy use karenge.

CODE:
-----
import copy

employee1 = {
    "name": "Rahul",
    "skills": ["Python", "SQL"]
}

employee2 = copy.deepcopy(employee1)
employee2["skills"].append("Django")

print(employee1)
print(employee2)

Output
------
{'name': 'Rahul', 'skills': ['Python', 'SQL']}
{'name': 'Rahul', 'skills': ['Python', 'SQL', 'Django']}

----------------------------------------------------------------------------------

* Ab employee1 bilkul unchanged hai.

employee1
skills → ["Python", "SQL"]

Original skills list
Independent object

<--------------------------------------------->

employee2
skills → ["Python", "SQL", "Django"]

Copied skills list
Separate object


- Ab nested lists bhi independent hain.

----------------------------------------------------------------------------------

Deep Copy           : outer container ke saath nested objects ko bhi recursively 
                      copy karta hai, isliye mutable nested objects mein changes generally original ko affect nahi karte.

Ek technical detail : immutable objects jaise integers aur strings ko Python ko 
                      har baar physically naya object banana zaroori nahi hota. 
                      Humein main focus nested mutable objects par rakhna hai.

==================================================================================

4. Real company project example:
--------------------------------

* Ab maan lo aap ek backend developer ho aur company ek employee management 
  system bana rahi hai.

Requirement hai:
----------------
- Employee ki original profile database se aayi hai.

- HR ko us profile ka temporary draft banana hai.

- HR draft mein skills ya address edit kar sakta hai.

- Original profile edit nahi honi chahiye jab tak HR final save na kare.

----------------------------------------------------------------------------------

Profile kuch aisi hai:
----------------------

employee = {
    "id": 101,
    "name": "Rahul",
    "address": {
        "city": "Indore",
        "pincode": 452001
    },
    "skills": ["Python", "SQL"]
}

----------------------------------------------------------------------------------

Case A: Galti se shallow copy use kar li
----------------------------------------
employee_draft = employee.copy()

employee_draft["address"]["city"] = "Pune"
employee_draft["skills"].append("Django")

print(employee["address"]["city"])
print(employee["skills"])

Output:
-------
Pune
['Python', 'SQL', 'Django']

- Problem! HR ne sirf draft edit kiya tha, lekin original employee data 
  bhi change ho gaya.

- Production code mein agar aap isi object ko aage use karte ho, toh 
  unintended changes bugs create kar sakte hain.

----------------------------------------------------------------------------------

Case B: Deep copy se problem solve
----------------------------------

import copy

employee_draft = copy.deepcopy(employee)

employee_draft["address"]["city"] = "Pune"
employee_draft["skills"].append("Django")

print(employee["address"]["city"])
print(employee["skills"])

print(employee_draft["address"]["city"])
print(employee_draft["skills"])

Output:
-------
Indore
['Python', 'SQL']

Pune
['Python', 'SQL', 'Django']

----------------------------------------------------------------------------------

* Ab original profile safe hai, aur draft ko independently edit kiya ja 
  sakta hai.

Original profile
Indore · Python, SQL

HR draft
Pune · Python, SQL, Django

* Real projects mein ye pattern configuration templates, nested request 
  data, draft forms, test fixtures aur independent object editing mein
  useful ho sakta hai. Lekin har jagah Deep Copy use karna sahi nahi hai.

==================================================================================

5. Developer ke liye kaunsa use karna chahiye ?
-----------------------------------------------

Situation	                                    Kya use karein ?
---------------------------------------------------------------------------------
Simple flat list ya dictionary copy karni    	Shallow copy often enough
hai.
---------------------------------------------------------------------------------
Nested mutable data ko independently edit 	    Deep copy
karna hai.
---------------------------------------------------------------------------------
Sirf original object ka reference chahiye	    Assignment (b = a)
---------------------------------------------------------------------------------
Bada object hai aur performance important 	    Pehle requirement samjho; Deep 
hai.                                            Copy blindly mat karo.
---------------------------------------------------------------------------------

* Ek aur important baat: agar aap sirf nested dictionary ka ek specific part 
  change karna chahte ho, toh poora object Deep Copy karne ke bajaye targeted 
  copy ya immutable data structure better ho sakta hai. Deep Copy comparatively 
  expensive bhi ho sakti hai.

==================================================================================

6. Ab apna concept test karo:
-----------------------------

Question 1: Output kya hoga ?
-----------------------------
import copy

a = [[1, 2], [3, 4]]
b = copy.copy(a)

b[0].append(99)
print(a)

o/p: [[1, 2, 99], [3, 4]]

<--------------------------------------------------------------->

Question 2: Usi code mein copy.copy(a) ki jagah copy.deepcopy(a) 
            hota, toh kya hota ?

o/p : Original a unchanged rehta

<--------------------------------------------------------------->

Question 1 correct!
-------------------
- Shallow copy mein nested list shared hai, isliye 99 original 
  mein bhi add hoga.

✓ Question 2 correct!
---------------------
- Deep copy mein nested list separate hogi, isliye original a 
  unchanged rahega.

* Bas ye ek line yaad rakhna : Shallow Copy mein outer object alag hota hai, 
                               par nested mutable objects share ho sakte hain. 
                               Deep Copy mein nested objects bhi recursively 
                               copy hote hain.

==================================================================================
----------------------------------------------------------------------------------
==================================================================================

Tumhara code:
-------------
employee = {
    "id": 101,
    "name": "Rahul",
    "address": {
        "city": "Indore",
        "pincode": 452001
    },
    "skills": ["Python", "SQL"]
}

employee_draft = employee.copy()

==================================================================================

Case 1: Puri nested list ya dictionary replace karna
----------------------------------------------------

* Skills ki poori list replace kar do:

employee_draft["skills"] = ["Java", "Django"]

print(employee["skills"])
# ['Python', 'SQL']

print(employee_draft["skills"])
# ['Java', 'Django']

- Original change nahi hoga. Kyunki tumne employee_draft ki skills 
  key ko ek nayi list de di.

----------------------------------------------------------------------------------

Address ki poori dictionary replace kar do:
-------------------------------------------
employee_draft["address"] = {
    "city": "Pune",
    "pincode": 411001
}

print(employee["address"])
# {'city': 'Indore', 'pincode': 452001}

print(employee_draft["address"])
# {'city': 'Pune', 'pincode': 411001}

- Yahan bhi original change nahi hoga.

==================================================================================

Case 2: Nested list ya dictionary ke andar ki value change karna
----------------------------------------------------------------

* Skills list ke andar item add karo:

employee_draft["skills"].append("Django")

print(employee["skills"])
# ['Python', 'SQL', 'Django']

- Original bhi change ho gaya!

----------------------------------------------------------------------------------

Address dictionary ke andar city change karo:
---------------------------------------------
employee_draft["address"]["city"] = "Pune"

print(employee["address"]["city"])
# Pune

- Original mein bhi city Pune ho gayi!

==================================================================================

# Final rule yaad rakho:
# ----------------------

Tum kya karte ho?	                            Original change hoga ?
---------------------------------------------------------------------
employee_draft["skills"] = ["Java"]	            Nahi
---------------------------------------------------------------------
employee_draft["address"] = {"city": "Pune"}	Nahi
---------------------------------------------------------------------
employee_draft["skills"].append("Django")	    Haan
---------------------------------------------------------------------
employee_draft["address"]["city"] = "Pune"	    Haan
---------------------------------------------------------------------

* Kyun ? employee.copy() se outer dictionary ki copy banti hai, lekin 
         address aur skills ke nested objects shared rehte hain.

- Poora object replace karoge          : draft ki key naye object ko 
                                         refer karegi.

- Shared object ke andar change karoge : original ko bhi wahi change 
                                         dikhega.
                                         
Yahi Shallow Copy ka core concept hai. ✅