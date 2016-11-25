---
title: brew sends your usage data to google analytics
layout: post
tags: 
---

Through a [hackernews post](https://news.ycombinator.com/item?id=13034936) I learned that homebrew is sending anonymized usage data to google analytics. I don't want to get into the discussion whetere that is good or not. homebrew gives the following [reasoning](https://github.com/Homebrew/brew/blob/master/docs/Analytics.md#why):

```
Homebrew is provided free of charge and run entirely by volunteers in their spare time. As a result, we do not have the resources to do detailed user studies of Homebrew users to decide on how best to design future features and prioritise current work.
```

which makes sense. If you don't agree with their policy you should probably support them either through a donation or other contributions.

To opt-out of usage data being sent you can set this variable in your environment:

```
export HOMEBREW_NO_ANALYTICS=1
```

Alternatively, this will prevent analytics from ever being sent:

```
brew analytics off
```
[opting-out](https://github.com/Homebrew/brew/blob/master/docs/Analytics.md#opting-out)


[original post](https://tobiastom.name/notes/7a79eed0)
