This is my small scala sumary. Syntax comparisons will be made mainly against ruby and javascript.
Used the content of the following page https://www.scala-exercises.org/scala_tutorial

<h2>Terms & types</h2>
 <h3>Primitives</h3>
  they represent the simplest elements

  The integer 1
  <pre>
   <code>
    1
   </code>
  </pre>
  The double 1.572
  <pre>
   <code>
    1.572
   </code>
  </pre>
  The boolean value "true"
  <pre>
   <code>
    true
   </code>
  </pre>
  The text(String) "Hello"
  <pre>
   <code>
    "Hello"
   </code>
  </pre>
  IMPORTANT! Strings on Scala are different from ruby, which accepts both '' and "". On Scala always use "" for strings.
 <h3></h3>Operators
  1 + 2 = 3

  1 and 2 are operands
  + is the operator

  "Hello, " ++ "Scala"

  "Hello, " and "Scala" are operands
  ++ is the operator

 <h3></h3>Method Calls
  <pre>
   <code>
    "hello".size
   </code>
  </pre>

  "hello" is the target object
  size is the method

  Methods are applied on expressions using the dot notation.
  Method parameters are passed inside ().
 <h3>Operators are methods</h3>
 In fact, operators are methods with symbolic values, or symbolic identifier.

 <pre>
  <code>
   3 + 2 == 3.+(2)
   1.to(10) == 1 to 10
  </code>
 </pre>

 Each expression (or object) has a value and a type.

<h2>Definitions & Evaluations</h2>
 <h3>Naming</h3>
  Naming things gives more readability to your program
  Use Val to define constants and Def to define methods.
  val = value
  def = definition
 <h3>Methods</h3>
  Can have one or more parameters, separated with ',', and with its respective types defined after a ':'.
  ex:

  <pre>
   <code>
    def square(x: Double) = x * x
    def sumOfSquares(x: Double, y: Double) = square(x) + square(y)
   </code>
  </pre>

  If a method is recursive, i.e. call for itself, you need to specify its return type

  <pre>
   <code>
    def factorial(n: Int): Int =
      if (n ==1) 0
      else factorial(n - 1) * n
   </code>
  </pre>
 <h3>Evaluation</h3>
  The substitution model is a expression evaluation scheme.Used when the expression can be reduced to a value(not a loop).
  Call-by-Value
  1- Reduces arguments first
  2- Compute the function values,from left to right

  Call-by-Name
  1-Start computing the function values,from left to right
  2-Reduce arguments when necessary. Can let an argument unreduced if it's not used on function body.

<h2>Functional Loops</h2>
 <h3>Conditional</h3>

  <pre>
   <code>
    def abs(x: Double) = if (x >= 0) x else -x
   </code>
  </pre>
 <h3>Boolean Expressions</h3>
  <pre>
   <code>
    true  false      // Constants
    !b               // Negation
    b && b           // Conjunction
    b || b           // Disjunction

    e <= e, e >= e, e < e, e > e, e == e, e != e
   </code>
  </pre>

