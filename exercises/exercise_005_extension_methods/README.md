# Extension Methods

## Background

Extension methods can be used to add methods to types after they are defined.

Lets say we need to add a method `square` to type `Int`. We used to achieve it 
with the help of `implicit class`es in _Scala 2_

```scala
implicit class RichInt(val i: Int) extends AnyVal {
  def square = i * i
}
```

Now you can use it as follows

```scala
4.square
// res1: Int = 16
```

With dotty `extension methods`, we can rewrite the above as

```scala
def (i: Int).square: Int = i * i

4.square
// val res0: Int = 16
```

More than one extension methods can be wrapped inside an `Extension Instance`,
in order to make them available as methods without needing to be imported explicitly.

```scala
extension {
  def (x: Int).square : Int = x * x
  def (x: Int).isEven: Boolean = x % 2 == 0
}
```

When a series of extension methods need to be defined on the same type,
encoding them one by one quickly becomes tedious. So-called
`Collective Extensions` can group the definitions together.

```scala
extension on (x: Int){
  def square : Int = x * x
  def isEven: Boolean = x % 2 == 0
}
```

> At present, Collective extensions have a limitation: the individual extension 
> methods cannot be generic (i.e. they cannot have additional type parameters).
> This restriction is specific to Scala 3.0 and it will be lifted in a later 
> Scala 3.x release.

## Steps

There are quite a few instances of Extension Methods in this project. A good 
starting point is to take a look at the `TopLevelDefinitions` and `ReductionRules`
which we have created in one of the previous exercises.

- Identify all extension methods defined using the _Scala 2 way_

- Replace them with `Dotty` extension methods

- Wrap one or more occurrences of such method in an `extension instance`

- If you find you need to add more than one extension method to a same type,
  wrap them inside a `collective extension`

- Run the provided tests by executing the `test` command from the `sbt` prompt
  and verify that all tests pass

- Verify that the application runs correctly.

