---

# A tour of Scala
## beyond others

---

# Disclaimer

## This is possibly wrong

This what I understand as far as now.
I may misunderstood scala since the beginning.

---

# Based on a true story

![](https://images-na.ssl-images-amazon.com/images/I/51y4d3qeABL._SX377_BO1,204,203,200_.jpg)

---

# Types

Scala is a **statically-typed** language.

Everything is typed, so you always know **at compile time** what you can do with anything.


---

# `val` and `var`

* `val` are **immutable**. You cannot change it.
* `var` are **mutable**. Yes, you can change it. Always ask you why you need a mutable structure in functional programming.

The use cases of usage of **mutable** structure in Scala are generally for **optimization** concerns (`ArrayBuffer` and so on...)

---

# Functions

Functions are the base of Scala. That's why it's called **functional programming**

```scala
def f(s: String) = "f(" + s + ")"
def g(s: String) = "g(" + s + ")"

val fComposeG = f _ compose g _ // f(g(x))
val fAndThenG = f _ andThen g _ // g(f(x))
```

Think first in **composing functions**, then in **multiple inheritance**.

---

# Functions

* Local functions

```scala
def foo = {
  def bar = ... // local function
  def baz = ... // local function
}
```

* First-class functions

**function literal** represented by objects, as function values.

```scala
val firstClassFunc = (x: Int) => x + 1
```

---

# Functions

* Repeated parameters

```scala
def echo(args: String*) =
  for(arg <- args) println(arg)

// to call it with an Array
val arr = ["foo", "bar"]
echo(arr: _*)
```

---

# Currying

```scala
def funcA(param1)(param2)(param3): AnyVal = ...

def funcB = funcA(myParam1)(myParam2)
```

This enable to create **new functions**

When called like in `funcB`, it is called **partially applied functions**

---

# Implicit Conversions

No need to use everywhere dumb `toBidule` to convert a `Machin` in `Bidule`

```scala
implicit def MachinToBidule(a: Machin) = new Bidule(a)
```

* Marking rule: only `implicit` are available
* Scope rule: must be in the scope
* One-at-a-time: only one `implicit` is inserted
* Explicits-first rule
* Arbitrary naming

---

# Implicit Classes

You can define `implicit` classes for lighter syntax.

```scala
val myRectangle = 3 x 4
```

---

# Implicit Parameters

Currying and implicit conversions are combined to create `implicit` parameters

```scala
def greet(name: String)(implicit prompt: Prompt) = println(s"${prompt.pref} Hello, ${name}")
```

---

# Partial Functions

It's basically a `case`, and generally refers to

```scala
def myPartialFunction: PartialFunction[A, B] = {
  case val1: A => new B(val1)
  case val2: A => ...
}
```

---

# Class

`class` modifier allows you to define classes.

```scala
class Number(n: Int)

new Number(3)
```

* Companion Object

Singleton allowing you to create shorthand

```scala
object Number {
  def apply(n: Int) = new Number(n)
}
```

* `sealed class`

A class which cannot have any subclasses except ones in the same file.

---

# `case class`

## Why `case` ?

---

# `case class`

class you can `case` on it

```scala
case class MyClass(name: String)
```

* add a factory method to create references without `new` modifier
* all parameters get a `val` and are fields
* natural implementations of `toString`, `hashCode`, `equals`

---

# Pattern matching

`match` is the scala `switch` version with powerful features

* Wilcard patterns : `case _ =>`
* Constant patterns: `case 5 => `
* Variable patterns: `case myVariable => `

---

# Pattern matching

* Constructor patterns: `case Number(x) => `
* Tuple/Sequence patterns: `case List(0, _, _) =>`
* Typed Pattern: `case n: Number =>`
* Pattern guards: `case Number(x) if x.n == 0 =>`
* Pattern overlaps: patterns are tried in order

---

# Try or try/catch ?

Basic `try/catch` works locally.

```scala
try {
  // Function
} catch {
  // Partial Function
  case e1: Exception1 => ...
  case e2: Exception2 => ...
} finally {
  // Function
}
```

The `Try` is a better way to expose tryable functions.

---

# For comprehensions

* a shorthand and more comprehensive way to write functional expression
* uses `map`, `flatMap`, `foreach`, `withFilter`

```scala
for {
  p <- params            // generator
  n = p.nam              // defintion
  if (n.startsWith "To") // filter
}
```

---

# For comprehensions

You can create `for` comprehensions by extending this abstract

```scala
abstract class C[A] {
  def map[B](f: A => B): C[B]
  def flatMap[B](f: A => C[B]): C[B]
  def withFilter(p: A => Boolean): C[A]
  def foreach(b: A => Unit): Unit
}
```

---

# Type parametrization

Allows you to create **generic** structure

```scala
class List[T] = { ... }
```

* Covariance `[+T]`, Contravariance `[-T]`, and NonVariance `[T]` helps you (and type checker) to check types deeply in the code.
* Bounds `[T :< SuperType]` allows you to reduce bounds of a generic type

---

# Futures

Simple way to thread an expression

```scala
def futureString(s: String): Future[String] = Future { s }
```

* Example of implementation of `for` comprehensions

---

# More things to look for

* Placeholder syntax `(_ > 0)`
* Covariance, Contravariance, Non-variance
* Tail recursions
* Akka and streams
* Advanced pattern matching and extractors
* Detailing List, Collection, and mutable strucutre

---

# Tools

* `amm`: a definitive useful tool

```bash
$ amm
Loading...
Welcome to the Ammonite Repl 0.7.6
@ println("this a sandbox")
this a sandbox
```

---

# Tools

* using `scala` as scripting language

```scala
#!/bin/sh
exec scala "$0" "$@"
!#
println(s"Hello ${args(0)} !")
```

---

# Tips

* Always try to introspect types and methods (remember all is method)

---

# References

* [Programming in Scala by Martin Odersky](https://www.amazon.com/Programming-Scala-Updated-2-12/dp/0981531687)
* [Scala school by twitter](https://twitter.github.io/scala_school/)
* [Official Scala lang](http://www.scala-lang.org/documentation/)

---

# Thanks

## [github.com/alexduros/tour-of-scala](https://github.com/alexduros/tour-of-scala)