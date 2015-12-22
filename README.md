#Scala Tips

This is the repository for top tips for writing more awesome Scala by the Singapore Scala Programmers. Check us out at http://www.meetup.com/Singapore-Scala-Programmers.

##Tips

###Use option to wrap up anything that could possibly return null.

If you initialise `Option` with `null` you get a `None`. This is really useful to wrap up existing java apis that insist on returning null. For example:

```scala
val maybeResult : Option[String]  = Option(naughtyNullReturningApi.doStuff())
maybeResult.map{
    s => ??? //now the api result can be used safely
}
```

###Use breakout to avoid creating new collections twice

If you perform a `map` on a specific type of collection, the output collection type is the same as the input, e.g.

```scala
val output = Seq(1, 2, 3).map(_ + 1)

output.toString() // Returns Seq(2, 3, 4)
```

If you want the resulting collection type to be different, you would usually use the `.toXXXX` function, e.g.

```scala
val list = Seq(1, 2, 3).map(_ + 1).toList

list.toString() // Returns List(2, 3, 4)
```

However, this is inefficient as Scala creates a new Seq, then copies it into a new List. To avoid this overhead, use `breakout` to tell Scala to build the desired collection type, not the input collection type, i.e.

```scala
val list: List[Int] = Seq(1, 2, 3).map(_ + 1)(collection.breakOut)

list.toString() // Returns List(2, 3, 4)
```
