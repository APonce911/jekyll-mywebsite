---
title: "Go Pointers"
date: 2020-05-27
lang: en
ref: go-pointers

---

A pointer holds the memory address of a value. They are used to reference of indirect affect a value.

Use '&' to set a the value of a pointer, and * to access (read or write) through a pointer

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

    func (u User) Greeting() string {
      return fmt.Sprintf("Dear %s %s", u.FirstName, u.LastName)
    }

    func GreetUser() {
      u := User{"Matt", "Aimonetti"}
      fmt.Println(u.Greeting())
    }
   </code></pre>

<h2>Pointer Receiver</h2>
  
  Methods can be declared on a value type, or on a pointer to a value type.
  
  As Go passes everything by value, if you declare the method on a value(as the above exemple), the struct will be copyed on every method call(Greeting)
  
  If you declare a method on a pointer, only the pointer will be copyed on the method call, which is cheap.
  <pre>
   <code>
    ...
    func (u *User) Greeting() string {
      return fmt.Sprintf("Dear %s %s", u.FirstName, u.LastName)
    }

    func GreetUser() {
      u := &User{"Matt", "Aimonetti"}
    }
   </code></pre>
  
  Another reason to assign a method to a pointer, is that the method can then modify the value that its receiver points to.
  
<h2>Source</h2>

https://tour.golang.org/moretypes/1
http://www.golangbootcamp.com/book/methods#:~:text=A%20method%20is%20a%20function,Go%20does%20not%20have%20classes.&text=The%20method%20receiver%20appears%20in,keyword%20and%20the%20method%20name.
