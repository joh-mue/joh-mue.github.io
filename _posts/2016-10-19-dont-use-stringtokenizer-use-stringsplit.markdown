---
title: Don't use StringTokenizer
layout: post
tags: programming, java
---

So here is something I did not know yet.

When I needed a String to be split into tokens - tokenized so to say - I would use a StringTokenizer. Obviously. But apparently that's not the way you do it and it hasn't been for a long time.

When you check the [java-docs]([https://docs.oracle.com/javase/7/docs/api/java/util/StringTokenizer.html]) you find this little note:

```StringTokenizer is a legacy class that is retained for compatibility reasons although its use is discouraged in new code. It is recommended that anyone seeking this functionality use the split method of String or the java.util.regex package instead.```

Fair enough. The split mehtod of String. How could that be better?

Well, instead of the usual

```
String string = "This:is:a:string";
StringTokenizer tokenizer = new StringTokenizer(string, ":")
ArrayList<String> tokens = new ArrayList<>();
while (tokenizer.hasMoreTokens()) {
  tokens.add(tokenizer.nextToken());
}
```

you could just write

```
String string = "This:is:a:string";
String[] tokens = string.split(":");
```

done*.



*Unless you don't want a String[] but something more practical instead like a List. But even then you just need to

```
String string = "This:is:a:string";
List<String> tokens = Arrays.asList(string.split(":"));
```
