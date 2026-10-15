* Ab tum Has-a Relationship samajh chuke ho, toh ab uske dono types ko 
  samajhna easy hoga: Composition aur Aggregation.

* Sabse pehle ek important baat: dono Has-a Relationship hain. Difference 
  ye hai ki ek object doosre object ko kitni strongly own ya manage karta 
  hai.

=================================================================================

1. Pehle real-life example se samjho:
-------------------------------------

* Maan lo hamare paas do examples hain:

- Composition: Car has an Engine.
- Aggregation: Department has Teachers.

--> Dono mein ek cheez ke paas doosri cheez hai. Toh phir difference 
    kya hai?

---------------------------------------------------------------------------------

# Composition — strong ownership:

* Socho ek Car object apne Engine object ko khud create karta hai aur 
  usko apne internal part ki tarah manage karta hai.

Car object
    |
Engine object
Car ke andar manage ho raha hai

- Composition: strong ownership

* Is tarah ke design mein Engine ko Car ke andar hi banaya aur manage 
  kiya ja sakta hai. Car ke design mein Engine uska closely managed 
  part hai.

---------------------------------------------------------------------------------

# Aggregation — weaker ownership:

* Ab Department aur Teacher ka example lo.

* Ek Teacher pehle se exist karta hai. Baad mein Department us Teacher 
  ka reference apne paas rakh leta hai.

Department object
Teacher ka reference rakhta hai
           |
Teacher object
Department ke bahar bhi exist kar sakta hai

* Aggregation: weaker ownership

---------------------------------------------------------------------------------

- Yahan Teacher Department se alag bhi exist kar sakta hai. Department 
  ka reference hat jaane ka matlab ye nahi ki Teacher object ko zaroor 
  destroy hona hi hai.

- Dhyan rahe: Car–Engine aur Department–Teacher common examples hain; 
  actual classification tumhare program ke design aur ownership rules 
  par depend karti hai.

=================================================================================

2. Ab Python code se difference dekho:
--------------------------------------

A. Composition:
---------------
class Engine:
    def start(self):
        print("Engine started")

class Car:
    def __init__(self):
        self.engine = Engine()

car1 = Car()
car1.engine.start()

Output:
-------
Engine started

Ismein important line hai:
--------------------------
=> self.engine = Engine()

* Jab Car object initialize hota hai, tab uske andar Engine object 
  bhi banaya jaata hai.

---------------------------------------------------------------------------------

Sequence:
---------
car1 = Car()
     |
Car object initialize hota hai
     |
Engine() se Engine object banta hai
     |
Car ka engine attribute uska reference rakhta hai

* Yahan Composition kyun? Kyunki is example mein Car khud apna 
  Engine object create aur manage kar rahi hai. Ye strong 
  ownership ko represent karne wala design hai.

---------------------------------------------------------------------------------
---------------------------------------------------------------------------------

# B. Aggregation:

CODE:
-----
class Teacher:
    def __init__(self, name):
        self.name = name


class Department:
    def __init__(self, teacher):
        self.teacher = teacher


t1 = Teacher("Rahul")
d1 = Department(t1)
print(d1.teacher.name)

Output:
-------
Rahul

Important lines:
----------------
t1 = Teacher("Rahul")
d1 = Department(t1)

---------------------------------------------------------------------------------

Yahan sequence alag hai:
------------------------

Step 1: t1 = Teacher("Rahul")
Teacher object pehle se ban gaya
           |
Step 2: d1 = Department(t1)
Existing Teacher object Department ko diya
           |
Department ka teacher attribute
Usi Teacher object ka reference rakhta hai

* Yahan Aggregation kyun? Kyunki Teacher object Department banne se 
  pehle exist karta hai aur Department se alag bhi exist kar sakta 
  hai.

=================================================================================

3. Dono ka main difference:

Feature             | Composition              | Aggregation
--------------------|--------------------------|-------------------------
Relationship        | Has-a                    | Has-a
Ownership           | Strong                   | Comparatively weak
Object kaise milta? | Aksar andar create hota  | Existing object pass hota
Independence        | Closely connected        | Alag exist kar sakta hai
Example             | Car aur Engine           | Department aur Teacher

=================================================================================

4. Ek important clarification:

* Python mein Composition aur Aggregation ke liye alag syntax ya special 
  keywords nahi hain. Dono ko objects aur attributes ke through implement 
  kiya ja sakta hai.

* Aur sirf ye dekhkar ki object class ke andar create hua hai ya bahar se 
  pass hua hai, har situation mein final classification decide nahi hoti. 
  Asli difference ownership aur object ki lifecycle/design mein hota hai.