<h2>Lexical Scopes</h2>
 <h3>Nested Functions</h3>
  Are auxiliary functions defined inside the parent fucntion. Used to isolate a function from the user, just like private functions.
  <pre>
   <code>
    def sqrt(x: Double) = {
      def sqrtIter(guess: Double, x: Double): Double =
        if (isGoodEnough(guess, x)) guess
        else sqrtIter(improve(guess, x), x)

      def improve(guess: Double, x: Double) =
        (guess + x / guess) / 2

      def isGoodEnough(guess: Double, x: Double) =
        abs(square(guess) - x) < 0.001

      sqrtIter(1.0, x)
    }
   </code>
  </pre>
 <h3>Blocks</h3>
  -It contains a sequence of definitions or expressions.
  -The last element of a block is an expression that defines its value.
  -This return expression can be preceded by auxiliary definitions.
  -Blocks are themselves expressions; a block may appear everywhere an -expression can.
  -The definitions inside a block are only visible from within the block.
  -The definitions inside a block shadow definitions of the same names outside the block.
 <h3>Lexical Scoping</h3>
  definitions outside blocks are visible inside unless they are shadowed.(Would it be shadowed when redefined, right?)
  defactorinng sqrt method:
  <pre>
   <code>
    def sqrt(x: Double) = {
      def sqrtIter(guess: Double): Double =
        if (isGoodEnough(guess)) guess
        else sqrtIter(improve(guess))

      def improve(guess: Double) =
        (guess + x / guess) / 2

      def isGoodEnough(guess: Double) =
        abs(square(guess) - x) < 0.001

      sqrtIter(1.0)
    }
   </code>
  </pre>
 <h3>Semicolons</h3>
  In most cases semicolons are optional.
  Used when you have two statements in a single line
  When you have 2 long expressions, you can overcome implicit ';' by putting the expressions inside () or by putting the operator(+) on the first line.
  <pre>
   <code>
    someLongExpression +
      someOtherExpression
   </code>
  </pre>
 <h3>Top-level Definitions</h3>

  the Object MyExecutableProgram has nested definitions (vals, defs & methods) and is called top-level because is not nested within another definition.
 <h3>Packages and Imports</h3>
  top level definitions can be organized an imported as packages

  <pre>
   <code>
    // file foo/Baz.scala
    package foo
    object Baz {
      Bar.someMethod
      // Bar is visible because it is in the `foo` package too
    }
   </code>
  </pre>

  when some definitions are not visible, you must use fully qualified names to refer them:

  <pre>
   <code>
    // file quux/Quux.scala
    package quux
    object Quux {
      foo.Bar.someMethod
    }
   </code>
  </pre>

  here foo is a package(class?), Bar is an object and someMethod is a method

  you can also import and object to not repeat them:

  <pre>
   <code>
    // file quux/Quux.scala
    package quux
    import foo.Bar
    object Quux {
      // Bar refers to the imported `foo.Bar`
      Bar.someMethod
    }
   </code>
  </pre>
 <h3>Automatic Imports</h3>

  Any Scala application automatically imports the packages scala, java.lang and scala.Predef.
 <h3>Writing Executable Programs</h3>
  All executable applications should have a main method inside an object
  <pre>
   <code>
    object Hello {
      def main(args: Array[String]) = println("hello world!")
    }
   </code>
  </pre>
  and can be executed with the following code:
  <pre>
   <code>
    $ scala Hello
   </code>
  </pre>

<h2>Tail Recursion</h2>
 <h3>Recursive Function Application</h3>

  Maximum Common Divisor

  <pre>
   <code>
    def gcd(a: Int, b: Int): Int =
      if (b == 0) a else gcd(b, a % b)
   </code>
  </pre>

  Factorial

  <pre>
   <code>
    def factorial(n: Int): Int =
      if (n == 0) 1 else n * factorial(n - 1)
   </code>
  </pre>

  MCD oscillates and Factorial extends the number of elements on its expression.
 <h3>Tail Recursion</h3>

  Is when the last action of a method is to call itself. In case of the factorial method, its not tail recursive because after calling itself with factorial(n-1) it has to multiply to n.

  "Both factorial and gcd only call itself but in general, of course, a function could call other functions. So the generalization of tail recursion is that, if the last action of a function consists of calling another function, maybe the same, maybe some other function, the stack frame could be reused for both functions. Such calls are called tail calls."

  What is the stack frame?

  Its possible to require that the following defined fuction is recursive using the @tailrec annotation. If the function were not tail recursive, it would pront an error.

  Tail recursive factorial:
  <pre>
   <code>
    def factorial(n: Int): Int = {
      @tailrec
      def iter(x: Int, result: Int): Int =
        if (x == 1) result
        else iter(x - 1, result * x)

      iter(n,1)
    }
   </code>
  </pre>

