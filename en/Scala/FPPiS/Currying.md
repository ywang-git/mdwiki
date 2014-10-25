**First Form of `sum` Function**
```scala
def sum(f: Int => Int, a: Int, b: Int): Int = 
  if (a > b) 0
  else f(a) + sum(f, a + 1, b)
```

**Using Accumulator to Convert Function as Tail-Recursive**
```scala
def sum(f: Int => Int, a: Int, b: Int): Int = {
  def loop(a: Int, acc: Int): Int = {
    if (a > b) acc
    else loop(a + 1, acc + f(a))
  }
  loop(a, 0)
}
```

**Rewrite of `sum` (Function returning another function)**

```scala
def sum(f: Int => Int)(a: Int, b: Int): (Int, Int) => Int = {
  def sumF(a: Int, b: Int): Int = 
    if (a > b) 0
    else f(a) + sumF(a + 1, b)
  sumF
}
```

**With Syntax Sugar (w/ Anonymous Function)**
```scala
def sum(f: Int => Int)(a: Int, b: Int): Int = 
  if (a > b) 0 else f(a) + sum(f)(a + b)
```

