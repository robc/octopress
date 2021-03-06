---
layout: post
title: "A Game For Ludum Dare 26"
date: 2013-04-29 20:42
comments: true
categories: [Prototypes, Ludum Dare]
---
With the 26th Ludum Dare just past (at least the *compo* part of the competition), I thought I'd write a little bit of a post-script about the development of my game **Onslaught In Space**.

![Onslaught In Space Gameplay Screen]({{ root_url }}/images/OnslaughtInSpace.png)

If you've not already seen it, the game is available [here](http://www.ludumdare.com/compo/ludum-dare-26/?action=preview&uid=15363) to play. If you have an account with the Ludum Dare site, I'd love if you could also vote &amp; post some feedback. Otherwise, enjoy it :)

<!-- More -->

When the theme of **Minimalism** was originally announced - my original thoughts drifted towards something in the vein of an arcade game. The original project was an attempt at doing something along the lines of a weird slalom game. Of course, as can sometimes happen in a Jam, I found the original implementation was rather poor as of the end of Saturday.

That led to me nuking the project come Sunday morning, and thinking up something else. Within that limitation, I shifted the focus towards a minimalistic arcade game.

### Inspirations ###
In doing a minimal arcade game, the primary inspiration is games from the late 70s, and early 80s - primarily using Vector Hardware. I think in terms of tone, Atari's own Asteroids was the best for this (on a number of levels in particular) - but only for the tone.

Gameplay wise, part of it was from the old game [Paratrooper](http://www.youtube.com/watch?v=SnPUsspS-LM) as well as a smaller concept I tried to prototype years ago.

### Graphics &amp; Audio ###
With that in mind, and my own capabilities on the line - I decided to use my rather minimal 3D modelling experience and use meshses for everything rather than sprites. For me, that means I get to crank up [Cheetah 3D](http://www.cheetah3d.com) - which is a great modeller for OS X, despite missing that *one* feature (in my case, vertex colouring). But, the resultant meshes were built in about an hour's work.

As for Audio, the majority was generated by [CFXR](http://thirdcog.eu/apps/cfxr) - an OS X specific conversion of [SXFR](http://www.drpetter.se/project_sfxr.html), which better fits within the OS X environment. Whilst there are other variants, I still prefer this just for the ease of generating audio. Most of the sound effects were taken straight from a few presents, although the general drone *hum* was two tweaked versions of the one sound joined together.

The *music* (well, it's incredibly short - so I'm unsure if it's worth being called that) was quickly thrown togther inside [Propellerheads'](http://www.propellerheads.se) [Figure](https://itunes.apple.com/au/app/figure/id511269223?mt=8) - a great little iOS application for quick sketches of music. I wish I'd chosen to spend a bit more time there, as I'd have loved an excuse to play around with things a bit more - but I guess as it happens, it falls apart at the end of a project.

Generally, I'm happy with both the visuals &amp; audio - in particular, the enemy droning - I originally intended for something similar to the background of Asteroids, but the combination of the sound being played over so many enemies, at such offset patterns really helps build an imposing atmosphere. I'm certainly interested in seeing what others happen to think about that as the ratings &amp; reviews post LD happen to come in :)

### Code &amp; Architecture ###

The majority of the time taken was working on the Unity side of things. Under the limitations of LD, I had to forego most of the common tools I tend to work with in Unity (primarily [NGUI](http://www.tasharen.com) and [HOTween](http://www.holoville.com/hotween/)), which moved the interface towards the spartan side of things - but totally appropriate.

I'm actually rather happy with how the code turned out - compared to some of the other prototypes I've played with, let along the codebase for [Pocket Dogfights](http://www.pocketdogfights.com), it's an incredibly compact one.

The logic was primarily split up between 3 main areas:

#### Managing the Game Loop ####
Here I employed a rather basic state machine to handle the basic tasks such as checking for Input, updating the Player, triggering waves to spawn, along with controlling what parts of the UI are shown.

#### Controlling Entities ####
Here, there are scripts for managing the player's rotation, firing, and enemy management.

The most interesting would be the enemy management - this takes a trigger to start spawning, then calculates randomised spawn locations, and velocities - leaving the actual movement up to the physics engine. It also handles callbacks when enemies either reach the player (thus ending the game), or have been shot - those are used for cleaning up resources, and also to fire additional callbacks to the Game Loop.

The one thing I would probably change if I were going to take this codebase further would be to add proper lifecycle management. At the moment, for the sake of speed, I don't cache or pool any of the entities in game (although this doesn't apply to the player). For a weekend proof of concept it's a satisfactory course of action, but in production you would want this to manage this to ensure that you don't get slow downs related to object creation & destruction, along with more efficient use of memory.

#### Interface Management ####
Without having a real UI system present, I decided to go down the path of displaying everything with text labels (via Unity's in-built TextMesh class). It also meant I didn't need to manually build out a font atlas, so tweaking sizes was incredibly easy.

The only state which is maintained is just the active/inactive states on the individual labels - this meant I could provide a few basic calls which would set the state of all labels as required - which centered around the *Title Screen*, *In Game*, *Game Over* and *Game Complete* screens. These are also all called from the Game Loop during the appropriate state transitions.

Although I didn't have any tools to assist in layout (other than the editor), this actually turns out to be a great way to prototype things. Performance wise, there weren't any additional draw calls, and despite all that labels present, the amount of polygons being rendered by the game wasn't that much higher.

I would probably keep this in future. However, the big question I do wonder about - is how well this does (or doesn't) work for mobile platforms. Whilst my prototyping tends to be on the Desktop (or Web Player), there are still times when I want to be able to put a Prototype on an iOS device and get feedback out in the wild.

### Conclusions ###
I had fun working on this one - despite the very limited nature of the gameplay, I find it a great little piece of challenge. Plus, some of the feedback post release has been great to read.

Unlike some of the other ideas I have worked on, I'm actually tempted to sit back with this one &amp; see what I can do in bringing it to a wider audience. I'm unsure what the best platform for this is at the moment, but it'll be a case of some redesigning, and obviously a lot more complexity to go in.

Finally, as per the spirit of Ludum Dare, I've got the source available online at [Github](https://github.com/robc/OnslaughtInSpace) - even if you don't use Unity yourself, you might find some of the code somewhat of interest to look at.

In addition, if you enjoyed this - your should totally check out [Pocket Dogfights](http://www.pocketdogfights.com) (if you've not already) - it takes a lot of the sensibilities which I've talked about here and expands on them quite a bit.