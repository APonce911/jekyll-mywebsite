---
title: "Go by example notes"
date: 2020-05-26
lang: en
ref: go-by-example-notes

---

This draft is made after go tutorial notes, so some topics were already covered(ex: values,variables,consts,etc.)

Values

Go has various value types including strings, integers, floats, booleans, etc.

Constant

A numeric constant has no tyoe until it's given one, such as an explicit conversion

For is the only looping construct

Single condition

  <pre>
   <code>
    i := 1
    for i <= 3 {
        fmt.Println(i)
        i = i + 1
    }
   </code></pre>

Classical Initial/ Condition/ After loop

  <pre>
   <code>
    for j := 7; j <= 9; j++ {
        fmt.Println(j)
    }
   </code></pre>

For without condition. Run until 'break'

  <pre>
   <code>
    for {
        fmt.Println("loop")
        break
    }
   </code></pre>

Skip the current iteration with 'continue'

  <pre>
   <code>
    for n := 0; n <= 5; n++ {
        if n%2 == 0 {
            continue
        }
        fmt.Println(n)
    }
  }
  </code></pre>