<h2>Structuring Information</h2>
 <h3>Aggregating Information with Case Classes</h3>
  Case class has a syntax close to a JS object

  <pre>
   <code>
    case class Note(
      name: String,
      duration: String,
      octave: Int
    )
   </code>
  </pre>

  we can create values(like objects or instances) of this type calling its constructor(Note(...))

  val c3 = Note("C", "Quarter", 3)

  and we can access any property by using the dot notation, just like Ruby or Javascript.
 <h3>Defining Alternatives with Sealed Traits</h3>
  a type(here, Symbol) is something that can only be embodied by a fixed set of alternatives.We can express it using the sealed trait definition.For example, a musical symbol can be a note or a rest:

  <pre>
   <code>
    sealed trait Symbol
    case class Note(...) extends Symbol
    case class Rest(...) extends Symbol
   </code>
  </pre>
 <h3>Pattern Matching</h3>
  Works like a case function. If the object matches a pattern(LHS) it execute an expression(RHS). The arrow symbol(=>) separates the parernt from the expressions.

  Used to to distinguish between the different cases of symbols.
  <pre>
   <code>
    def symbolDuration(symbol: Symbol): String =
      symbol match {
        case Note(name, duration, octave) => duration
        case Rest(duration) => duration
      }
   </code>
  </pre>

  Here, Note(...) and Rest(...) are constructor patterns and duration is called variable pattern.
 <h3>Exhaustivity</h3>

  when not all cases of a Symbol are handled, the compiler informs us.
 <h3>Equals</h3>
  Comparing instances of case classes you compare their values.
  This is different from Ruby classes, where each instance is different from other, even if its properties are equal.
 <h3>Enumerations</h3>
  Fix a set of alternatives to a property.

  <pre>
   <code>
    sealed trait NoteName
    case object A extends NoteName
    case object B extends NoteName
    case object C extends NoteName
    …
    case object G extends NoteName
   </code>
  </pre>
 <h3>Algebraic Data Types</h3>
  if a part of a program can be formulated in terms of an <strong>is</strong> relationship, you will express it as a sealed trait:
  “A symbol is either a note or a rest.”

  if it can be formulated in terms of an  <strong>has</strong> relationship,you will express it as a case class:

  “A note has a name, a duration and an octave number.”
 <h3>Observations</h3>
  case class != case object

  case class is used to define a class(name, properties and parent(extends ...))
  case object is used to restrict the values of a property

<h2>Higher-Order Functions</h2>
 <h3>Higher-Order Functions</h3>

   On functional languages functions are trated as first-class values, meaning they can be passed as parameters and returned as a result. Those are named higher order functions.
 <h3>Motivation</h3>
  its possible to factor out various recursive higher-order functions.
  Examples:

  b>a

  Sum all integers between a and b
  <pre>
   <code>
    def sumInts(a: Int, b: Int): Int =
      if (a > b) 0 else a + sumInts(a + 1, b)
   </code>
  </pre>
  Sum the cubes of all the integers between a and b
  <pre>
   <code>
    def cube(x: Int): Int = x * x * x

    def sumCubes(a: Int, b: Int): Int =
      if (a > b) 0 else cube(a) + sumCubes(a + 1, b)
   </code>
  </pre>
  Sum the factorials of all the integers between a and b
  <pre>
   <code>
    def sumFactorials(a: Int, b: Int): Int =
      if (a > b) 0 else factorial(a) + sumFactorials(a + 1, b)
   </code>
  </pre>
 <h3>Summing with higher-order functions</h3>
  the functions above can be summarized passing the respective function (id/cube/factorial) as a parameter to a higher order function (sum).

  <pre>
   <code>
    def sum(f: Int => Int, a: Int, b: Int): Int =
      if (a > b) 0
      else f(a) + sum(f, a + 1, b)
   </code>
  </pre>

  <pre>
   <code>
    def id(x: Int): Int = x
    def sumInts(a: Int, b: Int) = sum(id, a, b)
    def sumCubes(a: Int, b: Int) = sum(cube, a, b)
    def sumFactorials(a: Int, b: Int) = sum(factorial, a, b)
   </code>
  </pre>
 <h3>Functions Types</h3>
  A => B
  A argument
  returns B
 <h3>Anonymous Functions</h3>
  Function literal. i.e. dont need to define a name for it
  Anonymous cube function:
  <pre>
   <code>
    (x: int) => x * x * x
   </code>
  </pre>

  (...) is the parameter
   x * x * x is the body
  the type of the parameter can be omitted. Multiple parameters are separated by commas.
 <h3>Syntactic Sugar</h3>
  are functions defined as below:
  why they are used? I don't know...
  <pre>
   <code>
    { def funcName(x1: T1, …, xn: Tn) = e ; funcName }
   </code>
  </pre>
 <h3>Summation with Anonymous Functions</h3>
  the respective functions(id/cube) are not defined and passed as parameters anymore. They are passed as literals on the higher order function (sum).
  <pre>
   <code>
    def sumInts(a: Int, b: Int) = sum(x => x, a, b)
    def sumCubes(a: Int, b: Int) = sum(x => x * x * x, a, b)
   </code>
  </pre>

