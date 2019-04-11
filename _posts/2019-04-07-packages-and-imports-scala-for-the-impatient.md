---
title: "Packages and Imports - Scala for the impatient"
date: 2019-04-07 18:30:00
lang: en
ref: packages-and-imports-sfti

---
This is my small contribution to Gympass' Scala study group. Scala for the impatient, chapter 7: Packages and Imports.

<h2>Packages and Imports</h2>
  Packages are used to reference specific classes, objects, traits, etc.
  Imports are used to access packages from other files.
  In this chapter, the author presents how packages and import statements work in Scala. Key Points are:
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

  To add items to a package, we can include them in package statements, such as:
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

  Unlike Classes or objects definitions, packages can be defined in multiple files.(Ex: Manager class on package com.horstmann.impatient.manager)

  OBS: there is no enforced relationship between the source file and the package. employee.scala doesn't have to be on com/horstmann/impatient directory.

  we can contribute to more than one package in a single file.

<h3>Scope Rules</h3>

  Everything defined inside the parent package can be used without the full package reference. Ex:

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

  We can use Utils.percentOf instead of com com.horstmann.Utils.percentOf because it is used inside the parent scope.

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

  Instead of using the above example, we can use the following way, so com.horstmann.collection package would no longer be accessible as 'collection':

  <pre>
    <code>
      package com.horstmann.collection {
      // Members of com and com.horstmann are not visible here
        }
      }
    </code></pre>

<h3>Top-of-File Notation</h3>

  Instead of the nested notations presented until now, we can use a cleaned notation without braces:

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

  Packages can contain classes objects and traits, but not functions or variables. To address this issue we can use package objects.

  Every package can have its package object, and it should be defined inside the parent.

  <pre>
    <code>
      package com.horstmann.impatient
        package object people {
          val defaultName = "John Q. Public"
        }
        package people {
          class Person {
            var name = defaultName // A constant from the package
        }
        ...
      }
    </code></pre>

<h3>Package Visibility</h3>

  We can use qualifiers to explicit the visibility of a method.

  <pre>
    <code>
      package com.horstmann.impatient.people
      class Person {
        private[people] def description = "A person with name " + name
        ...
      }
    </code></pre>

  We can extend the visibility to an enclosing package:

  <pre>
    <code>
      private[impatient] def description = "A person with name " + name
    </code></pre>

<h3>Imports</h3>

  If we import packages, we can use shorter names instead of longer ones by bringing them into scope. (Ex: Color instead of java.awt.Color after importing it)

  To import all members of a package use the wildcard ._ (Ex: import java.awt._)

<h3>Imports Can Be Anywhere</h3>

  Imports can be anywhere inside a Scala file, not only on top. The scope extends until the end of the enclosing block.

  It is helpful to reduce potential namespace conflicts. It also makes our code more clear and organized. Ex:

  <pre>
    <code>
      package foo

      // available to all classes defined below
      import java.io.File
      import java.io.PrintWriter

      class Foo {
          // only available inside this class
          import javax.swing.JFrame
          // ...
      }

      class Bar {
          // only available inside this class
          import scala.util.Random
          // ...
      }
    </code></pre>

  However, import statements are read in the order of the file, so de code below won't compile:

  <pre>
    <code>
      // this doesn't work because the import is after the attempted reference
      class ImportTests {
          def printRandom {
              val r = new Random   // fails
          }
      }

      import scala.util.Random
    </code></pre>

<h3>Renaming and Hiding Members</h3>
  To import a few members from a package, we  can use a selector:

  <pre>
    <code>
      import java.awt.{Color, Font}
    </code></pre>

  On selectors, we can rename members using =>
  <pre>
    <code>
      import java.util.{HashMap => JavaHashMap}
    </code></pre>

<h3>Implicit Imports</h3>

  Every Scala program starts with:

  <pre>
    <code>
      import java.lang._
      import scala._
      import Predef._
    </code></pre>

  OBS: some scala package members override the java correspondents. (Ex: StringBuilder)
