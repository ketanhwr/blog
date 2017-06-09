---
layout:     post
title:      GSoC '17 - Week 1
date:       2017-06-08 05:31:19
summary:    A review of my work in the first week with Tiled.
categories: gsoc development
---

## The 1<sup>st</sup> Patch

Officialy, the coding phase began on 30th May, but I starting making pull requests before the period. [#1574](https://github.com/bjorn/tiled/pull/1574) was my first pull request as a part of GSoC. The patch added an 'Autocrop' feature.

## Custom Commands

One of the tasks in my proposal was to make the current custom command system as similar to the 'External Tools' system in Qt Creator. I already made a couple of patches in March towards this, and they helped quite a lot!

<center><img src="{{ site.baseurl }}/images/tiled-commands-old.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em; margin-bottom: 20px"><i>This is how the custom command system looked previously.</i></center>

[#1580](https://github.com/bjorn/tiled/pull/1580) and [#1593](https://github.com/bjorn/tiled/pull/1593) are the two pull requests towards this task. The current custom command dialog supports choosing the executable file, setting the working directory, keeping a shortcut and displaying the output in the debug console. I learned about `QProcess` a lot while working towards all of these!

<center><img src="{{ site.baseurl }}/images/tiled-commands-new.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em; margin-bottom: 20px"><i>After a lot of patches.</i></center>

## Specific Tool Bar

The next task in my proposal was adding a tool-specific tool bar. The current state of pull request can be seen here: [#1586](https://github.com/bjorn/tiled/pull/1586). This task is bit tricky since it requires a good design before implementing it, so that it can be easily extended (for example, making it dockable or adding more tools/tool-specific tools).

<center><img src="{{ site.baseurl }}/images/tiled-toolspecific.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em; margin-bottom: 20px"><i>Work in progress.</i></center>

## Casting Pointers in C++

While working on the autocrop feature, I learned new methods of casting pointers from one form to another. [This link](https://stackoverflow.com/questions/28002/regular-cast-vs-static-cast-vs-dynamic-cast) gives a good explanation about `static_cast` and `dynamic_cast` in C++.

You might already know that you can store the reference of a child class in a pointer of type parent class. But you can use only the functions of parent class this way. `static_cast<>` and `dynamic_cast<>` help when you need to use functions of the child class in such a case. Take a look into what the current code is doing (this is part of my Autocrop patch).

{% highlight cpp %}
void MapDocument::autocropMap()
{
    if (!mCurrentLayer || !mCurrentLayer->isTileLayer())
        return;
    
    TileLayer *tileLayer = static_cast<TileLayer*>(mCurrentLayer);

    const QRect bounds = tileLayer->region().boundingRect();
    if (bounds.isNull())
        return;

    resizeMap(bounds.size(), -bounds.topLeft(), true);
}
{% endhighlight %}

The `mCurrentLayer` is a pointer to class `Layer`. The class `TileLayer` inherits class `Layer` and therefore `static_cast<>` helps when I need to use the `region()` function of the current tile layer which is stored in a pointer of type `Layer`.

## Move Selection Feature

I'm currently working on a new Move Selection feature which will help in dragging the selected area to a particular tile location. This seems a bit tricky too, but I have finally made a working prototype which works fine. I hope to make another pull request soon!

The first week has been pretty good so far, and I'm keeping up with the timeline mentioned in the proposal. Thanks for giving this devlog a read! :)