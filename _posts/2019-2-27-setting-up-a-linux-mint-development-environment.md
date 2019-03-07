---
layout: post
title: Setting up a Linux Development Environment
subtitle: Using VirtualBox to set up isolated Linux Mint development environments
show-avatar: true
social-share: false
---

I'm a software developer, and most of my programming experience has been done on a Windows (or sometimes a Mac) operating system.  This is the case for a couple of reasons.  The first is that I tend to be resistant to change.  Sometimes I get too comfortable and I don't like to try new things because why fix something if it isn't broken?  The second is that I've been working in the Microsoft world for so long that I've never really seen the point.  Windows is the natural choice if you're coding a C# application using Visual Studio.

The problem comes whenever I work with a language heavily reliant on console commands like Ruby, or Python, or Node.js.  The list goes on and on but those are the ones I've had experience with in the past.  Working with languages like those is certainly workable on any operating system but some are certainly better than others.  On Windows the experience is frustrating at best.  In general, Windows does not like it's users messing around with console commands.  I spend more time just trying to implement workarounds to get pip and venv working correctly than actually programming with python.  Mac is better - since it's built on top of a Unix foundation, the system doesn't seem to actively punish you for having the nerve to use terminal commands.  This is probably the best bet for someone who wants to use scripting languages that rely on console tools, and it's how I've gotten by for years.  But my Mac is getting old.  Little problems have been slowly accumulating on it.  It's become slow and bogged down.

The solution I'm going to try is setting up a development environment using a Linux Mint operating system installed on a VirtualBox drive.  Why Linux Mint?  I simply chose Mint because it looks a bit more approachable than Ubuntu for beginners.  Although I plan on trying Ubuntu out as well at some point.  This approach comes with a number of advantages over using one of the big operating systems, but here are the big ones for me:

1. Of course, the first advantage is that Linux _expects_ you to use terminal commands.  I'm not going to need any silly workarounds just to use pip as in Windows.
2. You can completely isolate your environment based on what you're working on.  Working on a python project?  Spin up an environment and just have the python tools that you need installed and nothing else.
3. Quick and easy to restart from scratch.  If you make a mistake in your environment and you don't know how to fix it, all you have to do is spin up a new one.  Fresh operating systems are a pleasure to work on.  No tiny little bugs accumulating over the course of years that come back to bite you.  I already save all my work in git repos, so losing work isn't a worry.  Just checkout your projects after getting the new environment up and running.
4. Career prospects.  I'm a software developer.  I don't have an excuse for not having Linux experience.  It's a desirable trait to have, and I should have done this years ago for this reason alone.

With that out of the way, here's how I set up my environment.

## Installing Linux Mint on a VirtualBox disk

The first step is download VirtualBox if you don't have it already.  This is the software we'll use to 'virtually' install an operating system, in our case Linux Mint, without doing it the traditional way on a physical drive (or even uglier, dual booting on a drive sitting alongside Windows).  You can find [VirtualBox here](https://virtualbox.org/wiki/Downloads).

After installing VirtualBox, run it and select New to create a new virtual machine.

![New VirtualBox machine](/img/2019-3-7-setting-up-a-linux-development-environment/VBoxNewDrive.PNG)

On the screen that appears, give the new VM a name that is appropriate to what it is for, and select Linux as the type.  You'll notice that under version there is no Mint option.  That is because VirtualBox does not come with it as a default option.  To remedy this, we'll have to download Linux Mint ourselves.  You can find [Linux Mint here](https://linuxmint.com/download.php).  For now, just select Ubuntu and click Next.

![Select Linux and Ubuntu](/img/2019-3-7-setting-up-a-linux-development-environment/SelectLinuxAndUbuntu.PNG)

For the next screens you'll have to make the selections that make the most sense for your machine.  Memory size is how much RAM you'll allocate to it, I selected Create a virtual hard disk now under hard disk, the hard disk file type you usually keep as VDI, and I had mine set to dynamically allocated (space is used as it's needed, instead of immediately grabbing the full amount set), and for the file loaction and size just pick what makes sense.

After creating your new drive, we need to make a few changes in the settings before we can start it.  Select the drive you just created and click settings.

Under General, click on the Advanced tab.  Here, enabled bidirectional for Shared Clipboard and Drag'n'Drop.  This enables you to share your clipboard between the host and guest systems, as well as drag and drop files between them.

![Bidirectional clipboard and drag n' drop](/img/2019-3-7-setting-up-a-linux-development-environment/BidirectionalClipboardDragnDrop.PNG)

Next, under System, click on the Processor tab.  I increased the number of CPU's my VM is using to 8 out of 16.  Not sure what kind of difference it will make, but I want the VM to be able to handle processor heavy tasks if need be.

![Increase CPU allocation](/img/2019-3-7-setting-up-a-linux-development-environment/IncreaseCPUAllocation.PNG)

Next, under the Network tab, I selected Bridged Adapter.  This setting will allow the VM to directly connect to the network that the host machine is connected to.  I thought this might be useful so I selected it instead of the default NAT.

![Network Adapter Type](/img/2019-3-7-setting-up-a-linux-development-environment/NetworkAdapterType.PNG)

Lastly, go to the Storage tab.  This is where we're going to select the Linux Mint iso that we downloaded to that our VM uses it as the operating system.  Click on the disk image next to the Optical Drive dropdown.  Select Choose Optical Disk File and browse to the iso file that you downloaded from the Linux Mint site.

![Select Linux Mint OS disk image](/img/2019-3-7-setting-up-a-linux-development-environment/SelectLinuxMintDisk.PNG)

This was the last setting we need to change.  So click Okay, and back on the home page select the VM you created and click Start.  You should eventually see your VM boot up.  You should have a shortcut on the desktop that says Install Linux Mint.  Double click it.  Most of the screens you see here depend on your situation so just pick what makes sense to you until you get to this screen:

![Erase Disk And Install Mint](/img/2019-3-7-setting-up-a-linux-development-environment/EraseDiskAndInstallMin.PNG)

You don't have to actually change anything here.  Normally this is the screen where you'd carefully choose which drive/partition that you want to install mint to.  But since this is a VM we just want to Erase disk and Install Linux Mint.  Click Install Now, choose your region, and then the installer should do its thing, which should take 5 or 10 minutes.

After it's done, it will need to restart, so do so.  After it's done you can log in and then you're using your brand new Linux Mint environment.

...After just a couple more things!

Just to make sure everything is up to date, run the following two commands in the terminal:

```shell
sudo apt-get update
sudo apt-get upgrade -y
```

After that's done (it may take view minutes), click on the Devices dropdown at the top of your screen and click "Insert Guest Additions CD image".  This will install some nice-to-haves, such as making the virtual machine scale to full screen when expanded.

And that's it!  Install VS Code or whatever you prefer, and get your code environment up and running for whatever language you're working with.  Hope this article was helpful.
