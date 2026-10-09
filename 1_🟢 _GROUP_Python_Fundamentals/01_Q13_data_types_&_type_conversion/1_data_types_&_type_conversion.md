Quick Revision
--------------

| Data Type  | Example         | Use                     |
| ---------- | --------------- | ----------------------- |
| `int`      | `10`            | Whole number            |
| `float`    | `10.5`          | Decimal                 |
| `complex`  | `2+3j`          | Complex numbers         |
| `str`      | `"Hello"`       | Text                    |
| `bool`     | `True`          | True/False              |
| `list`     | `[1, 2, 3]`     | Changeable collection   |
| `tuple`    | `(1, 2, 3)`     | Unchangeable collection |
| `set`      | `{1, 2, 3}`     | Unique values           |
| `dict`     | `{"name": "A"}` | Key-value data          |
| `NoneType` | `None`          | No value                |

=================================================================================

# Type Conversion

Type conversion ka matlab hai ek data type ko doosre data type 
mein convert karna.

* Python mein commonly ye functions use hote hain:

int()
float()
str()
bool()
list()
tuple()
set()

---------------------------------------------------------------------------------

int()
-----
* String/float ko integer mein convert kar sakte hain.

* Converting string to integer

CODE:
-----
x = "10"
y = int(x)

print(y)
print(type(y))

Output: 
-------
10
<class 'int'>

-----------------------------------------------------------

* Converting float to integer

Float:
------

x = 10.8
print(int(x))

Output:
-------
10

⚠️ Decimal part remove ho jaata hai; rounding nahi hoti.

---------------------------------------------------------------------------------

* String to float:

float()
-------
x = "10.5"
y = float(x)

print(y)

Output:
-------
10.5

---------------------------------------------------------------------------------

* integer to string:

str()
-----
* Kisi value ko string mein convert karna:

age = 20
age = str(age)
print(type(age))

Output:
-------
<class 'str'>

<------------------------------------------------->

* Ye especially useful hai jab number ko text ke 
  saath combine karna ho:

age = 20
print("My age is " + str(age))

---------------------------------------------------------------------------------

bool()
------
* Value ko True ya False mein convert karta hai.

print(bool(1))
print(bool(0))

Output:
-------
True
False

Generally:
----------
bool(10)       # True
bool(-5)       # True
bool(0)        # False
bool("Hello")  # True
bool("")       # False

=================================================================================

# Ek Important Example

* Maan lo user se age input le rahe ho:

CODE:
-----
age = input("Enter your age: ")
print(type(age))

Agar user 20 enter karta hai, tab bhi:
--------------------------------------
<class 'str'>

. Kyunki input() hamesha string return karta hai.

---------------------------------------------------------------------------------

Isliye:
-------
age = int(input("Enter your age: "))
print(type(age))

Ab output:
----------
<class 'int'>

* Ye concept Python mein bahut important hai.

---------------------------------------------------------------------------------

Yaad rakhne ka simple rule:
---------------------------

=> input() → string

Agar number chahiye:
--------------------
age = int(input("Enter age: "))

Decimal chahiye:
----------------
price = float(input("Enter price: "))