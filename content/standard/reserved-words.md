---
title: "Reserved Words"
date: 2019-10-27T21:47:07+00:00
severity: must
category: properties
example_apis: []
---

None of the below words may be used as an identifier in our APIs. This encompasses being used as a resource name, a field name or a GET parameter. This is due to reserved keywords in one or more of our target supported languages.

* `__ENCODING__`
* `__LINE__`
* `__FILE__`
* `BEGIN`
* `END`
* `alias`
* `and`
* `begin`
* `break`
* `case`
* `class`
* `def`
* `defined?`
* `do`
* `else`
* `elsif`
* `end`
* `ensure`
* `false`
* `for`
* `if`
* `in`
* `long`
* `module`
* `next`
* `nil`
* `not`
* `or`
* `redo`
* `rescue`
* `retry`
* `return`
* `self`
* `super`
* `then`
* `true`
* `undef`
* `unless`
* `until`
* `when`
* `while`
* `yield`

### Why did we choose this?

To ensure compatibility with our target programming languages

### Related Links

[Ruby Keywords](https://docs.ruby-lang.org/en/2.5.0/keywords_rdoc.html)
