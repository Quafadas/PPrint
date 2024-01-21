---
title: Getting Started
---

Add the following to your build config:

### SBT
```scala sc:nocompile
libraryDependencies += "com.lihaoyi" %%% "pprint" % "0.7.0"
```

### Mill
```scala sc:nocompile
ivy"com.lihaoyi::pprint::0.7.0"
```

### Scala cli
```scala sc:nocompile
using dep com.lihaoyi::pprint::0.7.0
```

## Example

```scala mdoc
pprint.pprintln(new Object())
```

The above example then showed how to use the default pprint configuration. You can also set up your own custom implicit `pprint.Config` if you want to control e.g. colors, width, or max-height of the output.

The three main methods you need to care about are:

`pprint.pprintln(value: T): Unit` pretty-prints the given value to the console

`pprint.log(value: T, tag="optional") :Unit` pretty-prints the given value to the console along with debugging information (class-name, method-name, line-number, an optional tag) to make it easy to find your prints again later. If you're finding yourself putting many debug prints in different files, this makes it much easier to keep them straight

`pprint.tokenize(value: T): Iterator[String]` same as pprint.pprintln, except instead of dumping to standard output it returns an iterator you can consume or pass around to use at your leisure.

`pprint.apply(value: T): String` same as pprint.pprintln, except instead of dumping to standard output it returns a string.
You can of course define your own custom methods if you want to e.g. always log to a log file or some third-party service, or if you want your own custom set of debug information to be printed (instead of what .log provides). See the short implementation of these methods if you want ideas on how to write your own versions.

Pretty-printing is by default defined for most standard library types, as well as case classes and case objects. For other types not supported, it falls back to using toString

You can configure the pretty-printing by defining your own implicit Config object, to consistently set things like maximum width, height or colors across a codebase.

There are also built in helpers for common use cases. Let's say you're writing documentation and markdown (unlike a console) doesn't show ansi so well.


```scala mdoc
pprint.pprintln(Seq(1, 2, 3))
```


```scala mdoc
pprint.PPrinter.BlackWhite.pprintln(Seq(1, 2, 3))
```

Force wrapping

Wrap
```scala mdoc
pprint.PPrinter.BlackWhite.pprintln(Seq(1, 2, 3), width = 5)
```

Truncate

```scala mdoc
pprint.PPrinter.BlackWhite.pprintln(Seq(1, 2, 3), width = 6, height = 3)
```

PPrint also provides the pprint.log function, which automatically adds some context so you can find your printouts later:

```scala sc:nocompile
scala> class Foo{
     |   def bar(grid: Seq[Seq[Int]]) = {
     |     pprint.log(grid)
     |   }
     | }
defined class Foo

scala> new Foo().bar(Seq(0 until 10, 10 until 20, 20 until 30))
pkg.Foo#bar:13 grid: List(
  Range(0, 1, 2, 3, 4, 5, 6, 7, 8, 9),
  Range(10, 11, 12, 13, 14, 15, 16, 17, 18, 19),
  Range(20, 21, 22, 23, 24, 25, 26, 27, 28, 29)
)

```

Note how the package name, class name, and method name, along with the optional tag. are all formatted nicely for you to read. This should make it much easier for you to find each individual print later. Just like `pprint.pprintln`, the output is nicely formatted across multiple lines and syntax-highlighted for readability.