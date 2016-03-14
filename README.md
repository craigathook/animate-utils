# Alo - Adobe Animate CreateJS Export Loader

Alo helps with loading exported CreateJS from Adobe Animate and Adobe Flash. It also makes it possible to load multiple Animate/Flash animations on screen at the same time, with completely separate canvas elements.

# Usage

Alo requires the animations be exported as 'index.js', and be contained in their own folder. This helps keep image and other assets from conflicting between animations. For example, a bird animation containing a bird animation should be structured like this:

    /bird/images/bird.png - image used in animation
    /bird/index.fla - source animate/flash file
    /bird/index.js - exported CreateJS code

From here you would load the your animation like this:

    alo.load('/bird', '#birdContainer', function(stage){ stage.root.gotoAndPlay('flap') });

# Alo Module

Alo Modules are just javascript Functions/Classes with some very basic additional suggested structure. Alo Modules are instanciated _before_ the stage has rendered. This is _before_ code on the timeline has ran. So it's safe to add features animators can use on the timeline, such as triggering particle effects. Here's an example of the most basic Alo Module:

    function BirdModule(stage) {

      var root = stage.root; // root of the display list. same as "scene 1".
      var lib = stage.lib; // reference to the library of MovieClips for this animation

      root.hitSquare.addEventListener('click', function() { // referencing the hitSquare movieclip in our animation stage, adding a click event listener.
        root.gotoAndPlay('flap');
      });
    }

From here you would load the your animation like this:

    alo.module.load('/bird', '#birdContainer', BirdModule, {
      onLoaded: onLoadComplete,
      transparent: true
    });

# Methods

Alo has these methods and classes:

**alo.module.load** ( animationUrl, targetElement, module, [options] )
 > Instantiates a module with a reference to the stage Container of the given animation's display list. The module is instantiated BEFORE any frame is rendered, so methods in this module can be accessible on the animation's timeline.


**alo.load** ( animationUrl, targetElement, callback, [options] ) _Container_
 > Loads the given animation with a callback that returns the stage Container of the given animation's display list.

# Requirements

From the CreateJS suite: 
 * EaselJS
 * TweenJS
 * PreloadJS