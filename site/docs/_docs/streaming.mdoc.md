---
title: Streaming
---

PPrint is lazy and streaming. Unlike println(x.toString) which marshals the entire string in memory before returning it:

```scala
val large = Seq.fill(100000)("ABCDE" * 1000)
println(large.toString)
//java.lang.OutOfMemoryError: Java heap space
```

pprint.pprintln streams the result to standard output, meaning that even for enormous data structures like the one above you can immediately start seeing output:

```scala sc:nocompile
pprint.pprintln(large)
Seq(
  "ABCDEABCDEABCDEABCDEABCDEABCDEABCDEABCDEABCDEABCDEABCDEABCDEA
  BCDEABCDEABCDEABCDEABCDEABCDEABCDEABCDEABCDEABCDEABCDEABCDEABC
  ...

```
For example, if you have a massive (or even infinite!) data structure and wish to only show a certain amount of it, truncating it is straightforward:

```scala sc:nocompile
val large = Seq.tabulate(100000)("ABCDE" + _)

pprint.log(large, height=20)

```

If you want to do something else with the streaming output apart from displaying it on the console, you can also call PPrint.tokenize

```scala mdoc
val large = Seq.fill(100000)("ABCDE" * 1000)
pprint.tokenize(large)
large.head
```

This gives you an iterator with which you can do whatever you want: stream it to a file, to your logging system, etc.. Even for extremely large data structures, you can use this data structure to page through it and see what it contains without ever materializing the entire string in memory.

PPrint needs to buffer output in some cases in order to correctly wrap/multiline/truncate output. However, in all cases it should need to buffer at most one line