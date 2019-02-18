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
