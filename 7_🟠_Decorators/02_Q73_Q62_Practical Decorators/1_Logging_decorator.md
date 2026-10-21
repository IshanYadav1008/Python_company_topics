Q73 — Logging Decorator
-----------------------

Meaning: Aisa decorator banana jo function execute hone se pehle aur 
         baad mein log/message print kare.

CODE:
-----
def logging_decorator(func):
    def wrapper():
        print("Starting function...")
        func()
        print("Function completed!")
    return wrapper

@logging_decorator
def place_order():
    print("Order placed successfully")

place_order()

Output:
-------
Starting function...
Order placed successfully
Function completed!

* Yahan logging_decorator function ke execution ko track kar raha 
  hai — kab start hua aur kab complete hua.

==========================================================================

Q62 — Decorators for Logging:
-----------------------------

* Meaning: Decorators ka use karke functions ki activity log karna. 
           Jaise function ka naam, arguments, return value ya 
           execution time record karna.
    
CODE:
-----
def logging_decorator(func):
    def wrapper(*args, **kwargs):
        print(f"Calling function: {func.__name__}")
        print(f"Arguments: {args}, {kwargs}")

        result = func(*args, **kwargs)

        print(f"Returned value: {result}")
        return result

    return wrapper

@logging_decorator
def add(a, b):
    return a + b

add(10, 20)

Output:
-------
Calling function: add
Arguments: (10, 20), {}
Returned value: 30

==========================================================================

# Dono mein difference:

Q73 — Logging decorator	        Q62 — Decorators for logging
--------------------------------------------------------------------
Basic logging decorator banana	Logging ke liye decorators ka use 
                                samajhna
--------------------------------------------------------------------
Start/end messages	            Function name, arguments, result 
                                jaise details log karna
--------------------------------------------------------------------
Beginner-level implementation	Thoda broader, practical application
--------------------------------------------------------------------