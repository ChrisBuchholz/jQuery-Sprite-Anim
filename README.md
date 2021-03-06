# jQuery Sprite Anim
#### Version 0.1a

## Current state:

__Alpha Warning__: *We currently discourage any use of this plugin in production projects, as the state is currently alpha-quality! Some of the claims below, may not be true.*

## Introduction

jQuery Sprite Anim is intended to be a simple sprite animation library. There are already numerous excellent sprite animation libraries available for jQuery. This library differs in a couple of ways, from any of the others we've been able to find:

 * A freely available generator, optimized for this library, has been created.
 * Support for an unlimited number of frames.
 * Creates multiple sprite sheets, to work around size limitations in mobile browsers and some desktop browsers.

 
## Browser support

The library should work well in most modern browsers:

 * Internet Explorer 6+
 * Firefox 1+
 * Google Chrome
 
###### Notes:

 1. Enabling retina currently requires a browser with [background-size](http://caniuse.com/background-img-opts) support.


## License

The MIT License. See LICENSE for further information.


## Generating sprites

### Easy: Use our tool

You may use the webbased generator freely available at <http://sprite.smplr.com>. You can simply upload your images and have the tool generate the sprites for you.


### Hard: Do It Yourself

The images must be laid out in sprite sheets, with the first image in the top left corner, the next image right next to it. Once there's no more room in a row, start a new one. There must be no margin between images and all images must have the same size.

The sprite sheets must be saved with a digit, before the extension.


## Getting started

Please see the demo/-folder for a clear example of how to use the library.


## Data attributes

You should simply create a `<div>` with the following data-attributes to get started:

Attribute    | Required | Default value  | Description
:----------- | :------- | :------------- | :-------------------------
data-baseurl | **Yes**  |                | URL to the sprite. Exclude the digit and extension. Example: http://site.com/sprite. Then http://site.com/sprite0.png, http://site.com/sprite1.png etc. will be found automatically.
data-grid    | **Yes**  |                | Example 4x2 means 4 images per row and two rows per sheet.
data-blocksize | **Yes** |               | The size of the images. Example 500x200 means each image in the sprite is 500px width and 200px in height.
data-frames  | **Yes**  |                | How many images does this sprite animation consist of?
data-fps     | No       | 12             | Frames per second.
data-autoplay | No      | true           | Animation will play as soon as initialized and first image is loaded.
data-autoload | No      | true           | As soon as initialized, the first two sheets will be loaded.
data-retina  | No       | false          | Uses background-size and resizes the element, to half size.

Example:

    <div id='mySpriteAnimation'
      data-baseurl='sprite'
      data-grid='4x2'
      data-blocksize='100x50'
      data-frames='123'
      data-fps='12'
      data-autoplay='true'
      data-autoload='true'
      data-retina='false'
    ></div>

Then to initialize, call $.spriteanim() on the DOM element, like so:

    $('#mySpriteAnimation').spriteanim();


## Javascript API

You may call $.spriteanim with one or two arguments. The first is the `action` and the second may contain any additional arguments.

### play

Start playing the animation. Takes no arguments.

### stop

Stop playing the animation. Takes no arguments.

### fps

Changes the framerate. You must supply a second argument with the intended FPS.

If the animation is playing:
 * The animation will continue playing at the new FPS.

If the animation is not playing:
 * The animation will remain stopped.

Example:

    $('#mySpriteAnimation').spriteanim('fps', 24); // change the framerate to 24

## Javascript Events

Various events are dispatched and can be used to finetune the animation as you please.

Implementation is through the standard jQuery Events on the element.

Some events can be cancelled by calling preventDefault() on the event-object, which is always given as the first argument.

Example:

    // stop the animation the next time it is supposed to start playing
    $('#mySpriteAniamtion').one('play', function(ev) { ev.preventDefault(); })

### play

Called everytime the animation is set to start playing. This is not called when FPS is changed.

**Cancelable?** Yes.


### frame-`X`-show

Replace `X` with a frame number, 0-indexed. Called just before changing to the frame.

`X` may also be one of the following special keywords:

 * last: Called on the last frame of the animation.

**Cancelable?** Yes. Note: This also stops the animation.


### frame-`X`-shown

Replace `X` with a frame number, 0-indexed. Called just *after* changing to the frame.

`X` may also be one of the same special keywords from above.

**Cancelable?** No.


### sheet-loaded

A sprite sheet has been loaded. Please note: This may be triggered a lot, as loading occurs each time we change sprite sheet.

**Cancelable?** No.


### sheet-`X`-loaded

Replace `X` with a sheet number, 0-indexed. A specific sprite sheet has been loaded.

Please note: This may be triggered a lot, as loading occurs each time we change sprite sheet.

**Cancelable?** No.


## Feature wishlist

 * Currently the library only supports PNG sprites. Should support most common web image formats.
 * Support for reversing playback.
 * Support for programmatically skipping to a specific frame.
 * Support other high-resolution resolutions, instead of just "retina" (2x).
 * Background-size polyfill for older browsers.