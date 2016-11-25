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

![](file:///Users/aduros/scala_book.png)

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

# Partial Functions

It's basically a `case`, and generally refers to

```scala
def myPartialFunction: PartialFunction[A, B] = {
  case val1: A => new B(val1)
  case val2: A => ...
}
```

---

# Pattern matching


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

* use `withFilter` instead of filter

---

# Class

* `sealed class`

A class which cannot have any subclasses except ones in the same file.


---

# `case class`

## Why `case` ?


---

# `case class`

---

# Covariance, Contravariance, Non-variance


---

# Extractors


---

# Futures and concurrency

---

# More things to look for

* Placeholder syntax `(_ > 0)`
* Tail recursions
* Akka and streams


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