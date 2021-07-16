---
title: "Rails do's & don'ts"
date: 2021-07-16
lang: en
ref: rails_dos_and_donts

---

Criteria: SOLID Principles, clean code.

Don'ts

(what?why?what SOLID principle it violate?)

  - [Active Record Nested Attributes](https://api.rubyonrails.org/classes/ActiveRecord/NestedAttributes/ClassMethods.html) to create entities.
  - attr_accessors to alter an associated entity attributes(chaining).
  - Excessive use of instance variables.

Do's

(the alternatives)