This is my small scala sumary. Syntax comparisons will be made mainly against ruby and javascript.

Terms & types
 Primitives
 Operators
 Method Calls
 Operators are methods
Definitions & Evaluations
 Val(Constants) & Def(Variables)
 Methods
 Evaluation
Functional Loops
 Conditional
 Boolean expressions
<h1>Lexical Scopes</h1>
<h2>Nested Functions</h2>
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
