**Note:** This is a re-structured version of https://github.com/ericam/compass-animate.


SassyAnimate
===============

This is a restructured port of 
Eric Meyer's [animate.css][animate]
by [Dan Eden][dan]. This doesn't
require compass, I have pulled out some functions
from compass, and implemented them myself.


```scss
// *.scss
@import "animation-setup";
```

[animate]: http://daneden.me/animate/
[dan]: http://daneden.me/
[ca]: https://github.com/ericam/compass-animation
[c13]: http://beta.compass-style.org/reference/compass/css3/animation/

## Usage

I'll try my best to keep up to date with Dan's animation styles.

You can include any number of named animation keyframes,
each one with or without it's related class name.

The most basic option is simply:

```scss
// Include all the animations & keyframes:
@include animate;
```

But you can get much more detailed:

```scss
// Template:
@include animate[-animationName]([$sub: all, $properties: default, $class: false]);
// Example - This will pull in all the fade animations
@include animate-fade($sub: all, $properties: default, $class: false);
// _note: only groups have the $sub variable, (fade, attention, special, roll etc)_
// This will pull in only the fadeIn animation & keyframes & Overwrite the default animation properties
@include animate-fadeIn($properties: 0.2s ease-in);


```

Let's say you want just the "flash" animation:

```scss
// Include only the flash animation
@include animate-flash;
```

But you also want a pre-defined class
that calls that animation:

```scss
// Include only the flash animation keyframes,
// Use default animation properties, and also use the animation class name.
@include animate-flash($properties: default, $class: true);
```

That will output:

```css
@-moz-keyframes flash { 0% { opacity: 1; }
  25% { opacity: 0; }
  50% { opacity: 1; }
  75% { opacity: 0; }
  100% { opacity: 1; } }

@-webkit-keyframes flash { 0% { opacity: 1; }
  25% { opacity: 0; }
  50% { opacity: 1; }
  75% { opacity: 0; }
  100% { opacity: 1; } }

@-o-keyframes flash { 0% { opacity: 1; }
  25% { opacity: 0; }
  50% { opacity: 1; }
  75% { opacity: 0; }
  100% { opacity: 1; } }

@-ms-keyframes flash { 0% { opacity: 1; }
  25% { opacity: 0; }
  50% { opacity: 1; }
  75% { opacity: 0; }
  100% { opacity: 1; } }

@keyframes flash { 0% { opacity: 1; }
  25% { opacity: 0; }
  50% { opacity: 1; }
  75% { opacity: 0; }
  100% { opacity: 1; } }

.flash {
  -webkit-animation-name: flash;
     -moz-animation-name: flash;
      -ms-animation-name: flash;
       -o-animation-name: flash;
          animation-name: flash; }

.flash.animated {
  -webkit-animation-duration: 1s;
     -moz-animation-duration: 1s;
       -o-animation-duration: 1s;
      -ms-animation-duration: 1s;
          animation-duration: 1s;
  -webkit-animation-timing-function: ease-in-out;
     -moz-animation-timing-function: ease-in-out;
       -o-animation-timing-function: ease-in-out;
      -ms-animation-timing-function: ease-in-out;
          animation-timing-function: ease-in-out; }
```

Now you have the named keyframes
for the "flash" animation
and a class name that you can use in your HTML, as well as an animated class which will control the animation for the animation style.

You can also set `$class` to `true`, `false`, `nested`, `silent` or `null`

All will output the keyframes except nested, but the way the classes are setup will change.


# USING THE TRUE METHOD
_This will give you the animation name as a class, and an animated class name to control the animation._
```
.flash {
  -webkit-animation-name: flash;
     -moz-animation-name: flash;
      -ms-animation-name: flash;
       -o-animation-name: flash;
          animation-name: flash; }

.flash.animated {
  -webkit-animation-duration: 1s;
     -moz-animation-duration: 1s;
       -o-animation-duration: 1s;
      -ms-animation-duration: 1s;
          animation-duration: 1s;
  -webkit-animation-timing-function: ease-in-out;
     -moz-animation-timing-function: ease-in-out;
       -o-animation-timing-function: ease-in-out;
      -ms-animation-timing-function: ease-in-out;
          animation-timing-function: ease-in-out; }
```


# USING THE FALSE METHOD
_This will setup all animation under the animation name as a class._
```
.flash {
  -webkit-animation-name: flash;
     -moz-animation-name: flash;
       -o-animation-name: flash;
      -ms-animation-name: flash;
          animation-name: flash;
  -webkit-animation-duration: 1s;
     -moz-animation-duration: 1s;
       -o-animation-duration: 1s;
      -ms-animation-duration: 1s;
          animation-duration: 1s;
  -webkit-animation-timing-function: ease-in-out;
     -moz-animation-timing-function: ease-in-out;
       -o-animation-timing-function: ease-in-out;
      -ms-animation-timing-function: ease-in-out;
          animation-timing-function: ease-in-out;
}


```



# USING THE NESTED METHOD
_Nested will include the animation under a custom or user defined classname_
_Note: You will have to include the keyframes for this animation if you're using this method. `@include getKeyframes(fadeIn);`_

```

.fadeInCustom {
  @include animate-fadeIn(null, nested);
}

// Results >>>

.fadeInCustom {
  -webkit-animation-name: flash;
     -moz-animation-name: flash;
       -o-animation-name: flash;
      -ms-animation-name: flash;
          animation-name: flash;
}
```
# USING THE SILENT METHOD
_This will create a placeholder for us to extend the original animation_

