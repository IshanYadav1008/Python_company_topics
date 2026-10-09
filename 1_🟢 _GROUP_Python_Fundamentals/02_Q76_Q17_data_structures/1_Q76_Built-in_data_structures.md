1. Built-in Data Structures
---------------------------

Python mein data structure ka matlab hai data ko organize 
aur store karne ka tareeka.

* Python ke important built-in data structures hain:

# 1. List : Ordered aur mutable collection.
-------------------------------------------

fruits = ["apple", "banana", "mango"]
print(fruits[0])

Output:
-------
apple

. Ordered ✅
. Mutable ✅
. Duplicates allowed ✅
. Indexing available ✅

=============================================================================

# 2. Tuple
----------

* Ordered but immutable collection.

colors = ("red", "green", "blue")

. Ordered ✅
. Mutable ❌
. Duplicates allowed ✅
. Indexing available ✅

=============================================================================

# 3. Set

Unique elements ka collection.

numbers = {1, 2, 3, 4}

Example:
--------
numbers = {1, 2, 2, 3}
print(numbers)

Output mein 2 ek hi baar rahega.

. Unique values ✅
. Duplicates ❌
. Mutable ✅
. Normal indexing ❌

=============================================================================

# 4. Dictionary

* Data ko key-value pairs mein store karta hai.

student = {
    "name": "Rahul",
    "age": 20
}

Access:
-------
print(student["name"])

Output:
-------
Rahul

=============================================================================

| Data Structure | Ordered | Mutable | Duplicates |
| -------------- | ------- | ------- | ---------- |
| List           | ✅       | ✅       | ✅       |
| Tuple          | ✅       | ❌       | ✅       |
| Set            | ❌*      | ✅       | ❌       |
| Dictionary     | ✅       | ✅       | Keys ❌  |

* Modern Python sets ka iteration order insertion order jaisa appear 
  kar sakta hai, lekin set ko indexed/sequence type nahi samajhna 
  chahiye.