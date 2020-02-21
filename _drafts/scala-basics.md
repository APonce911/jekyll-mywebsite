

<h3>Expressions vs Statements</h3>

Expressions: What code is when evaluated. Returns a value.

Statements: represent an action or command to be executed. (What code does)

<h3>Functions definitions</h3>

def aRepeatedFunction(aString: String,n: Int): String ={
  ...
}

aRepeatedFunction function name, and returns a String
Takes 2 parameters, aString (type String) and n (type Int)

When a function last execution is a statement, it returns Unit, and it is considered a side effect.
Side effects are not desirable in functional programming, because they are imperative programming.

When you need loops, use recursion

<h3>Recursion</h3>

Stack Frame store in memory the operations needed to execute an evaluation 
Call Frame is the execution of the operation of the Stack Frame

The memory used to store the stack frame is limited
Stack overflow error. Occours when the recursive depth is too big, and our application reaches the memory limit.

To avoid using aditional stack frame, use tail recursive functions.
Use the recursive call as the last expression. To achieve that, store the intermediate results on an accumulator.

Use as many accumulators as the number of recursive calls you need. 
For example: Use two accumulators for fibonacci. One for n-1 and another for n-2.

to verify if the fuction is tail recursive use the following line above your function definition:
@tailrec


