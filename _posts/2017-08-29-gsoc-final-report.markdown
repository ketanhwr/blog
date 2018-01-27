---
layout:     post
title:      GSoC '17 - Final Report
date:       2017-08-29 03:31:19
summary:    This is the final report for Google Summer of code.
categories: gsoc
---

## General Improvements and Bug Fixes

This is the final report for Google Summer of Code written by Ketan Gupta.

### Summary

My aim for the summer was to add a bunch of features in Tiled. This included small features (like improving the custom command system, autocrop, etc.) to some major features (layer locking, automatically resized maps and improving the polygon/polyline editing tools).

Apart from this, I also planned to fix some bugs that were discovered during the GSoC period mainly because I was expecting some bugs to come up due to the release of Tiled 1.0 version. Although, most of my time was spent in adding features itself.

You can take a look into my proposal here: [Proposal](https://docs.google.com/document/d/1Xkqn64VydIIK0J9WuLwGcUqbC0xY7Fs-KpXgF8lMwz4/).

I also tried to maintain regular blogs which showed my progress for that particular period. You can read all the updates [here](http://ketangupta.in/blog/archive/).

Apart from my blogs, I also maintained a workflowy to-do list which you can see here: [Notes](https://workflowy.com/s/E6IW.NbDfz39WLJ)

### Code

#### Autocrop

Pull request: [#1574](https://github.com/bjorn/tiled/pull/1574)

This was a small feature requested in [#642](https://github.com/bjorn/tiled/issues/642). Triggering this action results in resizing of the map to the region of current Tile Layer.

#### Custom Command System

Pull requests: [#1580](https://github.com/bjorn/tiled/pull/1580), [#1593](https://github.com/bjorn/tiled/pull/1593), [#1648](https://github.com/bjorn/tiled/pull/1648), [#1699](https://github.com/bjorn/tiled/pull/1699)

![custom command system](http://ketangupta.in/blog/images/tiled-commands-new.png)

These couple of pull requests added support for working directory ([#941](https://github.com/bjorn/tiled/issues/941)), used the debug console to show output of commands ([#1552](https://github.com/bjorn/tiled/issues/1552)) and some minor additions. I also added `%executablepath` magic variable.

I even made significant changes in the custom command system during my pre-GSoC contributions which helped a lot during the GSoC period.

#### Tool Options

Pull requests: [#1586](https://github.com/bjorn/tiled/pull/1586), [#1620](https://github.com/bjorn/tiled/pull/1620)

![tools option](http://ketangupta.in/blog/images/tiled-toolspecific.png)

Another small addition was a 'tool specific tool bar'. Originally, in [#1084](https://github.com/bjorn/tiled/issues/1084), tool buttons for rotating/flipping. This was extended to make a 'Tool Options' tool bar, which would provide tool buttons for actions unique to a particular tool.

The first pull request added the tool specific tool bar and options for Stamp Brush and Bucket Fill Tool. The second pull request introduced `AbstractTileSelectionTool` (which would be extended by all the tile selection tools. This reduced code duplication) and tool options for the selection tools.

#### Move Selection Feature

Pull requests: [#1607](https://github.com/bjorn/tiled/pull/1607) (closed), [#1647](https://github.com/bjorn/tiled/pull/1647) (open)

This feature was requested in [#650](https://github.com/bjorn/tiled/issues/650). This was a bit complicated since it required a lot of feedback.

The first pull request was closed because it added move selection as a new tool. After discussion with the mentors, it was decided that the current pull request will be closed.

```
Just to add an explanatory note: this PR was closed because
@ketanhwr introduced an AbstractTileSelectionTool in #1620 
and will now merge the functionality of the Move Selection 
tool added here with that class.
```

The second pull request is still open. It still needs a bit of furnishing before it gets merged to the master branch. This time, the move selection feature was implemented within the `AbstractSelectionTool` in order to provide this functionality after selecting itself.

#### Layer Locking

Pull requests: [#1627](https://github.com/bjorn/tiled/pull/1627), [#1658](https://github.com/bjorn/tiled/pull/1658)

![layer locking](https://image.ibb.co/hekQHQ/Screenshot_from_2017_08_23_23_22_47.png)

This feature was requested in [#734](https://github.com/bjorn/tiled/issues/734). Apart from implementing layer locking, the visibility icon was shifted as well. In the above image, the change in the layer dock is quite visible. Layer locking is recursive, i.e. if a parent layer is locked, then the child layer is automatically locked.

The second pull request was a minor addition which previewed a red highlight in case the layer is locked. This gave a clear indication to the user that the current layer is locked.

#### Infinite Maps

Pull requests: [#1635](https://github.com/bjorn/tiled/pull/1635), [#1640](https://github.com/bjorn/tiled/pull/1640), [#1651](https://github.com/bjorn/tiled/pull/1651), [#1692](https://github.com/bjorn/tiled/pull/1692), [#1696](https://github.com/bjorn/tiled/pull/1696)

This feature was requested in [#260](https://github.com/bjorn/tiled/issues/260), and it was a major project in itself. It took me about 1-2 months to complete it (two small pull requests are still left to be merged). Here's a working prototype of this feature:

![infinite maps](http://ketangupta.in/blog/images/infinite-demo.gif)

The basic overview of this feature was to have an infinite grid, which can be drawn upon without worrying about the bounds of the layers. Since it has a lot of pull requests in itself, I'll explain what I've done in each of them:

##### Supporting Infinite Maps [#1635](https://github.com/bjorn/tiled/pull/1635)

In order to have an infinite canvas, there was a need to store the Tile Layer data in chunks. This patch aimed to change the way the data was previously stored (which was in a grid of fixed size) to a much more flexible and memory efficient way. Now, the Tile Layer consists of `Chunk` each of dimension `CHUNK_SIZE * CHUNK_SIZE` (this is kept 16 as of now), and these chunks are created whenever we paint on an area whose chunk has not yet allocated.

##### Adds iterator and const_iterator for TileLayer [#1640](https://github.com/bjorn/tiled/pull/1640)

I added a custom iterator and const_iterator in order to iterate over all the tiles in the TileLayer along with getting their coordinates easily.

##### Automatically Resize Maps [#1651](https://github.com/bjorn/tiled/pull/1651)

This was the base pull request for adding infinite maps. The `TileLayer::bounds()` function was modified to store current bounds of the layer, infinite grid was rendered, and every other change was done which was necessary for each tool and action to work on the infinite grid. This took a lot of time to code and merge since it required a lot of testing as well as feedback.

##### Fix automap [#1692](https://github.com/bjorn/tiled/pull/1692)

After modifying the `TileLayer::bounds()` function, it introduced a bug in Automapping of infinite maps. This adds the feature of Automapping to infinite maps as well.

##### New chunk based format for infinite maps [#1696](https://github.com/bjorn/tiled/pull/1696)

Currently each tile layer is stored in the following format:

```
<layer name=".." width="5" height="5">
  <data encoding="..">
    ...
  </data>
</layer>
```

For infinite maps, we obviously cannot store the whole `bounds()` of the TileLayer (otherwise what would be the point of allowing infinite maps in the first place if you store it in the grid eventually). So this pull request aimed to store chunks of Tile Layer Data for memory optimisation.

```
<layer name=".." width=".." height="..">
  <data encoding="..">
    <chunk x=".." y=".." width=".." height="..">
      ..
    </chunk>
    ...
  </data>
</layer>
```

#### Polygon Editing Tools

Pull requests: [#1674](https://github.com/bjorn/tiled/pull/1674) (closed), [#1682](https://github.com/bjorn/tiled/pull/1682), [#1683](https://github.com/bjorn/tiled/pull/1683) (open), [#1685](https://github.com/bjorn/tiled/pull/1685), [#1693](https://github.com/bjorn/tiled/pull/1693), [#1705](https://github.com/bjorn/tiled/pull/1705) (open)

The first pull request was closed since I added a lot of features in one pull request itself. So it was decided that I open separate pull requests for each of the feature. Here's an explanation for each pull request after the first one:

##### Delete key deletes selected nodes [#1682](https://github.com/bjorn/tiled/pull/1682)

This was requested in [#1555](https://github.com/bjorn/tiled/issues/1555), and was a small addition to make sure that if atleast 1 node is selected in the polygon, then the delete key should delete the selected nodes instead of the whole polygon.

##### Allows extending of the polyline [#1683](https://github.com/bjorn/tiled/pull/1683)

Requested in [#157](https://github.com/bjorn/tiled/issues/157), the primary goal was to allow extending of a polyline. Currently, you can split a segment, then move around the nodes. But this is obviously a bad solution if the user wants to add multiple nodes. The pull request is stil open, but I expect it to get merged soon.
##### Adds option to remove an edge from polygon [#1685](https://github.com/bjorn/tiled/pull/1685)

This allowed conversion of a polygon to a polyline. Two consecutive nodes can be selected and the segment between them can be deleted to allow formation of a polyline.

##### Option to split polyline [#1693](https://github.com/bjorn/tiled/pull/1693)

This was another important feature and a bit tricky to implement. The primary motive was to allow splitting of a polyline into two polylines.

##### Double click splits a segment [#1705](https://github.com/bjorn/tiled/pull/1705)

Just like Inkscape, the idea of clicking on a segment to select both the nodes and double clicking it to split the segment into another node was pretty helpful. This pull request aims to implement that in Tiled. Currently it requires some feedback but it will be a nice addition to Tiled!

#### Other Improvements and Bug Fixes

Apart from the above mentioned contributions, I also made some minor changes: [#1588](https://github.com/bjorn/tiled/pull/1588), [#1706](https://github.com/bjorn/tiled/pull/1706)

##### Rename Polygon tool icon names [#1588](https://github.com/bjorn/tiled/pull/1588)

This was a minor bug created during the release of Tiled 1.0. The icons for Polyline and Polygon tool were swapped.

##### Adds icon for animation editor in the tileset editor [#1706](https://github.com/bjorn/tiled/pull/1706)

This was requested in [#1686](https://github.com/bjorn/tiled/issues/1686). This patch added an icon for opening the animation editor in Tileset Editor in the main toolbar.

#### Documentation

Pull requests: [#1701](https://github.com/bjorn/tiled/pull/1701), [#1708](https://github.com/bjorn/tiled/pull/1708) (open)

I added most of the documentation in [#1701](https://github.com/bjorn/tiled/pull/1701). Currently the documentation for infinite maps is left, which I've already made a pull request and will get merged soon: [#1708](https://github.com/bjorn/tiled/pull/1708)

### What's Left

The following tasks are still left:

- Allow closing of a polyline into a polygon.

### The GSoC Experience

The past few months have been great working with Tiled! I learned a lot of new things about various technologies and gained a lot of exposure. I had been a bit active in open source before, but working with Tiled gave me a far more better experience in the open source world than what I had been involved in previously. I still plan to contribute to Tiled after GSoC ends, and possibly learn a lot more!