---
title: "Inheritance - Scala for the impatient"
date: 2019-04-10 06:50:00
lang: en
ref: inheritance-sfti

---

This is the second part of my contribution to Gympass' Scala study group. Scala for the Impatient, chapter 8: Inheritance.

<h2>Inheritance</h2>

  Inheritance is the mechanism that allows a child class to access properties( defs/ vals/ vars) of its parent classes*.( or traits/ case classes/ abstract classes etc.).

  We will learn how inheritance works in Scala.
  Highlights:

- The extends and final keywords are as in Java.
- You must use override when you override a method.
- Only the primary constructor can call the primary superclass constructor.
- You can override fields.

<h3>Extending a Class</h3>


<pre>
  <code>
    class Employee extends Person {
      var salary: 0.0
      ...
    }
  </code></pre>

We can specify fields and methods that are new to the subclass or that overrides properties of the superclass.

It is possible to declare class <i>final</i> so that cannot be extended. It is also possible to do this to individual methods or fields so it can't be overridden.

<h3>Overriding Methods</h3>

We must use <i>override</i> when you override a method that isn't abstract

<pre>
  <code>
    public class Person {
    ...
      override def toString = getClass.getName + "[name=" + name + "]"
    }
  </code></pre>

Invoking a superclass method using <i>super</i>:

<pre>
  <code>
    public class Employee extends Person {
      ...
      override def toString = super.toString + "[salary=" + salary + "]"
    }
  </code></pre>

<h3>Type Check and Casts</h3>
  Use <i>isInstanceOf</i> to test if an object belongs to a class or a subclass of it.
  The method <i>asInstanceOf</i> is used to convert an object to a specific subclass.

  <pre>
    <code>
      if (p.isInstanceOf[Employee]) {
      val s = p.asInstanceOf[Employee] // s has type Employee
      ...
      }
    </code></pre>

  if you want to test an object to a specific class (without subclasses) use:

  <pre>
    <code>
      if (p.getClass == classOf[Employee])
    </code></pre>

  However, pattern matching is usually better than using type check and casts.

<h3>Protected Fields and Methods</h3>

  A method or field can be declared as <i>protected</i> and it can be visible only for subclasses, and not throughout the package.

<h3>Superclass Construction</h3>

  The primary constructor is intertwined with the class definition. The call to the superclass too.
  <pre>
    <code>
      class Employee(name: String, age: Int, val salary : Double) extends Person(name, age)
    </code></pre>

<h3>Overriding Fields</h3>

  You can override fields with another field with the same name.

  These are the restrictions:
  - A <i>def</i> can only override another <i>def</i>.
  - A <i>val</i> can override another <i>val</i> or a parameterless <i>def</i>.
  - A <i>var</i> can only override an abstract <i>var</i>.

  OBS: A <i>var</i> cannot be overridden. If you provide a var, all subclasses will be stuck with it

<h3>Anonymous Subclasses</h3>

  An anonymous subclass is created when you include a block with definitions or overrides. (Object with structural type) Ex:

  <pre>
    <code>
      val alien = new Person("Fred") {
        def greeting = "Greetings, Earthling! My name is Fred."
      }
    </code></pre>

<h3>Abstract Classes</h3>

  Use <i>abstract</i> to create classes that cannot be instantiated.
  Used when one or more methods are not defined.

  No <i>override</i> needed on subclasses.

<h3>Abstract Fields</h3>

  An abstract field is a field without an initial value.

  No <i>override</i> needed on subclasses.

<h3>Construction Order and Early Definitions</h3>
  Construction order problem. Not sure when it occurs...

  early definition syntax is used instead of <i>final</i> or <i>lazy</i>

  You place the <i>val</i> fields in a block after the extends keyword:

  <pre>
    <code>
      class Bug extends {
        override val range = 3
      } with Creature
    </code></pre>

<h3>The Scala Inheritance Hierarchy</h3>

  <img src="assets/images/scala_hierarchy.png" alt="Scala Classes Hierarchy Diagram" style="max-width: 38rem">

<h3>Object Equality</h3>

  When we write a class we should consider overriding the <i>equals</i> method to provide an accurate representation for our class.

  Ex:

  <pre>
    <code>
      Class Item(val description: String, val price: Double)
      ...

      final override def equals(other: Any) = {
        val that = other.asInstanceOf[Item]
        if (that == null) false
          else description == that.description && price == that.price
        }
    </code></pre>

  OBS: The <i>equals</i> override only works for parameters with type Any.

  OBS2: Do not forget to override the <i>HashCode</i> too. Use only fields you use on equality check.

  <pre>
    <code>
      final override def hashCode = 13 * description.hashCode + 17 * price.hashCode
    </code></pre>

  In a normal application simply use == operator.
