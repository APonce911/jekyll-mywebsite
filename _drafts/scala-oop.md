
<h3>Class Parameters <> Class Fields </h3>

Class arguments cannot be assessed outside theinstance, to do that, you need a class field.
To convert a class parameter to a class field, use val on the constructor.

<h3>Methods Overloading</h3>  

Overloading means same method name, but different signature.
Signature means number of aparameters, or parameters with different types. It can result a different return type for the function, but it is not necessary to define overloading.

<h3>Auxiliary constructors</h3>

Is a method overloading for the parent method, implemented with different signature.
Auxiliary constructors can be exchanged by default values on the class constructor 

<h3>Syntatic Sugar: Method Notations</h3>

Infix notation
Methods with one parameter can be called this way:

mary.likes("Inception") === mary likes "Inception"

Operators (Ex: +) are equivalento to methods called with Infix notation
Unary operations(-1), are equivalento to methods called with Prefix notation.

-1 === 1.unary_-

Methods without parameters can be called with Postfix Notation

airton.isStudying === airton isStudying

Calling an instance as an function, is the same calling the apply method.

airton() ===  airton.apply()