<h2>Standard Library</h2>
 <h3>Lists</h3>
  They seems like an array, but they are not.
  they cannot be changes(immutable)
  they are recursive
  they are homogeneous; All elements have the same type

  Ex:

  <pre>
   <code>
    val fruit: List[String] = List("apples", "oranges", "pears")
    val nums: List[Int] = List(1, 2, 3, 4)
    val diag3: List[List[Int]] = List(List(1, 0, 0), List(0, 1, 0), List(0, 0, 1))
    val empty: List[Nothing] = List()
   </code>
  </pre>
 <h3>Constructors of Lists</h3>
  All lists are construted from:
  -the empty list nil
  -the construction operator(cons) ::
  x::xs gives a list with the first element x followed by the elements of xs, which is a list itself

  we use the cons operator because its the only way to add an element to a list. There is no .push method.
  <pre>
   <code>
    val nums = 1 :: 2 :: 3 :: 4 :: Nil
   </code>
  </pre>

  <pre>
   <code>
    val nums = Nil.::(4).::(3).::(2).::(1)
   </code>
  </pre>
 <h3>Manipulating Lists</h3>
  It's possible to decompose lists with pattern matching:
  <pre>
   <code>
    nums match {
      // Lists of `Int` that starts with `1` and then `2`
      case 1 :: 2 :: xs => …
      // Lists of length 1
      case x :: Nil => …
      // Same as `x :: Nil`
      case List(x) => …
      // The empty list, same as `Nil`
      case List() =>
      // A list that contains as only element another list that starts with `2`
      case List(2 :: xs) => …
    }
   </code>
  </pre>

  Insertion sort method:

  <pre>
   <code>
    val cond: (Int, Int) => Boolean = (x:Int,y:Int)=>x<y
    def insert(x: Int, xs: List[Int]): List[Int] =
      xs match {
        case List() => x :: Nil
        case y :: ys =>
          if (cond(x, y)) x :: y :: ys
          else y :: insert(x, ys)
      }

    insert(2, 1 :: 3 :: Nil) shouldBe (1 :: 2 :: 3 :: Nil)
    insert(1, 2 :: 3 :: Nil) shouldBe (1 :: 2 :: 3 :: Nil)
    insert(3, 1 :: 2 :: Nil) shouldBe (1 :: 2 :: 3 :: Nil)
   </code>
  </pre>

  This method is interesting because the condition (cond boolean) to place a element is an anomymous function, and its body is another anonymous function (boolean). So we have to define its parameters x,y and integers and also its body as x<y. The (Int,Int) part do not define it, its only the cond type.
 <h3>Common Operations on Lists</h3>
  .map(anonymous func)
  .filter(anonymous func)
  .flatMap{anonymous func}
 <h3>Optional Values</h3>
  Use options when you dont have a defined return type.
  Partially defined functions:

  <pre>
   <code>
    def sqrt(x: Double): Option[Double] =
      if (x < 0) None else Some(…)
   </code>
  </pre>
 <h3>Manipulating Options</h3>

  Use pattern matching to decompose options

  <pre>
   <code>
    def foo(x: Double): String =
      sqrt(x) match {
        case None => "no result"
        case Some(y) => y.toString
      }
   </code>
  </pre>
 <h3>Common Operations on Options</h3>
  .map(=>)
  .filter(=>)
  .flatMap(=>)
 <h3>Error Handling</h3>
  Try[A], represents a computation that attempted to return an A.
  Can be Success[A] or Failure;

  None x Failure
  Failure provide a reason of the failure

  Try[A] also have map, filter and flatMap

  Either[A,B], represents a value that can either be type A or type B, and can be decomposed in two cases: Left and Right.

  <pre>
   <code>
    def sqrt(x: Double): Either[String, Double] =
      if (x < 0) Left("x must be positive")
      else Right(…)
   </code>
  </pre>

  Either[A,B] have map and flatMap, but it transform the Right case only. "right biased".

  Either[A,B] has a filterOrElse method, it transforms a Right value into Left value if it does not satisfy a given predicate.

  Prior to Scala 2.12, Either was unbiased, so you had to specity the side you wanted to transform.

