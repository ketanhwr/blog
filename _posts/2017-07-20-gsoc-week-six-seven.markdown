---
layout:     post
title:      GSoC '17 - Week 6 and 7
date:       2017-07-20 03:31:19
summary:    Tinkering around with automatically resized maps!
categories: gsoc
---

## Merged Features

<center><img src="{{ site.baseurl }}/images/selection-tools.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em; margin-bottom: 20px"><i>Selection Tool Options</i></center>

[#1620](https://github.com/bjorn/tiled/pull/1620) was merged last week. Now the selection tool options are available in the toolbar as well! They work similar to how they're implemented in GIMP. You can lock a particular mode or use keyboard modifiers to switch in between modes. I introduced `AbstractTileSelectionTool` via this which wasn't a very tough thing to do.

[#1640](https://github.com/bjorn/tiled/pull/1640) was also merged last week itself. It inroduced `iterator` and `const_iterator` for `TileLayer` class. This was a simple and fun task to finish. I learnt about writing custom iterators, which turned out to be pretty easy!

<center><img src="{{ site.baseurl }}/images/two-commits.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em; margin-bottom: 20px"><i>Stupid me.</i></center>

[#1648](https://github.com/bjorn/tiled/pull/1648) was a smaller patch I made for improving `%executablepath`. bjorn suggested using `QStandardPaths::findExecutable`, when the executable wasn't a file but was on PATH instead.

_Note to self: Always test before pushing._

## Move Selection Feature

I closed the previous pull request ([#1607](https://github.com/bjorn/tiled/pull/1607)) because it implemented move-selection feature as a new tool. After a small discussion, it was decided that it would be a much better option to implement the feature within `AbstractTileSelectionTool` and use it by keyboard modifiers. I've made a pull request for this but it would take some time before I work on it properly and get it merged ([#1647](https://github.com/bjorn/tiled/pull/1647)).

## Infinite Maps

The prototype is working pretty nicely as of now. I've spent the past few days playing with Tiled's code and now after making a couple of changes, the infinite map feature works great! You can follow the patch here: [#1651](https://github.com/bjorn/tiled/pull/1651).

<center><img src="{{ site.baseurl }}/images/infinite-maps.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em; margin-bottom: 20px"><i>Current status of this task.</i></center>

The user can paint on the grid freely, and most of the tools work great! The bucket fill tool fills on the current bounds of the tile layer and therefore user need not worry about the map taking too much memory. Saving/Loading work fine now, but I introduced a `startx` and `starty` attribute in TileLayer in the TMX format because otherwise, every layer would start from (0, 0) whenever loaded.

The current plan is to test and fix and that's what I have been doing for the past 2 days :p

## Second Evaluation

Now that my college has started, it might get hectic sometimes with managing college and GSoC together. Luckily, my time table gives me a lot of free time during the day so I haven't faced any problem as of now. The second evaluation is coming up in the next week, so fingers crossed! :-)

To track the current plans, you can read the notes I'm trying to maintain: [Notes](https://workflowy.com/s/E6IW.NbDfz39WLJ).