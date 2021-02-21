---
title: "Game engines: Eating your Dog's food"
date: 2020-07-01
---

What are game engines ? Any aspiring game developer setting out to make their own may *think* they know, but are bound to realize how fuzzy of a concept it really is. The game engine would be the part of the game that's not the game, the technical foundation on which it's based. That intuitive definition is however insufficient, as then the entire stack, down to the graphics driver and kernel scheduler would then be part of the engine. In most settings we assume game engines to hold broad responsibilities with regards to rendering the graphics and audio, gathering input, simulating the gameplay systems and handling asset management. Added to this is often a networking play layer, frameworks for user interfaces, serialization etc. 

To come out and say you're making a game engine is quite a bold thing, as you're announcing to your peers you plan on solving at least most of those problems in a somewhat comprehensive way. If you are only concerned with graphics, one would be advised to speak of "graphics engine", "physics engine" and such. Sadly we also lack a term for the stuff in-between, thus anything that covers at least two areas tend to be called a game engine nonetheless.

<!--more-->

## How to make a good engine

Some newcomers to the field get the impression that a great game engine is a prerequisite of a great game, like the ones that probably inspired them into game development to begin with. This is understandable, and it's obviously true that any technically impressive game would not be the same game if you took away the impressive tech. However where you get the impressive tech from isn't that important, and you do not usually build a game entirely out of fancy tech. ([Except when you do](https://beamng.com), of course). If you have an concrete, doable idea about a game, chances are you can make it using existing tools. If you dearly want to make games, just make games and skip engines !

Okay but perhaps you're not so interested in making games, and you are more interested in the glamorous idea of making your own engine, or maybe you got it in your head if you start with the engine the rest will just follow naturally. You might be looking for resources to start out, perhaps you already bought a book on the topic, picked up a *serious grown-up language* like C++ or you started studying the likes of design patterns or Entity-Component Systems. Surely you hope for some grand revelation in reading these kinds of articles, and actually I've got one for you !

Game engines - and for that matter any library, framework, or any other software not directly serving a end user purpose - must solve *problems*. Your amazing engine, let's call it `Unirealigine`, has to solve problems for it to be of any value to anyone, you or otherwise. Of course any piece of software will be of value for it's author as a learning project, but in the gamedev world we take the word `Engine` quite seriously, and the kicker is, if your engine is created without anything using it, it's most likely *not solving any real problems*.

Loading and drawing a bunch of 3d meshes, perhaps applying some fancy shaders and simulating physics on them is a nice accomplishment on your programming journey, something you should be genuinely proud of. It isn't however an engine. So maybe it's lacking a terrain system, so you go in, add some terrain sysem. Nope, it's still not viewed as an engine so you go in and add a game logic subsystem, complete with entities with automatic serialization. Fancy ! However, still not an engine. Screw it you say, you're going to rewrite your entire graphics to use Vulkan, a big boy's tool, to prove everyone you know what you're talking about. I'm sorry. No matter how many impressive things you keep slapping on top, it can only be an engine if it *powers*, *enables* something else, as long as nothing depends on your "engine" project, it's only ever going to be a growing collection of techniques with an increasingly suspicious code smell.

## No engine can forgo this

What is needed here, is dogfooding. Dogfooding is the process of pretending you're your own end-user, and use your software as if you didnd't make it, as a depdency in another project. By dogfooding you'll be able to assess the quality of what you're doing, realize if what you make is of any use when creating an actual game, and the more you use it the more useful feedback on what is needed will be available. Turns out that engine design is really just "framework for games" design, and just like any other type of framework, the only way to make your APIs and tools good is to use them and iterate on them until they become good. So actually making the engine by itself is a recipe for disaster: what matters is how well it serves it's purpose, and you measure that by actually going out and making *games* with your *game* engine.

Maybe you're worried about writing non-reusable code. I'm sorry (and glad) if I'm the first one to tell you, but reusable code is one of the greatest mirages programmers have been chasing since the field came about, like thinking of software as cathedrals. One does not write reusable code, one writes *deletable* code. What is meant by that, is code never comes out of the oven perfect, and the single best know way to make quality code is to ruthlessly modify it for as many times as felt necessary. Therefore the idea that you must "get it right" the first time around is downright dangerous: you will not get it right first, certainly not at the scale of an entire engine. Make things easy for yourself and don't marry yourself - or your codebase - to any specific abstractions too early, get ready to hit delete, often.

So to make an engine: if you're starting out, think of a game you would want to make using your engine, and start making it. You will create in the process both code that is only relevant to that game, and code that isn't so much. You cannot separate those yet, and it's most likely your code doesn't do so cleanly. Don't mind that and keep working, making sure every feature is actually useful. As you go and use your framework for more and more games, you will organically start to separate out bits of the codebase that aren't relevant to any particular game. This residual matter is your engine, the set of helpers and libraries and the associated APIs that help you in game making. No game engine is truly general purpose, so of course your engine will lean towards some genre, based on what it was built to serve. Game engines are nothing more than that: tools for your craft, and before you can make good tools you must know your craft.

## Opinions 😱 & Thoughts

This article was written as a reaction to another article called *Write Games, Not engines* ([mirrored here](https://geometrian.com/programming/tutorials/write-games-not-engines/)), that I saw linked somewhere on Discord. Now I spend quite a bit of time on Discord ~~not doing productive work~~ *debating* various topics, and that article, while the underlying message is something I very much subscribe to - *as showcased by this article being a thing* - I kept finding irritating things in the wording of the article, stuff that felt to me more like backhanded comments on the idea of recreational programming than helpful advice. After not so fruitful bickering, I decided hey, what the heck, let's rewrite it in a way that doesn't make those unfortunate implications. Let me know how I did !

In particular I want to make it extremely clear that I believe it is *okay* to be more interested in creating engines than games themselves. I very much belong to that demographic, and thus I cannot fully claim I have a complete engine under my belt, certainly not a commercial-grade general purpose one. I am a hobbyist, I work on my projects for fun and thus the perspective of doing un-fun work to reach some standard of quality meant for people chasing commercial or at least internet success, isn't appealing. It isn't mandatory for a hobby engine to be behind serious shipping titles, but if you're calling yourself AAA-grade, then you have to make sure AAA-grade titles can be actually made with your engine !

Having worked on Chunk Stories for 5 years, I do know a thing or two about engine design though, and exploring that space for itself is something I am very much fond of. However even exploring that space for fun and with no real ambitions of actually disrupting the space, I keep in mind dogfooding. It's something every library and framework maker must keep at heart at all times: if what you are creating is meant to solve problems, then make sure it actually does that.

## A further note

One thing the original 2007 article didn't touch on but I would very much like to point out, is how untouchable general-purpose game engines are in 2020. No small-scale operation is ever going to worry the likes of Epic Games or Unity, and so to make a place for yourself you need some differentiating features. Attempting to provide the same features as the big players and compete head-on with them, you will always be behind feature-wise and quality-wise. You just don't have the manpower!

If you want your new engine to be taken seriously and used by someone, you need to do *something* specific, and do it *very well*. For example, you can be a modern RPGMaker with incredibly friendly visual programming. Perhaps you can specialize in block games à la Minecraft (like, I [dunno](/)). You'll have probably a fairer chance if you're going to compete on the niche of engines targeting the web. Doing so is the only way I can think of to make a place for yourself, and I think, a more satisfying way to approach the challenge.