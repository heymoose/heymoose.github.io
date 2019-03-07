---
layout: post
title: Comparing Stack and Queue data structures in Javascript
subtitle: Testing the efficiency of using arrays or objects for data storage in stacks and queues
show-avatar: true
social-share: false
---

I've been making an effort to get back to the basics lately.  And by basics I don't mean something like language syntax.  I'm talking about computer science basics in general.  Algorithms, data structures, networking, things like that.

In that effort, I revisited a topic that I haven't really given much thought to since college, and that's the simple data structures of stacks and queues.  I got to thinking about what the best way would be to implement a stack and a queue using functional programming in Javascript.  Specifically, do you use an Object {} or an Array [] to actually store the internal data of the stack or queue?  I had my suspicions, but I wanted to take a look at what the internet had to say on the subject.  After googling around for the thoughts of other programmers, I realized that the answers were kind of all over the place.  I thought there was really a "best" answer for each case, so some of what I was seeing was surely wrong.

And it turns out I was right.  To test things out, I created my own implementations of stacks and queues and tested out the time of execution for each one.  It was an interesting thought and experiment and I certainly learned something from it.  Hopefully you do to.

I created a gist for each data structure.  Check out the stack gist [here](https://gist.github.com/heymoose/bb4b327f071bd1113bed80e4035848b8), and the queue gist [here](https://gist.github.com/heymoose/30189d18efc1d8f582068f0bdd21854f).  Hope you find them interesting!
