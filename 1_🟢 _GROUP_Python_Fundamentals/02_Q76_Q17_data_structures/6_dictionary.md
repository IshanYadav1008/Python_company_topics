🔹 Dictionary kya hoti hai?
---------------------------
* Dictionary ek data structure hai jo data ko "key : value" 
  pair mein store karti hai.

Example:
--------
student = {
    "name": "Rahul",
    "age": 20,
    "marks": 85
}

# Yahan:

key       value
----------------
"name"  s→ "Rahul"
"age"   → 20
"marks" → 85

* Isliye dictionary ko simple language mein:

Dictionary = Key-Value pairs ka collection

============================================================================

🔹 Dictionary kyu use karte hain?
---------------------------------
* Maan lo tumhare paas student ka data hai.

List mein:
----------
student = ["Rahul", 20, 85]

* Ab problem ye hai ki 20 kya hai? Age? Marks? 😕

Dictionary mein:
----------------
student = {
    "name": "Rahul",
    "age": 20,
    "marks": 85
}

Ab clearly pata hai:

name  → Rahul
age   → 20
marks → 85

* Isliye dictionary real-world data ko represent karne mein 
  bahut useful hai.

============================================================================

🔹 Dictionary ka syntax
-----------------------
my_dict = {
    key1: value1,
    key2: value2,
    key3: value3
}

Example:
--------
person = {
    "name": "Amit",
    "age": 25,
    "city": "Indore"
}

============================================================================

🔹 Dictionary mein data kaise access karein?

* Dictionary mein list ki tarah index nahi hota.

Ye nahi:
--------
person[0]

Instead key se value access karte hain:
---------------------------------------
person = {
    "name": "Amit",
    "age": 25
}

print(person["name"])
Output: Amit

Aur:

print(person["age"])
Output: 25

---------------------------------------------------

**Yaad rakho:**

List       → index se value
Tuple      → index se value
Set        → index nahi
Dictionary → key se value

============================================================================

🔹 Dictionary mein value change karna

**Dictionary mutable hoti hai.**

* Matlab existing value change kar sakte ho.

CODE:
-----
student = {
    "name": "Rahul",
    "age": 20
}
student["age"] = 21
print(student)

Output:
-------
{'name': 'Rahul', 'age': 21}

============================================================================

🔹 Dictionary mein naya data add karna

* Agar key pehle se exist nahi karti, to assignment se new 
  key-value pair create ho jata hai.

CODE:
-----
student = {
    "name": "Rahul",
    "age": 20
}
student["marks"] = 85
print(student)

Output:
-------
{'name': 'Rahul', 'age': 20, 'marks': 85}

Yani:
-----
student["marks"] = 85

➡️ "marks" naam ki new key create ho gayi.

============================================================================
----------------------------------------------------------------------------
============================================================================

🔥 Dictionary ke Important Methods
----------------------------------
* Ab methods ko category-wise samjhte hain.

----------------------------------------------------------------------------

# 1. get()

* Kisi key ki value lene ke liye.

CODE:
-----
student = {
    "name": "Rahul",
    "age": 20
}
print(student.get("name"))

Output:
-------
Rahul

<---------------------------------------------------------->

# [] aur get() mein difference:

=> student["marks"]

* Agar "marks" key nahi hai toh: "KeyError"

Lekin:
------
=> student.get("marks")

Output: None

* Isliye get() safer hota hai.

<---------------------------------------------------------->

* Tum default value bhi de sakte ho:

=> print(student.get("marks", 0))

Output: 0

. Matlab marks nahi mile to 0 return karo.

============================================================================

# 2. keys()

* Dictionary ki saari keys deta hai.

CODE:
-----
student = {
    "name": "Rahul",
    "age": 20,
    "marks": 85
}
print(student.keys())

Output roughly:
---------------
dict_keys(['name', 'age', 'marks'])

Iska common use:
----------------
for key in student.keys():
    print(key)

Output:
-------
name
age
marks

============================================================================

# 3. values()

* Dictionary ki saari values deta hai.

print(student.values())

Output:
-------
dict_values(['Rahul', 20, 85])

Loop:
-----
for value in student.values():
    print(value)

============================================================================

# 4. items() ⭐

* Ye key aur value dono deta hai.

=> print(student.items())

