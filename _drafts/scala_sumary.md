This is my small scala sumary. Syntax comparisons will be made mainly against ruby and javascript.
Used the content of the following page https://www.scala-exercises.org/scala_tutorial
<h2>Terms & types</h2>
 <h3></h3>Primitives
 <h3></h3>Operators
 <h3></h3>Method Calls
 <h3></h3>Operators are methods

<h2>Definitions & Evaluations</h2>
 <h3></h3>Val(Constants) & Def(Variables)
 <h3></h3>Methods
 <h3></h3>Evaluation

<h2>Functional Loops</h2>
 <h3></h3>Conditional
 <h3></h3>Boolean expressions

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
