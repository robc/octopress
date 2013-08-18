---
layout: post
title: "Let's Talk Gamepads"
date: 2013-08-02 10:36
comments: true
categories: [Pocket Dogfights, Indie Dev Life, Waffle]
---
Though it's been slightly unplanned, I'm currently in the midst of a fairly comprehensive overhaul of how controllers are implemented within [Pocket Dogfights](http://www.pocketdogfights.com).

In some regard, it's not a surprised I've had to do this - the interface Unity abstracts is rather limited in a number of areas, the biggest being that it's not possible to redefine a control once in game. In addition, the amount of variation between how buttons are defined between platforms, between controller types (even the same controller on different platforms), means that there's a lot of complexity you need to manage.

Plus, when I originally added support for them in the desktop versions, I went for a path which was fairly limiting. In the end, especially with the recent launch of the standalone [Windows/Linux](http://gum.co/pocketdogfights) versions, I felt that this had to be done.

<!-- more -->

The other thing which convinced me it was necessary, was none other than this little surprise when testing my MOGA Pro controller with the game on my Nexus 7!

<iframe class="vine-embed" src="https://vine.co/v/hKUhMZ3hQ5Q/embed/simple" width="320" height="320" frameborder="0" style="display: block; margin: 0 auto; padding-bottom: 1em"></iframe><script async src="//platform.vine.co/static/scripts/embed.js" charset="utf-8"></script>

The result? Something had to be done, especially, if like me, you wish to give the players of your game a smoother experience on start-up, without the need to reconfigure controls before diving into the action. Again, this adds a little more complexity when you factor in the number of platforms the game is out on (iOS, Android, Windows, OS X &amp; Linux) - but after way too much pondering &amp; throwing things out the window, I think I have a solution.

The first phase was to adopt the [cInput](http://cinput2.weebly.com) library. This is a (relatively) cheap input wrapper allowing for controls to be remapped in-game (and they provide their own UI to do it as well - at least for Unity's in-built system). It also handles a few other tasks nicely as well.

Next, it's a case of creating a layer which abstracts controllers - this lets me create interfaces for the common ones I plan to support, being the Xbox 360 controller, PS3 controller, plus a *generic* controller (which can then be remapped by the player).

This, combined with some smarts in detection at start-up, should be enough for a solution which does what I need.

The question now - is what does this mean for you reading this (and hopefully playing the game)? Easy - as it stands right now, the *default* control setups are planned as follows:

### Windows
*  The planned default will be the **Xbox 360** gamepad (in both wired &amp; wireless form). In theory, any *blessed* third-party controller should work as well (thanks to XInput), but I'll need testing to verify.
*  If you don't have one of those, then you'll of course be able to use the custom mode &amp; remap controls as required.

### Mac OS X
*  The supported defaults will be the **Xbox 360** gamepad (again, in both wired &amp; wireless form thanks to [Colin's driver](http://tattiebogle.net/index.php/ProjectRoot/Xbox360Controller/OsxDriver)), and the Playstation 3's gamepad.
*  Again, if you don't have one of those, you will be able to manually assign buttons to any USB game pad.
*  Once OS X 10.9 (Mavericks) is released, I plan to investigate what it'll take to support the new MFI controllers as well.

### Linux
*  By default, you will need to manually bind - at this stage, there's not enough info in place to cover what is/isn't supported here, so it's best to be able to configure your controller in-game.

### iOS
*  For now, the default is going to be the iCade *standard*. I'm most certainly interested in hearing what types of compatible devices people are in fact using - as while I feel I have a good configuration, I'd certainly like to make sure with what people have out in the *field*.
*  Once iOS 7 is out, I'll evaluate the new Controllers API and try to get that in a later update (as with OS X).

### Android
*  For Android, the default options will be the [MOGA Pocket/Pro](http://www.mogaanywhere.com) controllers, along with supporting PS3 &amp; Xbox 360 game pads.
*  Again, if you've got a different USB gamepad, you'll be able to go &amp; customise the buttons as required.
*  As for other gamepads - if there's one which has enough of an audience, then I can see about what it'll take to support it.

That's the short-term plan for solving this little quagmire. However, I'm after input - if you're running any of these platforms, and what I'm proposing is **not** what you'd prefer, please do let me know. I'm at the stage where it's still a WIP, so I can adjust things as they go.