---
layout: post
title: Use functional style to fill a set instead of a loop
tags: scala, programming
date: 2020-08-12 16:52:00 +0100
---

In scala you should feel encouraged to use a more functional style of programming instead of the imperative paradigm that you might be used to.

So instead of initializing a Set and then filling it, the functional way of doing this is to create values in a functional flow and then assign them once. This way you can use an immutable Set and a `val` instead of a `var` and a mutable type. You want to avoid `var`s and mutable types because they carry state and might not be filled properly.

So instead of this imperative approach where you end up with a var that could be reassigned or changed:

```Java
#create a list of tuples that we are going to work with
val objectList = Array(("0", "a"), ("1", "b"))

#initiate an empty mutable set
var signalList: Set[String] = Set[String]()

for (object <- objectList) {
    signalList += object._1
    signalList += object._2
}
```
... you could write this more functional version with the same functionality:

```Java
#create a list of tuples that we are going to work with
val objectList = Array(("0", "a"), ("1", "b"))

val signalList: Set[String] = objectList.flatMap(obj => Array(obj._1, obj._2))
                                        .toSet
```

---

#### From the [scala docs](https://www.scala-lang.org/api/2.13.3/scala):

**FlatMap**

```
def flatMap[BS, B](f: (T) => BS)(implicit asIterable: (BS) => collection.Iterable[B], m: ClassTag[B]): Array[B]
```

**Implicit:** This member is added by an implicit conversion from Array[T] toArrayOps[T] performed by method genericArrayOps in scala.Predef.

**Definition Classes:** [ArrayOps](https://www.scala-lang.org/api/2.13.3/scala/collection/ArrayOps.html)