Output:
-------
dict_items([
    ('name', 'Rahul'),
    ('age', 20),
    ('marks', 85)
])

Loop mein ye bahut important hai:
---------------------------------
for key, value in student.items():
    print(key, value)

Output:
-------
name  Rahul
age   20
marks 85

Ye pattern yaad karna:
----------------------
for key, value in dictionary.items():
    print(key, value)

* Dictionary ke saath programming mein bahut use hota hai.

============================================================================

# 5. update() ⭐

* Existing dictionary mein multiple key-value pairs "add/update" 
  karta hai.

CODE:
-----
student = {
    "name": "Rahul",
    "age": 20
}

student.update({
    "age": 21,
    "marks": 85
})

Ab:
---
print(student)

Output:
-------
{'name': 'Rahul', 'age': 21, 'marks': 85}

<--------------------------------------------------------------->

Dhyan do:
---------
"age": 21     // pehle se tha, isliye update ho gaya.

Aur:
----
"marks": 85  // naya tha, isliye add ho gaya.

Isliye update():
----------------
key exists        → value update
key doesn't exist → new pair add

============================================================================

# 6. pop()

* Kisi specific key ko remove karta hai aur uski value return karta hai.

CODE:
-----
student = {
    "name": "Rahul",
    "age": 20,
    "marks": 85
}
x = student.pop("age")
print(x)
print(student)

Output:
-------
20
{'name': 'Rahul', 'marks': 85}

* Yani "age": 20 remove ho gaya.

============================================================================

# 7. popitem()

* Dictionary ka last inserted key-value pair remove karta hai 
  aur return karta hai.

CODE:
-----
student = {
    "name": "Rahul",
    "age": 20,
    "marks": 85
}
x = student.popitem()
print(x)
print(student)

Output:
-------
('marks', 85)
{'name': 'Rahul', 'age': 20}

* Modern Python dictionaries insertion order maintain karti hain, 
  isliye popitem() last inserted pair ko remove karta hai.

============================================================================

# 8. clear()

* Dictionary ke saare elements remove kar deta hai.

CODE:
-----
student = {
    "name": "Rahul",
    "age": 20
}
student.clear()
print(student)

Output:
-------
{}

============================================================================

# 9. copy()

* Dictionary ki shallow copy banata hai.

CODE:
-----
student = {
    "name": "Rahul",
    "age": 20
}
new_student = student.copy()
print(new_student)

Output:
-------
{'name': 'Rahul', 'age': 20}

* Ab dono separate dictionary objects hain.

============================================================================

# 10. setdefault()

* Ye thoda important aur initially confusing method hai.

* Agar key already hai, to uski existing value return karta hai.

CODE:
-----
student = {
    "name": "Rahul"
}
x = student.setdefault("name", "Amit")
print(x)
print(student)

Output:
-------
Rahul
{'name': 'Rahul'}   // Existing "name" ko change nahi kiya.

<------------------------------------------------------------->

Agar key exist nahi karti:
--------------------------
student = {
    "name": "Rahul"
}
x = student.setdefault("age", 20)
print(x)
print(student)

Output:
-------
20
{'name': 'Rahul', 'age': 20}

Yani:
-----
key exists      → existing value return
key doesn't exist → key add + default value return

============================================================================

# 11. fromkeys()

* Ye ek new dictionary create karta hai given keys ke saath.

CODE:
-----
keys    = ["name", "age", "city"]
student = dict.fromkeys(keys)
print(student)

Output:
-------
{'name': None, 'age': None, 'city': None}

<--------------------------------------------------->

* Tum default value bhi de sakte ho:

CODE:
-----
keys = ["name", "age", "city"]
student = dict.fromkeys(keys, "Unknown")
print(student)

Output:
-------
{'name': 'Unknown', 'age': 'Unknown', 'city': 'Unknown'}

============================================================================

# 🔥 Dictionary mein check karna

Ye bhi bahut important hai.
---------------------------
student = {
    "name": "Rahul",
    "age": 20
}
print("name" in student)  // Check karo key exist karti hai ya nahi:

Output: True

Aur:
----
print("marks" in student)

Output: False

----------------------------------------------------------------------------

# Important:
# ----------

* "in" dictionary mein normally keys check karta hai, values nahi.

=> print("Rahul" in student)

