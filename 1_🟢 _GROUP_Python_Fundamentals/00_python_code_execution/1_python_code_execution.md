TU
│
│ Python code likha
↓
hello.py
│
│
↓
python3
│
│ Ubuntu CPython executable start karta hai
↓
CPython
│
│ source code ko compile karta hai
↓
Python BYTECODE
│
│ CPU ise directly nahi samajhta
↓
CPython RUNTIME / BYTECODE EXECUTION MECHANISM
│
│ bytecode instructions ko read/execute karta hai
↓
CPython ke machine-level operations
│
↓
CPU
│
↓
actual result

======================================================================================

Notes ke liye final definition:
-------------------------------
Python ek high-level programming language hai. Commonly used CPython implementation 
mein, Python source code ko sabse pehle parse kiya jata hai, yani CPython code ki 
syntax aur structure ko check aur understand karta hai. Uske baad source code ko 
compile karke bytecode mein convert kiya jata hai. Ye bytecode Python ki intermediate instructions hoti hain. Phir CPython runtime is bytecode ko execute karta hai, jisme 
bytecode instructions ko generally sequentially, yani ek ke baad ek execute kiya jata 
hai. CPU Python bytecode ko directly execute nahi karta; CPython khud ek native program 
hai jo CPU par run hota hai aur bytecode ko execute karta hai.

Python Source Code
        ↓
      Parse
(syntax + structure check/understand)
        ↓
      Compile
        ↓
     Bytecode
(intermediate instructions)
        ↓
 CPython Runtime
        ↓
Bytecode instructions
ek ke baad ek execute
        ↓
       CPU
        ↓
      Output

======================================================================================

So the simplified execution flow is:
------------------------------------
Python Source Code → CPython Compiler → Bytecode → CPython Runtime → CPU → Output.