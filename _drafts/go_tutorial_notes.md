---
title: "Go tutorial notes"
date: 2020-05-25
lang: en
ref: go-tutorial-notes

---

Packages

Imports

Exported names

When importing a package, you can only access exported names. Those are the names starting with a capital letter.

Functions

func add(x int, y int) int{
  return x + y
}
  <pre>
   <code>
    func add(x int, y int) int{
      return x + y
    }
   </code></pre>

  you can ommit the time when parameters share a type
  
  <pre>
   <code>
      x, y int
   </code></pre>
  
  a function can return multiple results
  
  <pre>
   <code>
      func swap(x, y string) (string, string) {
        return x, y
      }
   </code></pre>
  
  It can also return named values, if they are defined as variables at the function signature

  <pre>
   <code>
    func split(sum int) (x, y int) {
      x = sum * 4 / 9
      y = sum - x
      return
    }
   </code></pre>
  
Variables

  The var statement declares a list of variables, and the Type is last.
  
  <pre>
    <code>
    var i int
  </code></pre>
  
  A var can take initializers, and in this case the Type can be omitted.
  
  <pre>
    <code>
    var c, python, java = true, false, "no!"
    fmt.Println(reflect.TypeOf(c) ,reflect.TypeOf(java))
    // bool string
  </code></pre>

  
Inside a function, the var assignment can be substituted by :=  (short assignment statement)

  <pre>
    <code>
    c, python, java := true, false, "no!"
  </code></pre>

Variables declared without an value are given their zero value. 

0 for numeric types,
false for the boolean type, and
"" (the empty string) for strings.

Type Conversions

T(v) converts the value v to the type T

ex

  <pre>
    <code>
    var i int = 42
    var f float64 = float64(i)
    var u uint = uint(f)
  </code></pre>

Type Inference

dependiong on the value bbeing declared, a var can have its type inferred according to the value precision

Ex:

<pre>
  <code>
  i := 42           // int
  f := 3.142        // float64
  g := 0.867 + 0.5i // complex128
</code></pre>

Constants

can be defined as variables but with the keyword const. (not using :=)

Numeric Constants are high-precision values 
