---
layout:     post
title:      async.auto
date:       2018-01-19 03:31:19
summary:    Role of Data Structures and Algorithms in Software Development.
categories: development
---

Many software developers resent competitive programming, or in general, algorithms and data structures. Competitive programmers, on the other hand, are perplexed by the real world use of data structures, and find it monotonous.

Here I try to explain with a simple real world illustration, that unlike what most people believe, the two programming paradigms are closely intertwined.

## Javascript

If you’ve worked with Javascript then you know about its property to be asynchronous. For those who don’t know about asynchronous programming, I’ll explain it in short.

<center><img src="{{ site.baseurl }}/images/js-async.png" alt="Couldn't Load Image" /></center>

In javascript, any blocking code (I/O operations, network operations, etc.), is run in a different pool, so that the remaining code can be executed asynchronously. This way, the waiting time and execution time is reduced a lot. But it also changes the programming methodologies. The completion of execution of such asynchronous calls are handled through callback functions.

For a more detailed explanation, you can refer this blog: [https://www.sohamkamani.com/blog/2016/03/14/wrapping-your-head-around-async-programming/](https://www.sohamkamani.com/blog/2016/03/14/wrapping-your-head-around-async-programming/)


Due to asynchronous nature, there often exists a problem called as “callback hell” in javascript codes. Callback hell can be explained simply by this image:

<center><img src="{{ site.baseurl }}/images/callback-hell.jpg" alt="Couldn't Load Image" /></center>

Callback hell is normally caused when you want the results of one asynchronous method in another one repeatedly. This is often a very big problem faced by js developers.

## async

> Async is a utility module which provides straight-forward, powerful functions for working with asynchronous JavaScript.

Async is a very popular javascript library to avoid callback hell (and a lot of other problems). One of the most used functions in async is `auto`. According to the documentation, the function is explained as:

> Determines the best order for running the AsyncFunctions in tasks, based on their requirements. Each function can optionally depend on other functions being completed first, and each function is run as soon as its requirements are satisfied.

I’ll explain in detail. Suppose you have many functions. Some of these functions need the results of some other functions to run. When you have many such functions and dependencies, determining the order of execution can be a bit tricky. `async.auto` is used to solve this problem. Here is a simple code to for explanation:

{% highlight javascript %}
async.auto({
    get_data: function(callback) {
        console.log('in get_data');
        // async code to get some data
        callback(null, 'data', 'converted to array');
    },
    make_folder: function(callback) {
        console.log('in make_folder');
        // async code to create a directory to store a file in
        // this is run at the same time as getting the data
        callback(null, 'folder');
    },
    write_file: ['get_data', 'make_folder', function(results, callback) {
        console.log('in write_file', JSON.stringify(results));
        // once there is some data and the directory exists,
        // write the data to a file in the directory
        callback(null, 'filename');
    }],
    email_link: ['write_file', function(results, callback) {
        console.log('in email_link', JSON.stringify(results));
        // once the file is written let's email a link to it...
        // results.write_file contains the filename returned by write_file.
        callback(null, {'file':results.write_file, 'email':'user@example.com'});
    }]
}, function(err, results) {
    console.log('err = ', err);
    console.log('results = ', results);
});
{% endhighlight %}

Here, `get_data` and `make_folder` do not need any result so they don’t have any dependency mentioned. `write_file` needs the results of `get_data` and `make_data`, and `email_link` needs the results of `write_file`. `async.auto` determines the best order to run such functions, possibly in parallel, for faster execution as well as less pain for the user.

## The algorithm

Okay, so the question now is, how is any of this connected to data structures and algorithms. Well, simple question: how would you implement `async.auto`?

Let me put this in simpler terms: Given some tasks and their dependencies, how would you determine an order to fulfill all these dependencies _or_ tell that there is no possible order to run the tasks?

I’ll try to explain the solution to this problem using the Graph data structure and Topological sort algorithm.

## Graph and a Directed Graph

Taking the simple definition from wikipedia, a graph is a structure amounting to a set of objects in which some pairs of the objects are in some sense "related". The objects correspond to mathematical abstractions called vertices (also called nodes or points) and each of the related pairs of vertices is called an edge. Typically, a graph is depicted in diagrammatic form as a set of dots for the nodes, joined by lines or curves for the edges.

<center><img src="{{ site.baseurl }}/images/graph.png" alt="Couldn't Load Image" /></center>

A directed graph is a set of nodes connected with directed edges. A directed edge is just a connected between two nodes which has a sense of direction.

<center><img src="{{ site.baseurl }}/images/directed-graph.png" alt="Couldn't Load Image" /></center>

If we try to model our problem in terms of a graph, we can see that all the tasks can be imagined as different nodes in the graph, and dependencies as directed edges between these nodes.

<center><img src="{{ site.baseurl }}/images/example-graph.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em; margin-bottom: 40px; margin-top: -20px;"><i>I'm not a designer, please forgive me for this illustration.</i></center>

The above graph is a model for the example `async.auto` code written above.

## Topological Order

Topological order of a directed graph, explained in simple terms, is a linear order of nodes such that every directed edge is facing rightwards. It’s quite clear in the image below.

<center><img src="{{ site.baseurl }}/images/topological.png" alt="Couldn't Load Image" /></center>

So now, if we think about our original problem, it’s solution is basically to find the topological order of the graph we modeled.
Why? Since dependencies are modeled as edges, we would want to find such an order of nodes, such that every dependency is satisfied i.e. every edge pointing towards a node should be rightwards.

<center><img src="{{ site.baseurl }}/images/example-topological.png" alt="Couldn't Load Image" /></center>
<center style="font-size: 0.9em; margin-bottom: 40px; margin-top: -20px;"><i>Topological Order for our example graph.</i></center>

There are plenty of algorithms to find the topological order of a directed graph. The algorithm used in the async library is Kahn’s algorithm which you can read about here: [https://www.geeksforgeeks.org/topological-sorting-indegree-based-solution/](https://www.geeksforgeeks.org/topological-sorting-indegree-based-solution/)

## Conclusion

I hope I gave a clear understanding of importance of data structures and algorithms in software development. This was just a small example, and there exist countless similar examples to reiterate this.

If you’re interested in the actual implementation of `async.auto`, then you can read it here: [https://caolan.github.io/async/auto.js.html](https://caolan.github.io/async/auto.js.html)
