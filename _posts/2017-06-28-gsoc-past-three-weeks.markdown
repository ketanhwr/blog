---
layout:     post
title:      GSoC '17 - The past 3 weeks
date:       2017-06-28 05:31:19
summary:    A lot happened over the past few weeks!
categories: gsoc
---

## Specific Tool Bar

The tool specific toolbar was recently merged and it was implemented in such a way so that new tools can be added easily! Thanks to Ablu and bjorn for their help throughout this patch. You can see the implementation [here](https://github.com/bjorn/tiled/pull/1586).

Previously I made a new class `ToolSpecificToolBar` which inherited the `QToolBar` class but it wasn't a very good implementation design-wise. The final implementation was pretty simple infact, I added a function in the class `AbstractTool` which could be overriden to add new tools specific to a particular tool.

{% highlight cpp %}
class AbstractTool : public QObject
{
    Q_OBJECT

public:
    AbstractTool(const QString &name,
                 const QIcon &icon,
                 const QKeySequence &shortcut,
                 QObject *parent = nullptr);

    virtual ~AbstractTool() {}

    ...
    ...

    virtual void populateToolBar(QToolBar*) {}

    ...
    ...

};
{% endhighlight %}
<center style="font-size: 0.9em; margin-bottom: 20px; margin-top: -5px;"><i>AbstractTool.h</i></center>

This function would then be overriden by the tools to add the specific tools.

{% highlight cpp %}
class StampBrush : public AbstractTileTool
{
    Q_OBJECT

public:
    StampBrush(QObject *parent = nullptr);
    ~StampBrush();

    ...
    ...

    void populateToolBar(QToolBar *toolBar) override;

    ...
    ...

};
{% endhighlight %}
<center style="font-size: 0.9em; margin-bottom: 20px; margin-top: -5px;"><i>StampBrush.h</i></center>

_Protip: Don't rely on copy-paste too much. I made [this](https://github.com/bjorn/tiled/commit/1679f3fd797eb1b67e1a55898c93889c7e1ba1c9) mistake which later bjorn corrected._

## Move Selection Feature

The move selected feature turned out to be a bit more complicated than I expected. I rolled out a new tool by extending `AbstractTileTool`. The first way I implemented it was by using cut-paste. As in, when a user starts dragging, then the selected area would be removed from the layer, and copied into the `ClipboardManager` and then the dragging stops, the layer cut would be pasted over to the layer.

This was just to get an idea of the implementation. In the end the working is similar to `StampBrush`, but creating a preview layer and passing it onto `BrushItem` for previewing and then using `PaintTileLayer` to paint the preview layer over the current layer. You can look over the implementation [here](https://github.com/bjorn/tiled/pull/1607).

I proceeded to add a 'Duplicate' feature as well, which would duplicate the selected area instead of moving it. This can be done by holding the Ctrl modifier. The feature isn't merged right now since bjorn suggested that it would be better to make an `AbstractSelectionTool` which would then be inherited by the Tile Selection Tool, Magic Wand Tool and Select Similar Tile tool as well.

This would reduce code repetition. Also, it would help in providing specific tools for all the selection tools with minimum effort. You can look over the discussion in [this](https://github.com/bjorn/tiled/pull/1620) pull request to get an idea of what I'm talking about.

## Layer Locking

This feature turned out to be pretty easy, and I think this would be my first pull request that got merged within two days <span><img src="{{ site.baseurl }}/images/tongue-emoticon.png" style="width: 1.1em"></span>

The main effort went into adding the locking option in the GUI. I moved the eye icon to a different column as well. This took a whole day (you'll understand if you try Qt GUI). This was supported by adding `isLocked()` and `isUnlocked()` functions in the `Layer` class. `isLocked()` returns true if the current layer is locked and false otherwise. `isUnlocked` returns true if the current layer and all its parent layers are unlocked as well. The naming doesn't make much sense, I know about that already.

{% highlight cpp %}
bool Layer::isUnlocked() const
{
    const Layer *layer = this;
    while (layer && !layer->isLocked())
        layer = layer->parentLayer();
    return !layer;
}
{% endhighlight %}
<center style="font-size: 0.9em; margin-bottom: 20px; margin-top: -5px;"><i>Layer.cpp</i></center>

The next day I added a check of `currentLayer()->isUnlocked()` in every place which could modify the layer. This was a pretty simple task, and just involved searching places throughout the codebase which could edit a tile layer.

There are still some features/issues left for Layer Locking, but it would be better to proceed after getting a user feedback.

## Infinite Maps

Supporting infinite maps is the next task in my proposal. This will the toughest thing I'll be working on Tiled so far. You can take a look over the discussion [here](https://github.com/bjorn/tiled/issues/260). [MyPaint](http://mypaint.org/about/) is such a software which supports an infinite canvas. [Paint.js](https://github.com/Squarific/Paint.js/) is also a similar thing. I'll first take a look into their working before starting to implement it in Tiled.

## First Evaluation

It's time for the first evaluation now. I've completed the tasks mentioned in my timeline that were upto the first evaluation so I'm confident that I'll pass this one. Still, fingers crossed! :-)