Yaad rakhne ka simplest tareeka:
--------------------------------
- Has-a       : Ek object doosre object ko refer karta hai.
- Composition : Has-a + strong ownership.
- Aggregation : Has-a + weaker ownership; doosra object independently 
                exist kar sakta hai.

- Abhi ke liye itna pakka kar lo. Agla natural step hai Composition aur 
  Aggregation ke code ko line-by-line compare karna, taaki tum khud 
  identify kar sako ki kis program mein kaunsa relationship hai.

=================================================================================
---------------------------------------------------------------------------------
=================================================================================

Doubt:
------
muje itna code samjhao
class Department:
    def __init__(self, teacher):
        self.teacher = teacher
d1 = Department(t1)

t1 object  as argument, teacher paraneter mai assign ho gaya
toh ye self.teacher mai kis tarah assign hua as object yaa 
object ki value Rahul kyuki aisa print(d1.teacher.name) krne 
par toh Rahul print ho raha hai ??

---------------------------------------------------------------------------------

* Tumhara doubt bilkul sahi hai. Tum soch rahe ho: teacher parameter 
  mein t1 aaya, toh self.teacher mein poora object store hua ya uski 
  value "Rahul"? Aur agar object store hua, toh .name se Rahul kaise 
  mila?

=================================================================================

Chalo, ek-ek step trace karte hain:
-----------------------------------

1. Pehle poora code dekho

CODE:
-----
class Teacher:
    def __init__(self, name):
        self.name = name

class Department:
    def __init__(self, teacher):
        self.teacher = teacher

t1 = Teacher("Rahul")
d1 = Department(t1)
print(d1.teacher.name)

Output:
-------
Rahul

=================================================================================

2. Sabse pehle t1 mein kya hai ?

=> t1 = Teacher("Rahul")

* Isse ek Teacher object banta hai. Us object ke andar name attribute 
  ki value "Rahul" hai.

   t1
Reference
    |
Teacher object
name = "Rahul"

* Dhyan do: t1 mein "Rahul" directly store nahi hai. t1 Teacher object 
            ka reference rakhta hai. "Rahul" us object ke name attribute 
            mein hai.

=================================================================================

3. Ab d1 = Department(t1) ko samjho:

=> d1 = Department(t1)

* Python t1 ke through Teacher object ka reference Department ke teacher 
  parameter ko deta hai.

Phir ye line execute hoti hai:
------------------------------
=> self.teacher = teacher

Yahan:
------
- teacher parameter Teacher object ka reference rakhta hai.
- self.teacher Department object ka attribute hai.
- Assignment se wahi reference self.teacher mein store ho 
  jata hai.

---------------------------------------------------------------------------------

* Isliye self.teacher mein "Rahul" nahi, Teacher object ka reference 
  store hua hai.

t1
Teacher object ka reference
        |
teacher parameter
Wahi object ka reference
        |
self.teacher
Department object mein wahi reference
        |
Wahi Teacher object
name = "Rahul"

* Yaani t1 aur d1.teacher dono usi Teacher object ko refer karte hain.

=================================================================================

4. Phir d1.teacher.name se Rahul kaise print hua ?

* Is expression ko right se samajhne ke bajaye, ek-ek step mein padho:

=> d1.teacher.name

--------------------------------------------------------------------
Expression	          Kya milta hai ?
--------------------------------------------------------------------
d1	                  Department object
--------------------------------------------------------------------
d1.teacher	          Us Department ka teacher attribute, jo Teacher 
                      object ka reference hai
--------------------------------------------------------------------
d1.teacher.name	      Us Teacher object ka name attribute, jiski value 
                      "Rahul" hai
--------------------------------------------------------------------


Copy karne ke liye:
-------------------
d1
 |
 v
Department object
 |
 | .teacher
 v
Teacher object
 |
 | .name
 v
"Rahul"


Isliye:
-------
print(d1.teacher.name)

Output:
-------
Rahul

=================================================================================

5. Ek chhota experiment

* Ye code chala kar dekho:

t1 = Teacher("Rahul")
d1 = Department(t1)

print(d1.teacher is t1)
print(d1.teacher.name)

Output:
-------
True
Rahul


- True ka matlab d1.teacher aur t1 dono wahi object refer karte hain.
- Rahul us object ke name attribute ki value hai.

Final answer: self.teacher mein Teacher object ka reference assign hua 
              hai, "Rahul" nahi. "Rahul" tak pahunchne ke liye pehle 
              d1.teacher se Teacher object milta hai, phir .name se 
              uski value milti hai.