Scala Tips
==========

This is the repository for top tips for writing more awesome Scala by the Singapore Scala Programmers. Check us out at http://www.meetup.com/Singapore-Scala-Programmers.

Tips
----

If you initialise `Option` with `null` you get a `None`. This is really useful to wrap up existing java apis that insist on returning null. For example:

```scala
val maybeResult : Option[String]  = Option(naughtyNullReturningApi.doStuff())
maybeResult.map{
    s => ??? //now the api result can be used safely
}
```

