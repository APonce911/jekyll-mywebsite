
<h3>Class Parameters <> Class Fields </h3>

Class arguments cannot be assessed outside theinstance, to do that, you need a class field.
To convert a class parameter to a class field, use val on the constructor.

<h3>Methods Overloading</h3>  

Overloading means same method name, but different signature.
Signature means number of aparameters, or parameters with different types. It can result a different return type for the function, but it is not necessary to define overloading.

<h3>Auxiliary constructors</h3>

Is a method overloading for the parent method(apply or this), implemented with different signature.
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

<h3>Scala Objects</h3>

You can have Java's class level funcionality (methods called on the class, not on an instance of the class) using objects on Scala.
A Scala object is a definition af a type, and it's the only instance of that type (Singleton)

Companions: a Scala class with a Scala object on the same scope with the same name

<h3>Inheritance</h3>

Single class inheritance - one class can only extend a single class
private methods - allows use only on the parent class
protected methods - allows use on subclasses
public methods - anyone can access the method
When extending a class, you must specify the correct constructors.

Polimorphysm
a method call will use the most overwritten version of a method.
EX Animal - Dog eat methods

overRiDING vs overLoading

overRiding: Supplying different implementation on derived classes. Can be implemented on constructor or on the body of derived classes
overLoading: Supplying multiple names with same name on the same class, but different signatures.

Super
call methods in the super(parent) class

Final
prevent derived classes to override method/var
prevent derived classes to inherit

Sealed
Can be extended on THIS file, and prevent on other files.

Abstract members
When you leave classes / methods / fields unimplemented

Traits
Like abstract classes, can have unimplemented fields and methods, but can be inherited along classes.