<h2>Syntatic Conveniences</h2>
 <h3>String Interpolation</h3>

  <pre>
   <code>
    def greet(name: String): String =
      s"Hello, $name!"

    greet("Scala") shouldBe "Hello, Scala!"
   </code>
  </pre>

  do not forget to prefix the string literal with "s"!!!

  If you want to splice a complex expression:

  <pre>
   <code>
    def greet(name: String): String =
      s"Hello, ${name.toUpperCase}!"

    greet("Scala") shouldBe "Hello, SCALA!"
   </code>
  </pre>

  IMPORTANT! Strings on Scala are different from ruby, which accepts both '' and "". On Scala always use "" for strings.
 <h3>Tuples</h3>
  work as a conjuntion of elements, and they can have different types.
  More generally, a type (T1, …, Tn) is a tuple type of n elements whose ith element has type Ti.

  You can retrieve the elements of a tuple using tuple pattern, or you can identify the member by its position (_i)

  <pre>
   <code>
    val is: (Int, String) = (42, "foo")
    is._1 shouldBe 42
    is._2 shouldBe "foo"
   </code>
  </pre>
 <h3>Functions as Objects</h3>
  Functions are objects with apply methods.
  <pre>
   <code>
    package scala
    trait Function1[A, B] {
      def apply(x: A): B
    }
   </code>
  </pre>
 <h3>Expansion of Function Values</h3>
  <pre>
   <code>
    {
      class AnonFun extends Function1[Int, Int] {
        def apply(x: Int) = x * x
      }
      new AnonFun
    }
   </code>
  </pre>
 <h3>Expansion of Function Calls</h3>
  f(a,b) = f.apply(a, b)
 <h3>For Expressions</h3>
  Map
  <pre>
   <code>
    /* xs.map(x => x + 1) */
    for (x <- xs) yield x + 1
   </code>
  </pre>
  Filter
  <pre>
   <code>
    /* xs.filter(x => x % 2 == 0) */
    for (x <- xs if x % 2 == 0) yield x
   </code>
  </pre>
  flatMap
  <pre>
   <code>
    /* xs.flatMap(x => ys.map(y => (x, y))) */
    for (x <- xs; y <- ys) yield (x, y)
   </code>
  </pre>
 <h3>Method's Parameters</h3>
  <pre>
   <code>
    Range(1, 10, 2)
   </code>
  </pre>
  Can be rewritten
  <pre>
   <code>
    case class Range(start: Int, end: Int, step: Int)
    Range(start = 1, end = 10, step = 2)
   </code>
  </pre>
  It's to set default values when defining the contructor, so the parameter can be omitted
   <pre>
    <code>
     case class Range(start: Int, end: Int, step: Int = 1)
    </code>
   </pre>

   Undefined number of parameters.
   <pre>
    <code>
     def average(x: Int, xs: Int*): Double =
      (x :: xs.to[List]).sum.toDouble / (xs.size + 1)
    </code>
   </pre>
 <h3>Type Aliases</h3>
  <pre>
   <code>
    type Result = Either[String, (Int, Int)]
    def divide(dividend: Int, divisor: Int): Result =
      if (divisor == 0) Left("Division by zero")
      else Right((dividend / divisor, dividend % divisor))
    divide(6, 4) shouldBe Right((1, 2))
    divide(2, 0) shouldBe Left("Division by zero")
   </code>
  </pre>

