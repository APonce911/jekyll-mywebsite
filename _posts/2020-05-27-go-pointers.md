---
title: "Go Pointers"
date: 2020-05-27
lang: en
ref: go-pointers

---

A pointer holds the memory address of a value. Used to reference and indirectly affect value.

Use '&' to set the memory address of a pointer, and the '*' operator to access (read or write) the value of a memory address through a pointer.

Ex: p is a pointer, n is not 

  <pre>
   <code>
    func main() {
      i, j := 42, 15
      var n int
      
      p := &i         // point to i
      fmt.Println(*p) // read i through the pointer
      *p = 21         // set i through the pointer
      fmt.Println(i)  // see the new value of i

      n = j    
      n = n / 5   
      fmt.Println(j)
      fmt.Println(n)
    }
    // $ 42
    // $ 21
    // $ 15
    // $ 3
   </code></pre>

OBS: Is possible to read the memory address of a value using the & operator.

  <pre>
   <code>
    func main() {
      luckyNumber := 7

      fmt.Println(&luckyNumber)
    }
    // $ 0xc00002c008
   </code></pre>

<h2>Method Receiver</h2>

Methods vs Functions

In OOP a method is a function on an instance of an object. In go, we can declare methods on structs.

The method receiver is the type/struct that will be able to receive a specific method call. It is declared between de func keyword and the function name.

Example

  <pre>
   <code>
    type User struct {
      FirstName, LastName string
    }

    func main() {
      u := User{"Roberto", "Barros"}

      fmt.Println(u.Greeting())
    }

    func (u User) Greeting() string {
      return fmt.Sprintf("Dear %s %s", u.FirstName, u.LastName)
    }

    // $ Dear Roberto Barros
   </code></pre>

<h2>Pointer Receiver</h2>
  
  Methods can be declared on a value type(User), or on a pointer to a value type(*User).
  
  As Go passes everything by value, if you declare the method on a value(as the above exemple), the struct will be copyed on every method call(Greeting).
  
  If you declare a method on a pointer, only the pointer will be copyed on the method call, which is cheap.

  <pre>
   <code>
    ...

    func main() {
      u := &User{"Roberto", "Barros"}

      fmt.Println(u.Greeting())
    }

    func (u *User) Greeting() string {
      return fmt.Sprintf("Dear %s %s", u.FirstName, u.LastName)
    }

    // $ Dear Roberto Barros
   </code></pre>
  
  Another reason to assign a method to a pointer, is that the method can then modify the value that its receiver points to.
  
  <pre>
   <code>
    ...

    func main() {
      u := &User{"Roberto", "Barros"}
      u.updateFirstName("Carlos")

      fmt.Println(u.FirstName)
    }

    func (u *User) updateFirstName(newFirstName string) {
      u.FirstName = newFirstName
    }

    // $ Carlos
   </code></pre>

OBS: Functions with pointers receivers(*User) can be called on a value of the same type(User). This is a Go shortcut.

<h2>Source</h2>

https://tour.golang.org/moretypes/1
http://www.golangbootcamp.com/book/methods
