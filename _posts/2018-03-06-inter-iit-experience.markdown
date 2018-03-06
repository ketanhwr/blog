---
layout:     post
title:      Road to Inter IIT
date:       2018-03-06 03:31:19
summary:    How we ended up winning an unexpected gold medal at Inter IIT Tech Meet.
categories: interiit
---

The 6th Inter IIT Tech Meet was organised at IIT Madras from 5th-7th January ‘18. As a part of the IIT Roorkee contingent, I took part in the ‘Orbital Simulator’ event along with my teammates Mohan Agrawal and Utkarsh Gupta.

## Preparing for the event

Towards the end of October, I got a call from Utkarsh one day while I was sleeping peacefully. He blurted, “Oye, Inter IIT hackathon ke liye register karna hai. Tu, mai aur Mohan. Chalega?” (Translation: I need to register for the Inter IIT Hackathon event. You, me and Mohan. In?). I drowsily replied “Sure!” and went back to sleep, unaware of what I had just signed up for.

I just knew that the event was supposed to be a “hackathon”, I had no idea what the theme would be or if any problem statement would be provided. After a week or so, we got shortlisted for the IITR contingent. Just like me, Utkarsh too had no idea what the event was exactly. During the last week of November, I learnt that the hackathon is related to astrophysics, and thus, we trusted Mohan, our Engineering Physics guy on this (Later he would go on to rant about how it was pretentious of IITM to call orbital mechanics, 'astrophysics’). While Utkarsh and I were pretty nervous about the nature of the event, Mohan calmly said that he would give us some reading material during December, and that it would be enough for the hackathon.

Needless to say, Utkarsh and I were both put at ease by Mohan’s composure. I left for a much-awaited Goa trip and from there, went to Bangalore (for a winter internship), while Utkarsh and Mohan stayed in Roorkee. December passed by and the three of us had done absolutely nothing for the meet. I eventually decided to visit the Inter IIT website to read the problem statement. It went something like this:

> Many space agencies have been working on the possibility of building a human settlement on Mars. However, Mars is plagued with a number of agents that could threaten our sustenance on the planet. The hackathon will look at one such agent (say X). The PS will be revealed on the day of the event and teams have 24 hours to code and come up with a simulator that would help deal with X. Hint: X is an agent that also threatens human sustenance on Earth albeit rarely. Teams will need to run the simulator to find the possibility of X in the next 5 years on Mars.

Sounds pretty generic right? At this point (only a week was left for the event), I realised that this event, in no way, was anything close to a hackathon that I had imagined. With a little bit of thinking, one can guess X to be asteroid impact and so did we, but it was still too vague to prepare anything solid. Confused and tensed, Utkarsh and I asked Mohan for the reading material. He told us about a couple of books and a few algorithms to read about. All of them related to orbital simulation and solving differential equations. It was probably too much to read, understand, and implement in a week.

<center><img src="{{ site.baseurl }}/images/interiit/chat.png" alt="Couldn't Load Image" style="width: 50%"/></center>
<center style="font-size: 0.9em; margin-bottom: 40px;"><i>I guess this image would give you some understanding of our state.</i></center>

Hence, we split the work. I decided to focus on implementing a particular n-body simulation algorithm that Mohan had dug out and Utkarsh was tasked with preparing all kinds of optimisations for a couple of differential equation solver we would be using. But naturally, looking after Physics of the problem was the job of the last remaining guy.
I decided to focus on Barnes Hut Tree algorithm for n-body simulations in particular. It seemed quite easy at first glance, and its implementation was based on a Quad Tree, something I had implemented a lot of times when I was into Competitive Programming. We weren't really tensed about implementation as all three of us were experienced programmers, the cause of all the tension, in this case, was that we had no idea what the fuck we would have to implement.

## Reaching Chennai

I took a train from Bangalore to Chennai on 4th of January along with Kush (who was also doing an internship at Bangalore and was part of IITR contingent). Unfortunately, my seat was full of bed bugs (which I realised the next morning)

<center><img src="{{ site.baseurl }}/images/interiit/cat.jpg" alt="Couldn't Load Image" style="width: 50%" /></center>
<center style="font-size: 0.9em; margin-bottom: 40px;"><i>This little guy was my first new friend in the IITM campus.</i></center>

I arrived on 5th morning, and immediately noticed the weather to be quite humid, much like summers in Roorkee. The IITM campus was very lush and had a lot of animals around (sometimes, a bit too much). I got acquainted with a friendly kitten when I first entered the hostel. I spent some time sleeping and listening to music while I waited for Mohan and Utkarsh to arrive. The event was originally supposed to be on the 5th, but it got rescheduled to the 6th of January. We were quite relieved because

- Mohan and Utkarsh were very tired after travelling from Roorkee to Chennai.
- My whole body was itching badly (thanks to the bed bugs)
- We hadn’t prepared anything concrete for the event.

We spent the day studying various algorithms for orbital simulation and techniques for solving differential equations. It was really tough to cover it all up in one day, but we tried our best. Mohan and Utkarsh had done some groundwork before arriving. Mohan had a working code for 2 body system in various reference frames, and Utkarsh had prepped some important solvers we might need. This helped us to utilize the day before the event to the maximum, as we knew what else we had to read.

## Orbital Simulation!

The event was finally rescheduled to start at 10 pm on the 6th of January 10 pm and finish at 6 am on the 7th of January. I’m not very experienced at pulling all nighters, in fact I’m terrible at it. So I decided to take a nice nap on 6th evening (eventually all 3 of us did the same!). We were asked to arrive at the CFI (Centre for Innovation) building by 9.30 pm. The area around CFI looked like some dilapidated godforsaken place in the middle of a jungle and we wasted a lot of time finding it. We arrived at 10 PM and the event eventually started at 10.30 PM as we were handed out the problem statements.

According to the problem statement, we were given the state vectors (positions and velocities) of 400 asteroids on 5th of January 2018 at 0000 hours IST as measured from a Kolkata observatory. The positions were given in alt-az coordinates while the velocities were given relative to Kolkata’s frame of reference. We were required to find the closest approach distance from Mars for the next 5 years for each asteroid along with the exact day on which this closest approach would take place.

Immediately after understanding the problem statement, I got sleepy. Utkarsh and I were just looking at each other and controlling our laughter since we had almost zero idea about the solution. Mohan on the other hand started thinking and tried to come up with an approach. Eventually Utkarsh and I understood what he was trying to do and started helping him, lest he punched one of us.

<center><img src="{{ site.baseurl }}/images/interiit/event.jpg" alt="Couldn't Load Image" style="width: 80%" /></center>
<center style="font-size: 0.9em; margin-bottom: 40px;"><i>The actual event.</i></center>

Our first task was to convert the coordinates and velocities to an inertial frame of reference. For our Solar System, Mohan explained, that the heliocentric coordinate system would be a good choice. As he was already experienced with astronomy, he explained how we’d go from topocentric to geocentric to heliocentric coordinates. This task was pretty complicated to do manually, but again Mohan, who had worked with a library called 'Astropy’ remembered that it had a coordinate conversion facility. Utkarsh started reading the documentation of astropy library to find a way to convert the coordinates and velocities into the heliocentric coordinate system (also called the ICRS). Meanwhile, I started implementing a brute force n-body approach which was obviously a very bad approach given that we had 400 asteroids, but we had to come up with at least some solution in the end. I thought up of coding Barnes Hut Tree algorithm eventually, but got stuck with the brute force approach itself. After an hour of trial and error we ended up writing a short code to convert all the coordinates and velocities from topocentric (with respect to Kolkata) to heliocentric frame of reference (a reference frame centered at  the barycenter of the solar system, that is, very close to the center of mass of the Sun).

Once we had our reference frame all set, we had to figure out the actual problem of finding closest approach. We argued and discussed on whether we should use use a 3-body simulation for each asteroid or go with the usual 2 body approach. Mohan showed by a small physical analysis(\*) that 2 body solver was all that would be needed (and why these guys wouldn’t give any more complex problem). We were already 6 hours into the competition now, with no output data yet. Something that comforted us was the fact that teams sitting in our room were struggling too (the organizer came around asking if we wanted ‘a hint’, which we denied of course 8-) ). It was a cakewalk from here. As I said, Mohan had already implemented a 2 body simulator (using Runge Kutta solver) before coming. We made a few changes and got it running for finding the closest approach distance and the exact day. Also, as per his analysis, we would require Mars’ position for each day for the next 5 years. For this we used the ephemerides provided by NASA JPL’s Solar System Dynamics group.

