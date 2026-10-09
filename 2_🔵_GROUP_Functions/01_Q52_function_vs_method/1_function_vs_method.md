1. Sabse pehle ek line mein difference

* Function ek standalone/reusable block of code hota hai.

* Method bhi function hi hota hai, lekin woh kisi object/class 
  ke saath associated hota hai aur usually object ke through 
  call hota hai.

Example:
--------
# Function
len("Python")

Aur:

# Method
"python".upper()

--> Yahan len()  → function
--> Aur .upper() → method

============================================================================

2. Function kya tha?

* Function hum independently define kar sakte hain:

CODE:
-----
def add(a, b):
    return a + b

result = add(10, 20)   // Ab ise directly call karenge:
print(result)

Output: 30

<------------------------------------------------------>

* Notice karo:

add(10, 20)  // add ke aage kisi object ka naam nahi hai.
                Ye standalone function hai.

============================================================================

3. Method kya hota hai?

* Ab string dekho:

=> name = "rahul"  // String ke saath Python ne bahut saare operations 
                      already provide kiye hue hain.

For example:
------------
name.upper()

Output:
-------
RAHUL

<-------------------------------------------------->

Yahan:
------

--> name, ek object hai.

Aur:

--> .upper(), us object ka method hai.

Isliye:
-------
* name.upper() ko hum method call bolte hain.

============================================================================

4. Sabse important visual difference:

Function
--------
function(object)

Example:
--------
len("Python")

<------------------------------------------------>

Structure:
----------

len()
 ↓
Function
 ↓
"Python" → input

<------------------------------------------------>

Method
------
object.method()

Example:
--------
"Python".upper()

<------------------------------------------------>

Structure:
----------

"Python"
   ↓
 .upper()
   ↓
 Method

<------------------------------------------------>

* Isliye beginner ke liye ye pattern yaad rakho:

FUNCTION:
---------
function_name(data)


METHOD:
-------
data.method_name()

============================================================================

5. Ek real example: String

Maan lo:
--------
name = "rahul"

Function
--------
len(name)      // len() ek built-in function hai.

----------------------------------------------------------------------------

Method
------
name.upper()            // upper() ek string method hai.

Aur:
----
name.lower()            // lower() bhi method hai.

name.capitalize()       // Ye bhi method hai.

name.replace("r", "R")  // Ye bhi method hai.

============================================================================

6. Ek bahut important confusion

Tum soch sakte ho:
------------------
* "Lekin len() bhi string par kaam kar raha hai aur upper() 
   bhi string par kaam kar raha hai. Phir difference kya?"

**Excellent question.**

----------------------------------------------------------------------------

# Difference mainly kis tarah associated hai:

=> len(name)   // len ek standalone function hai jo object 
                  ko argument ke roop mein leta hai.

Whereas:

=> name.upper()  // upper string object ka method hai.

--> Yaani method object ke saath attached/associated hota hai.

============================================================================

7. Object kya hai?

* Method samajhne ke liye object ka basic idea clear hona chahiye.

Example:
--------
name = "Rahul"                         // "Rahul" ek string object hai.

numbers = [10, 20, 30]                 // numbers ek list object hai.

person = {"name": "Rahul", "age": 20}  // Ye dictionary object hai.

--> Different objects ke different methods ho sakte hain.

============================================================================

8. List ka example

Maan lo:
--------
numbers = [10, 20, 30]
numbers.append(40)       // List ka method:
print(numbers)

Output:
-------
[10, 20, 30, 40]

<----------------------------------------------->

* Yahan: append(), method hai.

Kyun? Kyuki hum ise list object: numbers, ke through 
call kar rahe hain:

=> numbers.append(40)

============================================================================

9. Function vs Method side-by-side:

=> numbers = [10, 20, 30]

Function
--------
len(numbers)

Method
------
numbers.append(40)

Visual:
-------
FUNCTION
   ↓
len(numbers)


METHOD
   ↓
numbers.append(40)
↑              ↑
object       method

============================================================================

10. Ek aur example: String

=> text = "hello world"

Function:
---------
=> len(text)

<------------------------------------------>

Method:
-------
text.upper()                    // Method
text.title()                    // Method
text.replace("world", "Python") // Method

So:
---
len(text)
   ↑
 function

text.upper()
     ↑
   method

============================================================================

11. Function hum khud bana sakte hain:

Example:
--------
def greet(name):
    return "Hello " + name

Call:
-----
greet("Rahul")  // Ye function hai.

* Humne ise kisi particular object ke andar nahi banaya.

============================================================================

12. Method usually class ke andar define hota hai

* Ab yahan se actual difference aur clear hoga.

* Python mein hum class bana sakte hain:

CODE:
-----
class Student:

    def greet(self):
        print("Hello student")

Yahan:
------
greet()              // class ke andar define hua hai, Isliye ye method hai.
student1 = Student() // Ab object banao:
student1.greet()     // Aur method call karo:

Output:
-------
Hello student

Notice:
-------
student1.greet()  // greet() ko hum object student1 ke through call kar 
                     rahe hain.

============================================================================

13. self kya hai?

* Method ke saath ek aur important concept aata hai:

CODE:
-----
class Student:

    def greet(self):
        print("Hello")