```
@include animate-fadeIn(null, silent);
.customFadeIn { @extend %fadeIn; }
// Results >>>
.customFadeIn {
  -webkit-animation-name: fadeIn;
     -moz-animation-name: fadeIn;
       -o-animation-name: fadeIn;
      -ms-animation-name: fadeIn;
          animation-name: fadeIn;
}


```

# USING THE NULL METHOD
_This will still create a classname with the animation name and import keyframes, however it will not return any properties or a control class_

```
@include animate-fadeIn(default, null);

// Result >>>

@-webkit-keyframes fadeIn {
  0% {opacity: 0;}
  100% {opacity: 1;}
}

@-moz-keyframes fadeIn {
  0% {opacity: 0;}
  100% {opacity: 1;}
}

@-o-keyframes fadeIn {
  0% {opacity: 0;}
  100% {opacity: 1;}
}

@keyframes fadeIn {
  0% {opacity: 0;}
  100% {opacity: 1;}
}

.fadeIn {
  -webkit-animation-name: fadeIn;
     -moz-animation-name: fadeIn;
       -o-animation-name: fadeIn;
      -ms-animation-name: fadeIn;
          animation-name: fadeIn;
}


```


You can define a main class to control all your animations.

```@include animated-class($properties: 1s ease-in-out);```

This will output a control class which we can add to animation names to define when they're animated, the above outputs:

```
.animated {
  -webkit-animation-duration: 1s;
  -moz-animation-duration: 1s;
  -o-animation-duration: 1s;
  -ms-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-timing-function: ease-in-out;
  -moz-animation-timing-function: ease-in-out;
  -o-animation-timing-function: ease-in-out;
  -ms-animation-timing-function: ease-in-out;
  animation-timing-function: ease-in-out;
}
```

All mixins can have their own individual timing and duration properties set. Example:

```

@include animate-fadeIn($properties: 5s ease-in);

// >>> Result:

.fadeIn {
  -webkit-animation-name: fadeIn;
  -moz-animation-name: fadeIn;
  -o-animation-name: fadeIn;
  -ms-animation-name: fadeIn;
  animation-name: fadeIn;
}
.fadeIn.animated {
  -webkit-animation-duration: 5s;
  -moz-animation-duration: 5s;
  -o-animation-duration: 5s;
  -ms-animation-duration: 5s;
  animation-duration: 5s;
  -webkit-animation-timing-function: ease-in;
  -moz-animation-timing-function: ease-in;
  -o-animation-timing-function: ease-in;
  -ms-animation-timing-function: ease-in;
  animation-timing-function: ease-in;
}

@include animate-fadeOut($properties: 2s ease-out, $class: false);

// >>> Result:

.fadeOut {
  -webkit-animation-name: fadeOut;
  -moz-animation-name: fadeOut;
  -o-animation-name: fadeOut;
  -ms-animation-name: fadeOut;
  animation-name: fadeOut;
  -webkit-animation-duration: 2s;
  -moz-animation-duration: 2s;
  -o-animation-duration: 2s;
  -ms-animation-duration: 2s;
  animation-duration: 2s;
  -webkit-animation-timing-function: ease-out;
  -moz-animation-timing-function: ease-out;
  -o-animation-timing-function: ease-out;
  -ms-animation-timing-function: ease-out;
  animation-timing-function: ease-out;
}
```

There are a few shortcuts as well:

```scss
// this:
@include animate-fadeIn($properties: 1s ease-in-out);
@include animate-fadeOut($properties: 1s ease-in-out);
@include animate-fadeOutUpBig($properties: 1s ease-in-out);

// is equal to this:
@include animate-fade(in out outUpBig, 1s ease-in-out);
// Same principles as before, if you don't want to use the animated class, set it to false
@include animate-fade(in out outUpBig, 1s ease-in-out, false);

```

If you want all the fadeOut animations:

```scss
@include animate-fade(out);
```

## Animations

This plugin includes the following _mixins_ & animations:

**Attention**
- _attention_
- flash, bounce, shake, tada, swing, wobble, wiggle, pulse

**Flip** (currently Webkit, Firefox, & IE10 only)
- flip, _flipX_, _flipY_
- _flipIn_, flipInX, flipInY
- _flipOut_, flipOutX, flipOutY

**Fade**
- _fade_
- fadeIn, fadeInUp, fadeInDown, fadeInLeft, fadeInRight,
  fadeInUpBig, fadeInDownBig, fadeInLeftBig, fadeInRightBig
- fadeOut, fadeOutUp, fadeOutDown, fadeOutLeft, fadeOutRight,
  fadeOutUpBig, fadeOutDownBig, fadeOutLeftBig, fadeOutRightBig

**Bounce**
- _bounce_
- bounceIn, bounceInDown, bounceInUp, bounceInLeft, bounceInRight
- bounceOut, bounceOutDown, bounceOutUp, bounceOutLeft, bounceOutRight

**Roll**
- _roll_
- rollIn
- rollOut

**Rotate**
- _rotate_
- rotateIn, rotateInDownLeft, rotateInDownRight,
  rotateInUpLeft, rotateInUpRight
- rotateOut, rotateOutDownLeft, rotateOutDownRight,
  rotateOutUpLeft, rotateOutUpRight

**LightSpeed**
- _lightSpeed_
- lightSpeedIn
- lightSpeedOut

**Special**
- _special_
- hinge

**Slide**
- _slide_
- slideInDown, slideInLeft, slideInRight
- slideOutUp, slideOutLeft, slideOutRight
