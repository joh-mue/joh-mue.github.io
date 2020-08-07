---
title: scala-first-steps
layout: post
categories: programming, scala
---

# Baby steps

Sometimes even the most basic things are quite hard in a new programming language but so basic that they aren't really explained anywhere.

To start a scala repl and be able to import packages you have imported in build.sbt you can't just start run the plain `scala` command.

I want to play with code in a repl like I would in python, specifically I want to try out the breeze linalg library.

But when running the plain scala repl you get the following error on importing the package:

```
~/code/scala/project $ scala
Welcome to Scala 2.12.6 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_161).
Type in expressions for evaluation. Or try :help.

scala> import breeze.linalg.DenseMatrix
<console>:11: error: not found: value breeze
       import breeze.linalg.DenseMatrix
```

So that's a problem. Instead you should start a repl from sbt which will the include all the imports stated in build.sbt with

```
sbt console
```

Things will look as follows and suddenly work:

```
~/code/scala/project $ sbt console
[warn] No sbt.version set in project/build.properties, base directory: /Users/jomu/Downloads/adtf2parquet-2020-08-06_11_52_36
[info] Loading global plugins from /Users/jomu/.sbt/1.0/plugins
[info] Set current project to adtf2parquet-2020-08-06_11_52_36 (in build file:/Users/jomu/Downloads/adtf2parquet-2020-08-06_11_52_36/)
[info] Updating ...
[info] Done updating.
v[info] Non-compiled module 'compiler-bridge_2.12' for Scala 2.12.6. Compiling...
[info]   Compilation completed in 7.833s.
[info] Starting scala interpreter...
Welcome to Scala 2.12.6 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_161).
Type in expressions for evaluation. Or try :help.


scala> import breeze.linalg.DenseMatrix
import breeze.linalg.DenseMatrix
```
