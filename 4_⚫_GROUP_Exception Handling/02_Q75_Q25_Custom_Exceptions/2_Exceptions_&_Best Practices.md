1. Exception kya hota hai?
--------------------------

Simple language mein: Program run hote waqt koi unexpected problem/error 
                      aaye, usse exception kehte hain.

Example:
--------
x = 10 / 0

Yahan Python:
-------------
"ZeroDivisionError" dega, kyunki 0 se divide nahi kar sakte.

================================================================================

2. Exception handling kya hai?
------------------------------

Exception handling ka matlab: Error ko properly handle karna taaki program 
                              unnecessarily crash na ho.

Iske liye:
----------
try:
    # risky code

except:
    # error handle

.use karte hain.

Example:
--------
try:
    x = 10 / 0

except ZeroDivisionError:
    print("Cannot divide by zero")

Output: Cannot divide by zero

================================================================================

3. Best Practice #1 — Specific exception catch karo:
----------------------------------------------------

Ye avoid karna:
---------------
try:
    x = 10 / 0

except:
    print("Something went wrong")

* Isme problem ye hai ki tumne kaunsa error hua, ye specify nahi kiya.

<--------------------------------------------------------------------->

Better:
-------
try:
    x = 10 / 0

except ZeroDivisionError:
    print("Cannot divide by zero")

* Ab clearly pata hai ki hum kis problem ko handle kar rahe hain.

Simple rule:
------------
❌ except:
✅ except ZeroDivisionError:

================================================================================

4. Best Practice #2 — Multiple exceptions ko properly handle karo:
------------------------------------------------------------------

Maan lo:
--------
try:
    number = int(input("Enter number: "))
    result = 100 / number

except ValueError:
    print("Please enter a valid number")

except ZeroDivisionError:
    print("Number cannot be zero")

Ab:
---
hello → ValueError
0     → ZeroDivisionError
10    → successful

* Har problem ka appropriate message mil raha hai.

================================================================================

5. Best Practice #3 — Error ko hide mat karo:
---------------------------------------------

* Ye bad practice hai:

try:
    x = 10 / 0

except:
    pass    // pass ka matlab yahan essentially: "Error aaya? Kuch mat karo."

Problem:
--------
Error hua
   ↓
Python ne exception di
   ↓
except ne chup kara diya
   ↓
Tumhe pata hi nahi chala ki problem kya thi

* Debugging difficult ho jayegi.

================================================================================

6. Best Practice #4 — finally se cleanup:
-----------------------------------------

* Agar koi resource use kiya hai, toh cleanup important hai.

Example:
--------
file = None

try:
    file = open("data.txt")
    # file ke saath kaam

except FileNotFoundError:
    print("File not found")

finally:
    if file:
        file.close()


* finally normally execute hota hai, isliye cleanup ke liye useful hai.

* Modern Python mein files ke liye usually with open(...) preferred hota 
  hai, jise baad mein separately seekhna useful rahega.

================================================================================

7. Best Practice #5 — Useful error message do:
----------------------------------------------

Bad:
----
except ValueError:
    print("Error")

Better:
-------
except ValueError:
    print("Please enter a valid integer.")

* User ko samajh aata hai ki problem kya hai aur kya karna hai.

================================================================================

8. raise kya hota hai?
----------------------

* Ye bhi exception handling ka important concept hai.

* raise ka matlab: Khud se exception generate karna.

Example:
--------
age = -5

if age < 0:
    raise ValueError("Age cannot be negative")

. Yahan hum Python ko bol rahe hain: "Agar age negative hai, 
                                      toh ValueError raise karo."

================================================================================

9. Real example:
----------------
age = -5

if age < 0:
    raise ValueError("Age cannot be negative")

print(age)

* Program print(age) tak normally nahi pahunchega, kyunki humne  
  exception raise kar di.

================================================================================

10. try-except + raise:
-----------------------

* Ye thoda advanced but important pattern hai:

CODE:
-----
try:
    age = int(input("Enter age: "))

    if age < 0:
        raise ValueError("Age cannot be negative")

except ValueError as e:
    print("Invalid input:", e)

<-------------------------------------------------->

Agar user -5 deta hai:
----------------------
Invalid input: Age cannot be negative

Yahan:
------
except ValueError as e: mein e exception object ko 
                        represent karta hai.

Aur:
----
print(e), se exception ka message mil sakta hai.

================================================================================

11. Complete exception structure:
---------------------------------

* Ab tumhare paas poora picture hai:

try:
    # risky code

except SomeException:
    # error handle

else:
    # try successful hua toh

finally:
    # normally cleanup/final action

Aur raise:
----------
raise ValueError("Something is wrong")

→ khud exception generate karna.

================================================================================

# Interview answer

Q) Agar interviewer pooche: "What are exceptions and what are some best 
                             practices for handling them?"

Tum bol sakte ho:
-----------------
Exceptions are runtime errors or unexpected conditions that interrupt the normal 
flow of a program. We can handle them using try-except. Best practices include 
catching specific exceptions instead of using a bare except, providing meaningful 
error messages, avoiding silently ignoring exceptions, and using finally or 
appropriate cleanup mechanisms when necessary.

--------------------------------------------------------------------------------

Key Points
----------
1. Use try, except, and finally for exception handling.
2. Catch specific exceptions to avoid masking errors.
3. Use else with try for code that should run if no exception occurs.
4. Keep error handling logic separate from business logic.
5. Log exceptions for easier debugging and monitoring.

Real World Example
------------------
def divide(a, b):
    try:
        result = a / b
    except ZeroDivisionError:
        return "Error: Cannot divide by zero."
    else:
        return result
    finally:
        print("Execution completed.")

print(divide(10, 0))