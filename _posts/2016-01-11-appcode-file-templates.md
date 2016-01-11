---
layout: post
title: Making the most of AppCode's file templates.
description: Use the Velocity templating engine to take your file templates to the next level.
---

AppCode's File and Code templates are generated using [Velocity](http://velocity.apache.org/engine/index.html), a Java-based template engine. Taking a few minutes to tweak the existing templates orr create new ones can end up saving you a ton of time down the line.

What's a template engine?

> A template processor (also known as a template engine or template parser) is software designed to combine one or more templates with a data model to produce one or more result documents. ([Template processor](https://en.wikipedia.org/wiki/Template_processor))

You can find the existing templates in *Preferences* > *Editor* > *File and Code templates*. The data model is a set of predefined [template variables](https://www.jetbrains.com/idea/help/file-template-variables.html):

* `${PROJECT_NAME}` - the name of the current project.
* `${NAME}` - the name of the new file which you specify in the New File dialog box during the file creation.
* `${USER}` - the login name of the current user.
* `${DATE}` - the current system date.
* `${TIME}` - the current system time.
* `${YEAR}` - the current year.
* `${MONTH}` - the current month.
* `${DAY}` - the current day of the month.
* `${HOUR}` - the current hour.
* `${MINUTE}` - the current minute.
* `${PRODUCT_NAME}` - the name of the IDE in which the file will be created.
* `${MONTH_NAME_SHORT}` - the first 3 letters of the month name. Example: Jan, Feb, etc.
* `${MONTH_NAME_FULL}` - full name of a month. Example: January, February, etc.

You can also add your own variables. They'll be added to the file creation prompt:

![New file prompt]({{ site.url }}/assets/images/appcode-file-template.png)

Combining the template with the data model is actually very easy. A good example I came across is the creation of test files. Let's say you want to write tests for `MyClass`, you need to create a `MyClassSpec.h` file. A good starting point for that file could be the following:

{% gist garriguv/ede7618af6a2dcd57901 %}

The problem is that it's not possible to generate this file using only the predefined template variables, because `${NAME}` will equal `MyClassSpecs` and not `MyClass`. You can either add another variable or use Velocity to get the desired result. We'll look into the latter.

It's possible to execute Java code in velocity templates, which means that we can use Java's [String](http://docs.oracle.com/javase/8/docs/api/index.html?java/lang/String.html) methods to manipulate the file name and extract the base class' name:

{% gist garriguv/03c61706a745f6f68cb4 %}

In the end, this is what the Spec template looks like:

{% gist garriguv/973112a964eed09ba2e1 %}

That's it!

I've setup a quick project to experiment with [Velocity] templates, you'll find it here: [https://github.com/garriguv/velocity](https://github.com/garriguv/velocity)
