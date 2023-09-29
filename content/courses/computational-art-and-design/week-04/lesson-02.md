---
title: "FRI | Sound"
bookCollapseSection: false
weight: 30
p5js-widget: true
---

# Week 04 | Sound, Sound Visualizations

---

## Inspiration

{{<youtube rtR63-ecUNo>}}

- [Jerobeam Fenderson](https://oscilloscopemusic.com)

## New p5js functions that we are going to need today

- [keyPressed()](https://p5js.org/reference/#/p5/keyPressed)
- [mousePressed()](https://p5js.org/reference/#/p5/mousePressed)

These functions are called ***once*** when you either press a key on your keyboard or a button on your mouse/touchpad. This is often more desired functionality compared to the [keyIsPressed](https://p5js.org/reference/#/p5/keyIsPressed) and [mouseIsPressed](https://p5js.org/reference/#/p5/mouseIsPressed) system variables that we have been using.

- [lerp()](https://p5js.org/reference/#/p5/lerp)
- [lerpColor](https://p5js.org/reference/#/p5/lerpColor)

`lerp()` is a really useful function that is used to intepolate between two values. Use it to smooth audio input values or to create laggy or smoothed movements.

`lerpColor` is similar but works with colors instead of numbers.

{{< p5js width="400" height="400">}}
let s = 10;
let targetS = 10;

function setup() {
  createCanvas(300, 300);
}

function draw() {
  background(0);
  s = lerp(s, targetS, 0.2);
  circle(width/2,height/2,s)
}

function mousePressed(){
  targetS = targetS * 2;
  if(targetS > width){
    targetS = 10;
  }
}
{{</ p5js >}}

{{< p5js width="400" height="400">}}
let c;
let targetC;

function setup() {
  createCanvas(300, 300);
  c = color(random(255), random(255), random(255));
  targetC = c;
}

function draw() {
  background(0);
  c = lerpColor(c, targetC, 0.1);
  fill(c);
  circle(width/2,height/2,100)
}

function mousePressed(){
  targetC = color(random(255), random(255), random(255));
}
{{</ p5js >}}

## Download example files

[Download the foghorn sample](/sound/foghorn.wav)

## p5js Sound Library

[Sound library reference](https://p5js.org/reference/#/libraries/p5.sound)

The p5.js sound library allows you to:
- load, play and manipulate sound files
- synthesize sounds
- use audio filters
- get audio input from microphones and other input devices
- analyze sound

In the p5.js editor, the sound library is loaded by default so you can just start using it.

## Examples

{{<hint warning>}}
There seems to be something wrong with the sound library on some browsers. Use Chrome to make sure all theses examples work.
{{</hint>}}

### Example: Play a SoundFile

Loading a sound file is very similar to loading images. It's recommended to load the file using the preload function so that it gets loaded before you do anything else in your code.

<iframe src="https://editor.p5js.org/mnstri/full/fhv6vN4z1" width="100%" height="450"></iframe>

```js
let sample;

function preload(){
  sample = loadSound("data/foghorn.wav");
}

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
}
function mousePressed(){
  sample.play();
}
```

### Example: Mic Input

{{<hint warning>}}
Note that the mic input is not working in Firefox, use Chrome or Safari for example. You also need to give your browser the permission to use the sound input when it asks for it.
{{</hint>}}

<iframe src="https://editor.p5js.org/mnstri/full/gJVPvB5ST"width="100%" height="450"></iframe>

```js
let mic;
let loudness;
let s=10;
let sTarget;

function setup() {
  createCanvas(400, 400);
  mic = new p5.AudioIn();
  mic.start();
  textAlign(CENTER);
}

function draw() {
  background(220);
  
  // get the audio level
  loudness = mic.getLevel();
  
  // map the value to something more suitable for the size
  sTarget = map(loudness,0,1,10,100);
  // use lerp to create a smooth transition
  s = lerp(s,sTarget,0.1);
  
  circle(width/2,height/2,s);
  text(loudness,width/2,20);
}

function mousePressed(){
  userStartAudio();
}
```

The ```userStartAudio``` is required since modern browsers require the user to activaly start audio playback and input with a specific action. In the p5.js examples, you will probably see it done this way:

```js
function setup(){
  let cnv = createCanvas(100, 100);
  cnv.mousePressed(userStartAudio);
  mic = new p5.AudioIn();
  mic.start();
}
```

I used the mousePressed() function since we have been talking about in the class. Both ways will work.

### Example: Advanced

The sketch below uses a folder of images. You can download this .zip file:
[Chromatrope Images](/images/examples/chromatrope.zip)

<iframe src="https://editor.p5js.org/mnstri/full/k21MpFuTt" width="100%" height="600"></iframe>

---

## Homework

Create a sketch that uses the following:

- at least one image
- video camera input
- at least one sound file
- mouse and/or keyboard interaction

Extra (add if you have the time):

- Sound reactivity

[Add your sketch to our OpenProcessing class.](https://openprocessing.org/class/86575)

{{<hint info>}}
NOTE! to make the sound library work in OpenProcessing, you should turn on the toggle for the sound library in the settings.
{{</hint>}}