The final code was executed on my laptop, since it was the fastest among the three we had. The simulation took over an hour to execute and we had the final output data by 5.30 am. At this time Utkarsh was very sleepy, and he acts like a drunk baby when he’s sleepy. So he got really cranky and started doing weird things. I just kept laughing at this stage as I couldn’t believe we had pulled off an all nighter and had also come up with the final results. Mohan was still looking into the code and the output data, and checking if anything was wrong.

_\*I am skipping the actual solution for now, but rest assured, this analysis turned out to be actually correct as we had the most accurate output data. :) Anyone interested may contact me or Mohan._

## The Presentation

We were told before leaving, that we have to present our solutions to a judge as well. It was 7am, the three of us were very sleepy, and we needed to wake up again at 10 am to prepare a presentation. It was tough, really tough, but I woke up after sleeping just 2 hours and opened up Google Slides. Mohan and I made the presentation and then Mohan and Utkarsh re-worked the assumptions. Once prepared, we left for the IITM lecture halls where the presentation was to be held at 1 pm. After listening to the other teams’ solutions, it was clear that almost every team had followed a more or less similar approach for the first part (converting coordinates etc.), what mattered was:

- Being able to explain the actual analysis for the second part (finding closest approach) and along with the reasons behind the assumptions involved. The judge, who did his Bachelor's, Master's and PhD in Aerodynamics, was quick to obliterate assumptions that had a weak physical basis.
- Considering an inertial frame or not. Some teams used the frame of reference of Mars, Earth etc. which was an obvious mistake. Heliocentric was the clear winner!
- The method used for solving the differential equations.

