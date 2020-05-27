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
   