Output: False  // Kyunki "Rahul" value hai, key nahi.

<-------------------------------------------------------->

Values check karni hain:
------------------------
print("Rahul" in student.values())

Output: True

============================================================================
----------------------------------------------------------------------------
============================================================================

# 🔹 Dictionary mein duplicate keys?

* Dictionary mein same key ko multiple times nahi rakh sakte.

CODE:
-----
student = {
    "name": "Rahul",
    "name": "Amit"
}

Final result:
-------------
{'name': 'Amit'}  // Last value reh jaati hai.

<--------------------------------------------------->

* Lekin values duplicate ho sakti hain:

CODE:
-----
student = {
    "name": "Rahul",
    "friend": "Rahul"
}

* Ye perfectly valid hai.

============================================================================

🔹 Dictionary ki keys kaisi honi chahiye?

* Dictionary ki keys hashable honi chahiye.

Simple examples:
----------------
{
    "name": "Rahul",
    1: "one",
    2: "two",
    (1, 2): "tuple"
}

<------------------------------------------------->

* Lekin list ko key nahi bana sakte:

{
    [1, 2]: "hello"
}

. Ye error dega: TypeError: unhashable type: 'list'

<------------------------------------------------->

# Easy rule:

Generally:
----------
String     ✅
Integer    ✅
Float      ✅
Tuple      ✅ (agar uske elements hashable hain)
List       ❌
Set        ❌
Dictionary ❌

============================================================================

🔹 Dictionary ki values par aisi restriction nahi

* Values almost kisi bhi Python object ki ho sakti hain.

CODE:
-----
student = {
    "name": "Rahul",
    "marks": [80, 85, 90],
    "subjects": {"Python", "SQL"},
    "address": {
        "city": "Indore"
    }
}

Ye valid hai.

============================================================================

🔥 Nested Dictionary
--------------------
* Dictionary ke andar dictionary bhi rakh sakte ho.

students = {
    "student1": {
        "name": "Rahul",
        "age": 20
    },
    "student2": {
        "name": "Amit",
        "age": 22
    }
}

Access:
-------
print(students["student1"]["name"])

Output: Rahul

============================================================================

🔥 Dictionary ke andar List:
----------------------------
student = {
    "name": "Rahul",
    "marks": [80, 85, 90]
}

Access:
-------
print(student["marks"][0])

Output: 80

============================================================================
----------------------------------------------------------------------------
============================================================================

📌 Dictionary ke saare important methods
----------------------------------------

| Method         | Kaam                      |
| -------------- | ------------------------- |
| `get()`        | Key ki value safely get   |
| `keys()`       | Saari keys                |
| `values()`     | Saari values              |
| `items()`      | Key-value pairs           |
| `update()`     | Add/update pairs          |
| `pop()`        | Specific key remove       |
| `popitem()`    | Last inserted pair remove |
| `clear()`      | Sab remove                |
| `copy()`       | Dictionary ki copy        |
| `setdefault()` | Key nahi ho to add        |
| `fromkeys()`   | Keys se new dictionary    |

============================================================================
----------------------------------------------------------------------------
============================================================================

🧠 Chaaron data types ko ek saath compare karo:

* Ab tak tumne List, Tuple, Set aur Dictionary dekhe hain:

| Feature     | List  | Tuple | Set     | Dictionary         |
| ----------- | ----- | ----- | ------- | -------------------|
| Syntax      | `[]`  | `()`  | `{}`    | `{key:value}`      |
| Ordered     | ✅    | ✅    | ❌*     | ✅                 |
| Duplicate   | ✅    | ✅    | ❌      | Keys ❌, Values ✅ |
| Mutable     | ✅    | ❌    | ✅      | ✅                 |
| Indexing    | ✅    | ✅    | ❌      | ❌                 |
| Data access | Index | Index | Element | Key                |

============================================================================

* Set ko unordered samajhna safest hai; set ka iteration order 
  guaranteed indexing/order jaisa nahi hota.

Ek line mein yaad karo:
-----------------------
LIST        → [10, 20, 30]
TUPLE       → (10, 20, 30)
SET         → {10, 20, 30}
DICTIONARY  → {"name": "Rahul", "age": 20}

List       = collection
Tuple      = fixed collection
Set        = unique collection
Dictionary = key-value collection