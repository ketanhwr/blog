---
layout:     post
title:      Google Summer of Code '17
date:       2017-05-28 05:31:19
summary:    I got accepted into the GSoC 2017 program under the organisation Tiled!
categories: gsoc
---

<center><img src="{{ site.baseurl }}/images/gsoc-1.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em"><i>The congratulatory email.</i></center>
<br/>

The list of accepted student projects for Google Summer of Code '17 came on  4th May, 9:30 pm IST to be precise. I opened the website at 9:35 pm, searched `Ketan Gupta` and saw my project before I could complete my surname.

_Magical._

It was a moment of bliss. I had never been this surprised or happy since IOITC results back in high school.

I then proceeded to search up a couple of names of my friends who had applied as well. Most of my friends also got accepted, and we went out to have a nice chapo!

_Note: For non-IITR people, chapo is a substitute for 'treat'. It's part of the IITR lingo, and one of the most heard words on the campus._

## Tiled

The list of organisations selected for GSoC came on February 27. I had previously decided not to participate in GSoC (Looking back, I have no idea why I decided that) probably because I couldn't find a nice organisation. I decided to go through the organisations page anyway and came across Tiled. It was in C++ and the ideas page seemed simple. Tiled seemed interesting to me due to the following reasons:

- It was the first time Tiled had been selected for the program and therefore, it had very few people and therefore, less competition. (We used to call this _bhasad_ whenever we discussed various organisations inside SDSLabs)
- The code is primarily in C++. Prior to GSoC, my only development experience in C++ had been in Turbo C++, but due to my involvement in competitive programming, I got a bit fluent in C++11.
- I have been interested in game development for a long time, and Tiled seemed a great way to dive into it. Many people involved with Tiled are either closely related to game development, or are, themselves, professional game developers.
- The mentors were very active and gave quick and helpful feedback. The communication methods were organised. Tiled has one forum and one primary chat which is linked to IRC as well as Gitter.

<center><img src="{{ site.baseurl }}/images/gsoc-2.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em"><i>First contact.</i></center>
<br/>

I registered on the forum and got involved. The mentors replied quickly and were really helping. I went through the issues page, and I found a simple issue that I decided to get started with. [Link to Issue](https://github.com/bjorn/tiled/issues/1127)

Unfortunately, Tiled is written using the Qt framework. For those who don't know Qt, it is an application development framework for C++. I had never worked in Qt, and it was totally a new dimension for me. I quickly looked up documentation and guides, and google helped me as well. Someone had previously worked on this issue, and even though his pull request wasn't merged, it helped me a lot to start working on the issue. I took feedback from the problems in his patch and quickly submitted a pull request the next day.

<center><img src="{{ site.baseurl }}/images/gsoc-5.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em"><i>The first pull request.</i></center>
<br/>

As the days passed by, I went through the codebase. It was *huge*. I could't understand most of it, but slowly and slowly, I got the basic idea. I started working on the custom commands system, and my next pull request was comparatively a bigger patch compared to the previous once and I learned a lot of new things while I was working on it. I also looked into other pull requests and helped in reviewing them, mostly on the basis of coding style.

I still wasn't sure about my proposal, because I was totally a noob in Qt, and I couldn't understand how I would tackle any project mentioned in the ideas page. At this point of time, I realised how tough writing a proposal is! The mentors suggested that I take up `General Improvements and Bug Fixes` as my proposal. One of my seniors ([@karandesai-96](https://github.com/karandesai-96)) suggested that this project is normally given high priority since it helps in closing a lot of old issues which developers don't work upon.

His proposal was a big help, and I took it as a template for my proposal. I quickly went through the issue tracker and made a list of some issues that seemed interesting. It took a few days to write my proposal properly, but I still couldn't explain the issues properly mainly because of my lack of knowledge of the codebase as well as Qt.

<center><img src="{{ site.baseurl }}/images/gsoc-3.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em"><i>My total contribution before submitting the final proposal.</i></center>
<br/>

Due to lack of time, and quizzes and assignments piling up, I decided to submit my proposal in a state I wasn't very happy with. I slowly lost confidence since I hadn't contributed for some while and number of students submitting patches increased with time. I still had some hope of getting selected, because I remained the highest contributor till the results came.

## Result

In the end, Tiled got 3 slots, and I got accepted in one of it. My mentors are Erik Schilling ([@Ablu](https://github.com/Ablu)) and Thorbjørn Lindeijer ([@bjorn](https://github.com/bjorn)) (surprisingly, both of them are from Germany). Tiled 1.0 was released recently, and I felt really great contributing towards it!

<center><img src="{{ site.baseurl }}/images/gsoc-4.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em"><i>The congratulatory forum post.</i></center>
<br/>

I had a nice time in the community bonding period, and the coding phase is about to begin soon. I hope to continue writing blogs regarding the development of Tiled. Till then, Auf Wiedersehen!
