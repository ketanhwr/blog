---
layout:     post
title:      GSoC '17 - Week 5
date:       2017-07-10 03:31:19
summary:    Getting started with infinite maps!
categories: gsoc
---

<center><img src="{{ site.baseurl }}/images/patreon-appreciation.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em"><i>This made my day.</i></center>
<br/>

## AbstractTileSelectionTool and Move Selection Tool

I recently introduced the `AbstractTileSelectionTool` in [#1620](https://github.com/bjorn/tiled/pull/1620). The main reason behind this was to reduce code duplication. This class is further inherited by `TileSelectionTool`, `MagicWandTool` and `SelectSameTileTool`.

It also introduces specific tools for these three classes and as per the current plan, the move selection feature will be implemented within `AbstractTileSelectionTool` so that a selection can be moved just by using some keyboard modifiers (like GIMP) instead of introducing a new tool.

This change is yet to be reviewed so let's see where it goes.

## Infinite Maps

I mentioned some doubts in the [issue tracker](https://github.com/bjorn/tiled/issues/260#issuecomment-312618241) and you can read further to get an idea of the current plan.

The first pull request ([#1635](https://github.com/bjorn/tiled/pull/1635)) modifies how `TileLayer` stores all the tile cells. Currently, it stored all the cells in a `QVector<Cell>` of size `mWidth * mHeight` which, obviously, is an inefficient method if we consider automatically resizing the maps.

So my approach towards this was storing `Chunks` of cells in the `TileLayer` class. `Chunks` are basically a cell grid of 16x16 size. Whenever the user paints at a particular point, the cell of that particular chunk gets modified. If the chunk doesn't exist, it gets allocated. This way, we only store the non-empty cells. This is a far more faster method than the previous one! So now, instead of `QVector<Cell> mGrid`, the data structure used is `QHash<QPoint, Chunk> mChunks`. I used `QMap` before but [bjorn](https://github.com/bjorn) suggested that it would be better to use a `QHash` since it's faster in average case.

The next pull request ([#1640](https://github.com/bjorn/tiled/pull/1640)) introduces a custom iterator for the class `TileLayer`. Previously, we had `QVector<Cell> grid(mWidth * mHeight)` which could be easily traversed through. But now, since we're storing the cells in random chunks, we need a custom iterator which would iterate through all the chunks and their respective cells and provide the method `key()` as well which would give the correct coordinate as well. This turned out to be an interesting task since I'd never implemented an iterator before. This PR is also yet to be reviewed and I plan to write a tutorial towards this after it gets merged!

To track the current plans, you can read the notes I'm trying to maintain: [Notes](https://workflowy.com/s/E6IW.NbDfz39WLJ).