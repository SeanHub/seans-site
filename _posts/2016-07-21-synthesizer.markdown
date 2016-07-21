---
layout: post
title: "JavaScript Synthesizer"
date:   2016-07-21 20:20:00 +0100
categories: javascript, music
images:

  - url: /assets/posts/synthesizer.png
    alt: JavaScript Synthesizer
    title: JavaScript Synthesizer
links:

  - url: https://en.wikipedia.org/wiki/Piano_key_frequencies
    text: https://en.wikipedia.org/wiki/Piano_key_frequencies
---
{% assign link = page.links[0] %}
{% assign image = page.images[0] %}

I have always loved synthesizers. Using window.AudioContext, I was able to create my own software synthesizer.
An oscillator is the most basic fundamental unit of a synthesizer, using the AudioContext you can create an oscillator:

{% highlight javascript %}
audioContext.createOscillator();
{% endhighlight %}

By setting its wave type and frequency you can generate any sound you can imagine. I expanded the project to support both a computer and onscreen graphical keyboard. Multiple modules were made to seperate each of the synthesizer components.

The keyboard pictured below was created using PixelMator, a click on the keys would produce a sound corresponding to piano key frequencies found here: {% include link.html link=link %}.

The calculation for converting the paino key to the oscillator frequency is as follows:

{% highlight javascript %}
var getKeyFrequency = function (key) {
    return Math.pow((Math.pow(2, 1 / 12)), (key - 49)) * 440;
}
{% endhighlight %}

A MIDI module was also added to support external keyboards. The follow code is a snippet of the core MIDI functionality:

{% highlight javascript %}
navigator.requestMIDIAccess().then(function (success) {
    midiInputDevices = success.inputs();
    midiInputDevices[0].onmidimessage = fn;
},
function (error) {
    //errorFn
});
{% endhighlight %}

Finally, slider controls were added to manually tweak each oscillators wave type and frequency. When the frequencies compliment one another, you hear an awesome polyphonic sound.

{% include image.html image=image %}