<h2>Object Oriented Programming</h2>
 <h3>Classes</h3>

  a class define a new constructor, and a new type.
 <h3>Objects</h3>
  Objects are the elements of a class type.
  Use the operator 'new' to create an object.
 <h3>Members of an Object</h3>
  Just like a property of a Ruby object, you can get the member of an object
  with the infix operator '.'
 <h3>Methods</h3>
   A package of functions operating on a data abstraction in the data abstraction itself.
   i.e. defined inside the class definition.
 <h3>Data Abstraction</h3>
 <h3>Self Reference</h3>

  'this' represents the object on which the current method is executed.
 <h3>Preconditions</h3>
  require is used to enforce a precondition on the caller of a function.

  require function
  <pre>
   <code>
    class Rational(x: Int, y: Int) {
      require(y > 0, "denominator must be positive")
      ...
    }
   </code>
  </pre>
 <h3>Assertions</h3>
  assert is used as to check the code of the function itself.
  <pre>
   <code>
    val x = sqrt(y)
    assert(x >= 0)
   </code>
  </pre>
 <h3>Constructors</h3>
 <h3>Operators</h3>
  as said before, operators are methods with symbolic identifiers. So you can override the operators for some types:

  <pre>
   <code>
    class Rational(x: Int, y: Int) {
      private def gcd(a: Int, b: Int): Int = if (b == 0) a else gcd(b, a % b)
      private val g = gcd(x, y)
      def numer = x / g
      def denom = y / g
      def + (r: Rational) =
        new Rational(
          numer * r.denom + r.numer * denom,
          denom * r.denom
        )
      def - (r: Rational) = ...
      def * (r: Rational) = ...
      ...
    }
   </code>
  </pre>
 <h3>Precedence Rules</h3>
  Increasing priority

  <pre>
   <code>
    (all letters)
    |
    ^
    &
    < >
    = !
    :
    + -
    * / %
    (all other special characters)
   </code>
  </pre>
 <h3>Abstract Classes</h3>

  No instances of an abstract class can be created with the operator new.
 <h3>Class Extensions</h3>
  subclasses extends superclass:

  <pre>
   <code>
    class NonEmpty(elem: Int, left: IntSet, right: IntSet) extends IntSet {
   </code>
  </pre>
  NonEmpty is a subclass and IntSet is its superclass.
  IntSet is a subclass of Object.
 <h3>Implementation and Overriding</h3>
  <pre>
   <code>
    abstract class Base {
      def foo = 1
      def bar: Int
    }

    class Sub extends Base {
      override def foo = 2
      def bar = 3
    }
   </code>
  </pre>
 <h3>Object Definitions</h3>
  When you need a single instance of a class (Empty for IntSet), you can create a singleton object named Empty. No other instances of it can be created. This type of object are values.

  <pre>
   <code>
    object Empty extends IntSet {
      def contains(x: Int): Boolean = false
      def incl(x: Int): IntSet = new NonEmpty(x, Empty, Empty)
    }
   </code>
  </pre>
 <h3>Traits</h3>
  use when you want to inherit code from more than one superclass.
  Defined just like an abstract class.
  OBS
  <pre>
   <code>
    trait Planar {
      def height: Int
      def width: Int
      def surface = height * width
    }
   </code>
  </pre>
  classes,objects and traits can inherit from one class,but from many traits:
  <pre>
   <code>
    class Square extends Shape with Planar with Movable …
   </code>
  </pre>

<h2>Imperative Programming</h2>
 The substitution model of computation cannot be used.
 The state of an object depend on its history.
 use 'var' to create a variable definition .
 use '=' to assign a new value to a variable.
 <h3>State in Objects</h3>
  Stateful objects
  Objects with state have some variable members. Ex: a Bank Account
 <h3>Operational Equivalence</h3>

  After a sequence of testing, and the results are same, there is operational equivalence.
 <h3>Imperative Loops</h3>
  while loops
  <pre>
   <code>
    def power(x: Double, exp: Int): Double = {
      var r = 1.0
      var i = exp
      while (i > 0) { r = r * x; i = i - 1 }
      r
    }
   </code>
  </pre>
  for-loops
   <pre>
    <code>
     for (i <- 1 until 3) { System.out.print(i + " ") }
    </code>
   </pre>

<h2>Classes vs Case Classes</h2>
 creating instances
 class: require the keyword new
 case class: constructor parameters are promoted to members

 <pre>
  <code>
   val aliceAccount = new BankAccount
   val c3 = Note("C", "Quarter", 3)
  </code>
 </pre>

 The same definition of BankAccount(class) create different objects (notion of identity), and the same definition of Note(case class) lead to equal values

 pattern matching does not work on regular classes.

 A case class cannot extend another case class.

 A case class is a special case of a class, with predifined overriting on some properties(parameters are promoted to members;Equality redefinition;Java hashCode redefinition;toString redefinition;Create a copy of a case class;Constructor that allows the omission of the `new` keyword; Extractor for pattern matching).

<h2>Polymorphic Types</h2>
