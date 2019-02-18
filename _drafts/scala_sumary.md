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
 <h3></h3>
