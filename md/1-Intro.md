# Playing **DVD**<br> in **JavaScript**<br> <span style="font-size: 80%;">for the sake of</span><br> **interoperability**

---

[@g_marty](https://twitter.com/g_marty)

<img src="img/French.svg" style="height: .8em; vertical-align: middle;" alt="French" title="French"> guy living in London, <img src="img/UK.svg" style="height: .8em; vertical-align: middle;" alt="UK" title="UK">

Working at <img src="img/Mozilla.svg" style="height: .8em; vertical-align: middle; margin-bottom: 25px;" alt="Mozilla" title="Mozilla"> on <img src="img/Firefox-OS.svg" style="height: 1.7em; vertical-align: middle; margin-bottom: 25px;" alt="Firefox OS" title="Firefox OS">

Note:
This talk is about a side project and is not related in any way to Mozilla.

---

## I have DVDs

<img src="img/dvd-collection.jpg" style="width: 50%;" alt="My DVD collection" title="My DVD collection">

Note:
This is a picture of my DVD collection, mostly made of Japanese animation DVD.

---

I use Google Play Music

<img src="img/google-play-music.png" style="width: 50%;" alt="Google Play Music logo" title="Google Play Music logo">

Note:
I noticed that I listen to my CD more often since I'm using Play Music.

I encoded my CD collection.

Now I want to do the same with my DVD.

---

I love JavaScript

<img src="img/JavaScript.svg" style="width: 50%;" alt="JavaScript logo" title="JavaScript logo">

---

I want **Google Play Music** for **DVDs**

<div class="fragment" data-fragment-index="1">
<p>A service that streams my DVDs</p>

<ul>
<li>from the cloud
<li>to my (mobile) browser
</ul>
</div>

Note:
So I tried to combine DVD and JavaScript.

---

### But why?!!!1!1!ONE

<blockquote class="fragment" data-fragment-index="1">Q: Y U NO Netflix?</blockquote>

<!-- .element: class="fragment" data-fragment-index="2" -->
A: Not interesting for me.

<blockquote class="fragment" data-fragment-index="3">Q: Y U NO rip the video?</blockquote>

<!-- .element: class="fragment" data-fragment-index="4" -->
A: DVDs are more than just video.

Note:
Legal offer is too mainstream.
I don't want to pay to see a movie I already own.

A DVD is made of one or more video and audio tracks. There are menus, interactivity.
It can be used to make games, karaoke, quizzes...
I want that in my browser.

---

I implemented this in **JavaScript**

but faced **problems**

Note:
This talk is about how I implemented this service.

Before explaining you how, let's see the multiple issues I faced and the many experimentations I tried.

---

## The structure

DVD = Digital *Versatile* Disc

Note:
(aka the boring details)
The V DVD does not stand for video.
DVD-video is just one possible application.
Let's examine the structure of a DVD-video disc now.

---

### The DVD specs...

... is a paying document,

but was *reverse engineered* from discs

Note:
The specs requires signing a NDA.
Open source libraries libdvdread and libdvdnav.

---

### Files organisation

2 folders:

* AUDIO_TS/ (optional)
* VIDEO_TS/

Note:
AUDIO_TS is optional.

Let's consider VIDEO_TS.

---

### File types

* Info files (`*.IFO`, `*.BUP`)
* Video files (`*.VOB`)

---

### IFO files

* Playback logic
* Chapters
* Languages available

Note:
BUP files are backup files located elsewhere on the disc for the sake of data redundancy to make the format compliant to scratches.

The DVD specs are a bit old and there is a lot of data redundancy in the format.

---

### VOB files

* Video / Audio
* Subtitles
* Menu UI

Note:
Menu files also contain the data related to the UI.

---

### DVD Virtual Machine

<ul>
<li class="fragment" data-fragment-index="1">16 general parameter registers (≈ variables)
<li class="fragment" data-fragment-index="2">24 system parameter registers (language, region...)
<li class="fragment" data-fragment-index="3">36 commands (jump, compare, set, goto...)
</ul>

Note:

* System parameters: active button, parental level...
* Commands: Link, Jump, GoTo, Compare (==, >, <...), SetSystem (6 settable system params), SetGPRM (+=, rnd, Or...).

---

#### Example of command

<pre class="fragment" data-fragment-index="1"><code class="undefined">30 25 00 0A 00 03 01 02</code></pre>

<pre class="fragment" data-fragment-index="2"><code class="undefined">If (GPRM1 == GPRM2)
  JumpVTS_PTT (PTT:10, VTS:3)</code></pre>

<table style="margin: 15px auto;">
  <tr>
    <td class="fragment" data-fragment-index="3">`30 25 00`</td>
    <td class="fragment" data-fragment-index="4">`0A`</td>
    <td class="fragment" data-fragment-index="5">`00`</td>
    <td class="fragment" data-fragment-index="6">`03`</td>
    <td class="fragment" data-fragment-index="7">`01`</td>
    <td class="fragment" data-fragment-index="8">`02`</td>
  </tr>
  <tr>
    <td class="fragment" data-fragment-index="3">JumpVTS_PTT </td>
    <td class="fragment" data-fragment-index="4">10 (PTT)</td>
    <td class="fragment" data-fragment-index="5">==</td>
    <td class="fragment" data-fragment-index="6">3 (VTS)</td>
    <td class="fragment" data-fragment-index="7">1 (GPRM1)</td>
    <td class="fragment" data-fragment-index="8">2 (GPRM2)</td>
  </tr>
</table>

<pre class="fragment" data-fragment-index="9"><code class="javascript">if (gprm[1] === gprm[2]) {
  dvd.playTitle(3);
  dvd.playChapter(10);
}</code></pre>

Note:
1 command = 8 bytes of binary data.

JumpVTS_PTT = Jump to a chapter in the specified title.
Here, chapter 10 of title 3.