Yahan:
------
self    // current object ko represent karta hai.

Example:
--------
class Student:

    def __init__(self, name):
        self.name = name

    def greet(self):
        print("Hello", self.name)

Ab:
---
student1 = Student("Rahul")
student2 = Student("Aman")

Call:
-----
student1.greet()

Output:
-------
Hello Rahul

Aur:
----
student2.greet()

Output:
-------
Hello Aman

Same method: greet(), Lekin different objects ke saath 
                      kaam kar raha hai.

============================================================================

14. self ko simple language mein samjho:

=> student1.greet()   // Conceptually Python internally current object 
                         ko method ke saath associate karta hai.

Roughly:
--------
student1
   ↓
greet()
   ↓
self = student1

<--------------------------------------------->

Aur:
----
=> student2.greet()

mein:
-----
student2
   ↓
greet()
   ↓
self = student2

<--------------------------------------------->

Isliye:
-------
=> self.name  // ka matlab hota hai: "Jo current object hai, 
                                      uska name."

============================================================================

15. Function aur method ko table se samjho:

| Function                                     | Method
| -------------------------------------------- | ----------------------------
| Standalone hota hai                          | Object/class se associated 
                                                 hota hai

| Direct call hota hai                         | Usually object ke through  
                                                 call hota hai

| `function()`                                 | `object.method()`     

| Example: `len(x)`                            | Example: `x.upper()`    

| `def` se outside class define ho sakta hai   | Usually class ke andar define 
                                                 hota hai

| Object ko argument ke roop mein le sakta hai | Object ke context mein operate 
                                                 karta hai

============================================================================

16. Ek common mistake

* Beginners kabhi-kabhi likhte hain:

name = "Rahul"
upper(name)    ❌ Ye generally sahi nahi hai, 
                  kyunki upper() string ka 
                  method hai.

Sahi:
-----
name.upper()

<------------------------------------------------>

Aur:
----
numbers = [10, 20, 30]
append(numbers, 40)     // ❌ Aise nahi.

Sahi:
-----
numbers.append(40)

============================================================================

17. Lekin len() method kyun nahi hai?

* Ye bahut common interview/exam question hai.

Hum likhte hain:
----------------
=> len(numbers)

na ki:
------
=> numbers.len()

<---------------------------------------------------->

* Kyun? Kyuki Python mein len() built-in function hai.

* Python ka design aisa hai ki length lene ke liye 
  generic function:

=> len()  // use hota hai.

<---------------------------------------------------->

# Lekin list mein:

append()
remove()
sort()
reverse()

--> jaise operations methods hain.

<---------------------------------------------------->

Example:
--------
numbers = [30, 10, 20]
len(numbers)

numbers.append(40)
numbers.sort()
numbers.reverse()

============================================================================

19. Kya har method function hota hai?

* Conceptually haan — method Python mein function ka ek specialized 
                      form samjha ja sakta hai.

Lekin terminology mein:
-----------------------
def add(a, b):
    return a + b

→ function

<--------------------------------------------->

Aur class ke andar:
-------------------
class Calculator:

    def add(self, a, b):
        return a + b

→ method

* Difference mainly context/association ka hai.

============================================================================

20. Ek hi example mein dono:

CODE:
-----
def greet(name):
    return "Hello " + name

class Student:

    def __init__(self, name):
        self.name = name

    def introduce(self):
        return "I am " + self.name

Ab:
---
print(greet("Rahul"))        // greet() → function

Aur:
----
student = Student("Rahul")
print(student.introduce())  // introduce() → method

============================================================================

21. Ek shortcut yaad rakhna

* Jab bhi Python code dekho, pehle ye dekho:

Aise hai?
---------
something(...)   // Toh likely function hai.

Examples:
---------
print()
len()
type()
sum()
max()

<------------------------------------------------>

Aise hai?
---------
something.method(...)  // Toh likely method hai.

Examples:
---------
name.upper()
name.lower()

numbers.append(10)
numbers.sort()

text.replace("a", "b")

============================================================================

22. Lekin ek advanced point

* Har object.something() ko blindly method mat samajhna.

* Python mein attributes, callable objects, class methods, 
  static methods, descriptors jaise concepts bhi hain.

Lekin beginner level par:
-------------------------
function()

vs

object.method()

--> ye distinction bilkul sufficient hai.

============================================================================

23. Final picture

* Isko yaad rakho:

                    PYTHON
                       │
             ┌─────────┴─────────┐
             │                   │
          FUNCTION             METHOD
             │                   │
       independent          object/class
         operation           associated
             │                   │
       add(2, 3)          name.upper()
       len(list)          list.append()
       print()            list.sort()

----------------------------------------------------------------------------

# Ekdum simple definition:

Function:
---------
Aisa reusable code block jise hum directly call kar sakte hain.

CODE:
-----
def add(a, b):
    return a + b

add(10, 20)

----------------------------------------------------------------------------

Method:
-------
Aisa function jo kisi object/class ke context mein associated 
hota hai aur commonly object ke through call hota hai.

name = "rahul"
name.upper()

----------------------------------------------------------------------------

* Sabse important pattern:

# Function
function(data)

# Method
data.method()