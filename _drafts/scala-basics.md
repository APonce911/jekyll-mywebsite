

<h3>Expressions vs Statements</h3>
Expressions: What code is when evaluated. Returns a value.

Statements: represent an action or command to be executed. (What code does)

Functions definitions
def aRepeatedFunction(aString: String,n: Int): String ={
  ...
}
aRepeatedFunction function name, and returns a String
Takes 2 parameters, aString (type String) and n (type Int)

When a function last execution is a statement, it returns Unit, and it is considered a side effect.
Side effects are not desirable in functional programming, because they are imperative programming.


When you need loops, use recursion
@tailrec

