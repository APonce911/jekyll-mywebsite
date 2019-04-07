---
title: "Packages and Imports - Scala for the impatient"
date: 2019-04-07 18:30:00
lang: en
ref: packages-and-imports-sfti

---
This is my small contribution to Gympass' Scala study group. Scala for the impatient, chapter 7: Packages and Imports.

<h2>Packages and Imports</h2>

  In this chapter the author presents how packages and import statements work in Scala. Key Points are:
  - Packages nest just like inner classes.
  - Package paths are not absolute.
  - A chain x.y.z in a package clause leaves the intermediate packages x and x.y invisible.
  - Package statements without braces at the top of the file extend to the entire file.
  - A package object can hold functions and variables.
  - Import statements can import packages, classes, and objects.
  - Import statements can be anywhere.
  - Import statements can rename and hide members.
  - java.lang, scala, and Predef are always imported.

<h3>Packages</h3>

  To add items to a package, you can include them in package statements, such as:
  <pre>
    <code>
      package com {
        package horstmann {
          package impatient {
            class Employee
            ...
          }
        }
      }
    </code></pre>

  Then the class name Employee can be accessed anywhere as com.horstmann.impatient.
  Employee.

  Unlike Classes or objects definitions, packages can be defined in multiple files.Ex Manager class on package com.horstmann.impatient.manager

  OBS: there is no enforced relationship between the source file and the package. employee.scala doesn't have to be on com/horstmann/impatient directory.

  You can contribute to more then on package in a single file.

<h3>Scope Rules</h3>

  Everything defined inside the parent package can be used without the full package referente. Ex:

  <pre>
    <code>
      package com {
        package horstmann {
          object Utils {
            def percentOf(value: Double, rate: Double) = value * rate / 100
            ...
          }
          package impatient {
            class Employee {
              ...
              def giveRaise(rate: scala.Double) {
                salary += Utils.percentOf(salary, rate)
              }
            }
          }
        }
      }
  </code></pre>

  We can use Utils.percentOf instead com com.horstmann.Utils.percentOf because its used inside the parent scope.

  If a package is defined with a conflicting name (Ex: collection vs scala.collection), one solution is to use absolute package names. Another approach is to use chained package clauses.

<h3>Chained Package Clauses</h3>
  <pre>
    <code>
      package com {
        package horstmann {
          package collection {
          ...
          }
        }
      }
  </code></pre>

Instead of using the above example, we can use the following way, so com.horstmann.collection package would no longer be accessible as collection:

  <pre>
    <code>
      package com.horstmann.collection {
      // Members of com and com.horstmann are not visible here
        }
      }
    </code></pre>

<h3>Top-of-File Notation</h3>

Insead of the nested notations presented until now, we can use a cleaned notation without braces:

<pre>
  <code>
    package com.horstmann.impatient
    package people
    class Person
    ...
  </code></pre>

is equivalent to:

<pre>
  <code>
    package com.horstmann.impatient {
      package people {
        class Person
        ...
        // Until the end of the file
      }
    }
  </code></pre>

<h3>Package Objects</h3>


<h3>Package Visibility</h3>
<h3>Imports</h3>
<h3>Imports Can Be Anywhere</h3>
<h3>Renaming and Hiding Members</h3>
<h3>Implicit Imports</h3>
