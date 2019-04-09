---
title: "Inheritance - Scala for the impatient"
date: 2019-04-08 20:12:00
lang: en
ref: inheritance-sfti

---

This is the second part of my contrubution to Gympass' Scala study group. Scala for the Impatient, chapter 8: Inheritance.

<h2>Inheritance</h2>

  We will learn how inheritance works in Scala,:
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

We can specify fields and methods that are new to the subclass or that override methods in the superclass.

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
  Use <i>isInstanceOf</i> to test if an object belogs to a class or a subclass of it.
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

<h3>Protected Filds and Methods</h3>

  A method or field can be declared as <i>protected</i> and it can be visible only for subclasses, and not throughout the package.

<h3>Superclass Construction</h3>



<h3>Overriding Fields</h3>
<h3>Anonymous Subclasses</h3>
<h3>Abstract Classes</h3>
<h3>Abstract Fields</h3>
<h3>Construction Orded and Early Definitions</h3>
<h3>The Scala Inheritance Hierarchy</h3>
<h3>Object Equality</h3>
