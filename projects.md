---
layout: page
title: Projects
subtitle: Stuff I've worked on
---

A short list of projects that I'm most proud of, separated by previous employers and hobby work.

## Sonoma Partners
---
Much of the work I did at Sonoma was private, and not easily shareable anyway, but I did work on some
pretty cool stuff all the same.  Here's some of the highlights:
- **Virtual Entities**:  A client I worked for wanted to implement Microsoft Dynamics in such
a way that none of their data was stored in Dynamics databases.  Instead, they wanted all of
their data to stay on their own databases, but still be able to browse and edit the data
in Dynamics.  This required some very complex backend trickery done in C#, as well as plenty
of front end customizations in javascript (since none of the data Dynamics looks for to populate
grids and fields existed in the database, all of this had to be manually retrieved using the
clients API).
- **Calendars in Kendo UI**: I implemented a couple of calendars inside Dynamics implementations
using the Kendo UI Javascript library.  The calendars acted like native pages in Dynamics, and
the users could create appointments with other Users/Contacts in the system that would automatically sync with Outlook.
- **Powershell build tool**: Many times the only way we could access the clients CRM implementation was by remoting into a server provided by them.  In this scenario the build tools that we used to deploy our code (say from the dev environment to QA, or the UAT environment to prod) would not work, since they required access to the Sonoma network.  This was a big time drain for big projects, as we would then have to do the deploys manually.  To solve this problem for a particularly large project, I wrote a script in Powershell (that could be run on any Windows machine) that would automatically build our C# code, grab the resulting DLL as well as our Javascript files and push them to the new environment, as well as migrate any database changes that had happened.  This was a huge time saver over the course of the project.

## NEXT/NOW Agency
---
### Cars.com Racing Game
{% include youtube.html id="-AOfTkTqbrk" %}
A short racing game where the user controls a car and collects powerups by leaning their body left or right.  The game was installed at a convention for Cars.com and was a big hit.  Created with the Unity3D game engine.

### John Deere Parts Quiz Game
{% include youtube.html id="1rHBbusImgM" %}
A game made for installation at a John Deere installation, the user grabs parts for a few different machines and tries to install it on the right one.  Created with the Unity3D game engine.

### Glade Glide Virtual Reality Experience
{% include youtube.html id="jRCVfgEnino" %}
User hang glides down the side of the mountain and through picturesque valleys from the perspective of an Oculus Rift.  Created with the Unity3D game engine.

### Harry Caray Basketball Game
{% include youtube.html id="FFR0GJXdBxU" %}
Basketball game installed at the Harry Caray sports museum in Chicago.  User plays as Scottie Pippen, and controls the game by making the motion of shooting a basketball with the Kinect sensor.  Featuring the real voice of Scottie Pippen.  Created with the Unity3D game engine.

### Accenture Reactive Wall
{% include youtube.html id="ffZhVnV_57I" %}
Two particle wall modes: a passive mode where pictures float by and react to users walking by in the area, and active mode where particles shoot from your hands.  Written in C++ using openFrameworks.

## Personal Projects
---
- [Intrinsify](https://github.com/heymoose/intrinsify) - A python command line tool for pulling stock data and calculating the intrinsic values.  Read more about it [on the blog post]({% post_url 2018-12-11-python-module-stock-intrinsic-value %}).
