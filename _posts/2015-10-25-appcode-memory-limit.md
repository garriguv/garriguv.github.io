---
layout: post
title: AppCode memory limit
---

I love AppCode, but sometimes it can get excruciatingly slow when working on large projects. A good thing to check in those cases is the memory usage. Here's how to access it:

![]({{ site.url }}/assets/images/appcode-memory.png)

You'll now have a little memory indicator in the bottom right toolbar of the IDE. If you see that the memory fills up instantly when opening your project, then maybe it's time to increase it.

AppCode runs on the JVM, and you can change the JVM parameters. First, copy the default launch options to AppCode's preferences directory:

```
$ cp /Applications/AppCode.app/Contents/bin/appcode.vmoptions ~/Library/Preferences/AppCode33
```

Then edit the copied `appcode.vmoptions` file. You should change both the `-Xmx` (memory limit) and `-Xms` (initial memory allocation) options.

This set of values has been working pretty well so far:

{% gist garriguv/c769aa160fc219269ed2 %}

You don't necessarily have to go up to 4 GB of memory limit. But since the new MacBook Pro ships with 16 GB of memory, why not use some of it?
