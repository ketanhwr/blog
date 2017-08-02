---
layout:     post
title:      GSoC '17 - Week 8 and 9
date:       2017-08-02 03:31:19
summary:    Working prototype of infinite maps!
categories: gsoc development
---

<center><img src="{{ site.baseurl }}/images/second-eval.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em; margin-bottom: 20px"><i>A really great feedback.</i></center>

## Minor Addition

I added a simple feature [here](https://github.com/bjorn/tiled/pull/1658). It ensures a red highlight over the preview region whenever you're working on locked layer. This will help, when a parent layer is locked, but the child layer isn't locked (because it's not quite evident that the user won't be able to work on the child layer as well).

## Infinite Maps

Current state of the pull request: [#1651](https://github.com/bjorn/tiled/pull/1651). Last 2 weeks were a bit occupied due to college but I still managed to work properly on the weekends. This task requires a lot of testing and feedback, so it's been quite slow in progression.

<center><img src="{{ site.baseurl }}/images/infinite-demo.gif" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em; margin-bottom: 20px"><i>Working Prototype. (Open this in a new tab for a clearer view)</i></center>

Everything I could possibly test works now, which is pretty great since I was very skeptical during the beginning if I would be able to even start it. Thanks a lot to bjorn and Ablu for their feedback and help!

## Second Evaluation

Due to the college's internship season coming up, I couldn't get much time during the last 2 weeks. So I got a bit worried if I'd be able to pass the second evaluation. Luckily I passed it, and I hope to work with more commitment now. The next task is polygon editing tools and let's see where it goes :-)

To track the current plans, you can read the notes I'm trying to maintain: [Notes](https://workflowy.com/s/E6IW.NbDfz39WLJ).