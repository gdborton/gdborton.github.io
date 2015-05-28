---
layout:     post
title:      "You Don't Need a Style Guide."
date:       2015-05-28 06:00:00
categories: ["Random Thoughts"]
---

Firstly, I need to say that I think having a style guide **is** important.  They help ensure that your projects are clean and consistent, and help developers adapt to your code more quickly.

The point that I want to make in this post, is that there is no need for you (or your company) to roll your own.  The Internet is [already littered with style guides](https://www.google.com/search?sclient=psy-ab&es_sm=122&btnG=Search&q=javascript+style+guide), and there are a lot of reasons to pick one of them instead of creating a new one.

Many public style guides are very well maintained, as well as being very thorough.  There are a lot of rules to consider when creating a style guide, and anything that isn't covered will be questioned sooner or later and need to be added.  Public style guides have the benefit of covering these for you, while being updated by their community with little to no effort by you.  Even better, [some tools](http://jscs.info/) come pre-configured for the [more popular style guides](http://jscs.info/overview.html#presets).

The only reason for creating your own style guide can be summed up pretty shortly *"But I like tabs not spaces!!"*. So what? [They don't matter](http://blog.codinghorror.com/death-to-the-space-infidels/).  If your code is properly compiled, they won't affect your user.  The only thing that really matters is that your code is consistent across your project.


There are other areas of your projects that will affect your users, and could probably use some love.  Performance, code abstractions/interfaces, UI pattern libraries.  These are the things that deserve your time, not where the comma should be placed in an object literal.
