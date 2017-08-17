---
layout:     post
title:      GSoC '17 - Week 10 and 11
date:       2017-08-17 03:31:19
summary:    Improving Polygon Editing Tools!
categories: gsoc development
---

## Polygon Tool Improvements

I started off by adding all improvements in a single pull request ([#1674](https://github.com/bjorn/tiled/pull/1674)). Then the mentors suggested using interactive rebase for a nicer commit history. Even though the pull request was later closed (so that separate pull requests could be opened for each improvement), I learned about `git rebase -i`, which was pretty cool!

The separate pull requests are [#1682](https://github.com/bjorn/tiled/pull/1682), [#1685](https://github.com/bjorn/tiled/pull/1685) and [#1683](https://github.com/bjorn/tiled/pull/1683). [#1682](https://github.com/bjorn/tiled/pull/1682) and [#1685](https://github.com/bjorn/tiled/pull/1685) were merged quickly.

[#1682](https://github.com/bjorn/tiled/pull/1682) was a simple patch which allowed the delete key to delete the selected nodes rather than directly deleting the object. [#1685](https://github.com/bjorn/tiled/pull/1685) was a bit more complex that this. It allowed deleting a segment from a polygon to convert it into a polyline.

[#1683](https://github.com/bjorn/tiled/pull/1683) is for allowing extending a polyline with more nodes. This was quite complex since it involved switching the tools as well.

## Infinite Maps

The base pull request [#1651](https://github.com/bjorn/tiled/pull/1651) was finally merged!. The last few commits were dedicated to supporting infinite maps in isometric and hexagonal maps. There are a few things still left to do:

- Fixing Automap. Currently automap behaves rather weirdly in infinite maps.
- Implement a new chunk-based storage for infinite maps. Currently the infinite map is stored in the previous format itself.

## Final Evaluation

I got two internship offers after the first day of the intern season itself! :-)
That ended the intern season for me, so I've been fully committed to GSoC since that time. The final evaluation is coming up and I still have a few tasks left to do!

To track the current plans, you can read the notes I'm trying to maintain: [Notes](https://workflowy.com/s/E6IW.NbDfz39WLJ).