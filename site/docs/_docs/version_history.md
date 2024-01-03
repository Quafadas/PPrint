---
title: Version History
---

## 0.7.3

Add support for Polytypes [79](https://github.com/com-lihaoyi/PPrint/pull/79)

## 0.7.2
Support Scala Native on Scala 3
[75](https://github.com/com-lihaoyi/PPrint/pull/77)

## 0.7.1
Fixes for pprinting and tprinting literal constants [75](https://github.com/com-lihaoyi/PPrint/pull/75)
## 0.7.0
Overhaul and simplify TPrint implementation [72](https://github.com/com-lihaoyi/PPrint/pull/72)

Fix PPrint for Product2 [36](https://github.com/com-lihaoyi/PPrint/pull/36)

Make PPrint robust against `toString` returning `null` [70](https://github.com/com-lihaoyi/PPrint/pull/70)

Add flag to control unicode escaping [71](https://github.com/com-lihaoyi/PPrint/pull/71)
## 0.6.0
Add support for field names when printing case classes in Scala 2.13

## 0.5.6
Make `pprint.log` use `sourcecode.FileName` instead of `sourcecode.Enclosing`
to reduce verbosity of logging
## 0.5.5
Support for Scala 2.13.0 final

## 0.5.3
Support for Scala-Native
## 0.5.2
Fix crash when pretty-printing `new java.io.ByteArrayOutputStream()`
## 0.5.1
Performance improvements that speed up my benchmarks by 30-50%

## 0.5.0
Ground-up rewrite to use manual pretty-printer registration instead
of implicit derivation. `pprint.log` and `pprint.tokenize`
still exist, but most of the internals have been totally rewritten.


@sect.ref{Customization} of things like the default width/height of
the output, colors, or adding special support for additional classes,
is now done in instantiating new `PPrinter` objects rather than
by passing around implicits. This should be much more intuitive and
harder to get wrong


Line-wrapping should be much more strict about following the desired
width and height. There are likely still bugs in it, but it should be
better than before.


Line-wrapping in general should be more predictable, especially in the
presence of infix operators like `->` or `::`


Performance should be far better than in previous versions; my ad-hoc
benchmarks show a ~200-220x (~20,000-22,000%) speedup over the previous
version. With all the lazy/iterator/formatting overhead, it's still ~50x
slower than `.toString`, but that sure beats being 10,000x slower!


If you've enjoyed using PPrint or any of my other libraries, please
consider [chipping in](https://www.patreon.com/lihaoyi) to support
their ongoing development on [Patreon](https://www.patreon.com/lihaoyi)!
Any amount helps ensure we can continue improving these libraries going forward.


## 0.4.3
Add `pprint.stringify` function, thanks to
[David Portabella](https://github.com/dportabella)

## 0.4.2
Bump fansi version
## 0.4.1
Updating PPrint to use the [Fansi](https://github.com/lihaoyi/fansi) library for dealing with colors, instead of `Console.*`
## 0.4.0
Added [TPrint](tprint.mdoc.md) implicit, which can be materialized for any type to get a nicely-formatted, colored version of the type `T}s normal `toString


## 0.3.9
Tweaks to `pprint.log` to make it less verbose, added `pprint.log2` with the old behavior and verbosity.
## 0.3.8
Robustify PPrint macros slightly against crashes Ammonte #198, href:="https://github.com/lihaoyi/Ammonite/issues/198 and doobie ## 258 https://github.com/tpolecat/doobie/issues/258


Added the `pprint.log` function, for convenient no-setup console logging and debugging

## 0.3.7
Case-classes providing custom `.toString` methods now use those instead of the macro-generated pretty-printer (#115)

`pprint.tokenize} now takes the default `Config` by default, thus removing the need for a special import, just like `pprint.pprint1` does

Slightly improve hygiene of uPickle/PPrint macro expansion

## 0.3.6

Fix more bugs in PPrint derivation

## 0.3.5

Fix some bugs in PPrint derivation

## 0.3.4

Remove unnecessary shapeless dependency

## 0.3.3

Fix more edge cases to avoid diverging implicits

## 0.3.2
Fix compiler crash on pretty-printing `akka.http.Http.ServerBinding`

Made pretty-print work for inferred type `Nothing`
## 0.3.1

Fixed edge cases around typeclass derivation

## 0.3.0
First release outside of the Ammonite project where this lived for a long time

Shared case-class implicit-derivation back-end with uPickle, greatly expanding the scope of things that can be prettyprinted