<center><img src="{{ site.baseurl }}/images/interiit/presentation.jpg" alt="Couldn't Load Image" style="width: 80%" /></center>
<center style="font-size: 0.9em; margin-bottom: 40px;"><i>Utkarsh and Mohan trying to explain our assumptions.</i></center>

Our presentation went really smooth, and the judge was quite impressed since we had implemented 4th order Runge Kutta in our solution and the fact that we had come up with a really neat solution in the end. Only two or three teams had used dynamic solvers in total. A lot of teams attempted a static solution which was not entirely correct. Satisfied with our performance, we went to sleep. During the start of event, I had no hopes of finishing even in top 5, but after watching other presentations and delivering our presentation, somehow I felt that we might end up in top 3.

Who did we think might win? IIT Bombay. The presentation that they had prepared was, I would say, picturesque. Very neatly prepared (even plotted the final orbit for each asteroid) and smoothly delivered. 

Fate had something else in store.

## The Results

The final results were sum total of the scores of the relative accuracy of distances (35), relative accuracy of dates (35) for each asteroid (a score was calculated for each asteroid, and the final sum scaled to 35) and the presentation score (30). 

We kept sleeping until 6 pm, when I woke up because some people shouting and celebrating outside. I checked my messages to see that Punit (our contingent leader) had uploaded the results on the group.

I woke up Mohan and Utkarsh and we opened the results to see that we had finished 2nd! We shouted and celebrated and hugged (and slipped and fell on the bed :p). But I felt like we had checked out the wrong results. I opened the results once again to see that we had actually finished 1st! _Classic Steve Harvey right there_. This time, we celebrated even more loudly and ran up to the hall where the prizes were being distributed. Wouldn’t wanna miss the Gold now, would you?

<center><img src="{{ site.baseurl }}/images/interiit/results.png" alt="Couldn't Load Image" style="width: 35%" /></center>
<center style="font-size: 0.9em; margin-bottom: 40px;"><i>We actually won by a huge margin.</i></center>

At the end, IITR ended up with 5 gold medals (maximum by any IIT) out of 10 events! (We were 1st Olympics style :p)

After the prize distribution, we had dinner, watched Narcos, and took a nice 10 hour long sleep.

_Muy fantastico_

<center><img src="{{ site.baseurl }}/images/interiit/medal.jpg" alt="Couldn't Load Image" style="width: 70%" /></center>
<center style="font-size: 0.9em; margin-bottom: 40px;"><i>Getting the medals awarded.</i></center>

Overall, it was an amazing experience for me! I enjoyed a lot, learnt a lot of things and made a few new friends. Now we’re even more pumped up for the next Inter IIT Tech Meet :)

_You can find our code here: https://github.com/mohanagr/interiit_

_And the presentation here: goo.gl/TN4aKc_

