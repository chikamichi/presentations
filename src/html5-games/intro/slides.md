!SLIDE
# HTML5 Games
## Not so hard, not so new — my attempt at creating a game (engine)

!SLIDE
# A W3C workshop…

![pacman](pacman.jpg)

This presentation I ma<s><i>d</i></s>ke while attending a 4-weeks W3C workshop about HTML5 Games development (nov. 2011).

!SLIDE
# The battlefield

* DOM + CSS(3)
* `canvas`
* SVG/VML

Which one should I pick? Hum…

!SLIDE
# "Not so new"

Game design has invariants. And one knows that:

* game loops are cool
* rendering is always heavy
* a good Game Design is required to go a long way
* IO is a pain (mostly)
* games are *complete* and never perfectly designed

!SLIDE
# "Not so hard"

Tools are available. Prototypes are available. Lot of **FOSS**!

But the frameworks are **young** and feature-limited.

!SLIDE
# Before we dive in, some great engines

* [Crafty](http://craftyjs.com/)
* [Jaws](http://jawsjs.com/)
* [GameJS](http://gamejs.org/)
* [melon.js](http://www.melonjs.org/)
* [Impact](http://impactjs.com/)
* [so many more…](https://gist.github.com/768272)

This means I must code mine. Before it's too late. Wait…?

!SLIDE
# HTML5? Well…

* feature detection (Modernizr)
* `<video>`, `<audio>`
* local storage
* CSS3 for DOM manipulations

But setters, DOM repaint or worse, `innerHTML`, are slow…

!SLIDE
# & the late-guy in the party is:

`requestAnimationFrame`

> Tells the browser that you wish to perform an animation; this requests that the browser schedule a repaint of the window for the next animation frame.

[MDN](https://developer.mozilla.org/en/DOM/window.requestAnimationFrame)

~60 FPS max

!SLIDE
# `canvas`
## DOM element + 2D/WebGL JavaScript drawing API ([spec](http://www.whatwg.org/specs/web-apps/current-work/multipage/the-canvas-element.html#the-canvas-element))

* a resolution-dependent **bitmap** canvas
* direct rendering for **drawing images**
* alpha **transparency**
* **no interactions** (see spec)

=> heavy **scripting**, means freedom & trouble

!SLIDE
# W3C's workshop 1s assignment
## *Create a single element on a scene and control it using mouse or/and keyboard* — KISS:

* only 1 canvas
* not too much abstraction yet
* components bind and listen to events
* IO (keyboard) is pre-fetched
* main loop "Knows it All"

!SLIDE

demo-effect

!SLIDE
# *This slide is here so that I recall what to say:*

* `Game.MainLoop`
* `Game.Canvas` & rendering instructions
* components (should be `Game.Sprites`) & "mixins"
* events aggregator
* IO is prefetched
* main loop "Knows it All"
* missing frame rate compensation!

!SLIDE
# Errors

* (Most) MVC frameworks are **slow** (DOM rendering, code overhead…)
* You'd **better be free** to choose your code layout
* Law of Demeter (**loose coupling**)…

So I **switched from** a sexy legacy JS, *Backbone* backend **to** a lighter, *CoffeScript class*-based layout. So much nicer & simpler. Not so much optimized, but…

!SLIDE
# Optimizations

Rendering is the heavy part, long before other areas. Ideas:

* **pre-render** offscreen and `drawImage()` large chunks
* batch rendering operations
* operate color-wise
* do diff-rendering (targeted updates) — *really hard on 1 canvas*
* use **several layers** — *ease diff-rendering*
* use **integer coordinates**
* …

!SLIDE
# Useful resources

* [MDN](https://developer.mozilla.org/)
* **Studying a selection of FOSS JS game engines' APIs**
* [HTML5rocks](http://www.html5rocks.com) — *nice tutos*
* [jsPerf](http://jsperf.com/) — *so tight, dude*
* [Play my code](http://www.playmycode.com/)


