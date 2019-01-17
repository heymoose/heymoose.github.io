---
layout: post
title: Next Steps for Intrinsify-React
subtitle: Applying advanced React techniques to the Intrinsify app
show-avatar: true
social-share: false
---

As I talked about [in my last post]({% post_url 2019-1-8-Intrinsify-React-Step-One-Complete %}), the [Intrinsify-React](https://intrinsify-63630.firebaseapp.com/) app had reached a good point that utilized the basic ideas of React.  Most of this was refresher for me, but it was a good exercise and a good project to have in place to utilize some of the more advanced techniques that I've learned.

To that end, I'm diving back into the app in order to flesh it out and add functionality.  Some of what I want to add I'm adding less so because I think they are good ideas for the function of the app, but more because I'm just interested in applying the advanced React knowledge.  Here's my bucket list as it stand for what I plan to add:

1. Tests for existing functionality using jest and enzyme so that I can then adopt a test driven development approach to new code.
2. Manage global state using Redux, because Redux is great.  Side note - I have plenty of experience writing apps with Javascript with plain HTML/CSS and JQuery, usually in conjunction with some Kendo UI components.  I know what it's like to manually manage state in a growing app, and it is such a headache.  Redux is a breath of fresh air.
3. Think of a couple more 'pages' I can add so I have an excuse to use routing in the project.  One idea for this is a login page.  This will also give me an excuse to implement lazy loading.  Absolutely not needed for such a small app, but again this is an excuse to practice.
4. Add the ability for users and authentication, thus the login page in step 3.  Doing this will let me add the ability for users to save Intrinsify configurations that they've already tried, as well as set defaults.
5. Remove hard coded values.  Right there are two hard coded values.  The flat growth estimate, which represents a guess in the growth rate of earnings per share for that stock, which obviously is different for every business and thus should not be hard coded.  And the other is a value for current AAA corporate bond yields, which represent a "safe" alternative to investing in the stock market.  This value obviously is always changing, so I should either give the user the option to enter a value for themselves, or retrieve it somehow.
6. I learned a good method of wrapping a component around an error handler higher order component.  I'd like to implement that here as well.

I'm really looking forward to fleshing out the Intrinsify app.  I really enjoy working with React.  The whole framework really makes sense to me, and to be completely honest I've had much more fun doing front end development using React as compared to most of my previous experience, which involved straight up JS/HTML/CSS/JQuery.

I already have an idea for an app that I want to build after I'm happy with where Intrinsify stands.  I'll really flesh it out in another post, but the idea is that I want to use my back end knowledge in Django and my front end knowledge in React in one app, and really get a full stack project going.  More on that next time though.
