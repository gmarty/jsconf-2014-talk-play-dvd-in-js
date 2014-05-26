## Reintroducing the **web**

---

Using a **converter**

Note:
Static website generator is a hot topic.

Let's compile a DVD to a format that a browser can easily consume.

---

### Advantages

---

#### Host it yourself

* Videos take a lot of **server space**
* Static server runs on **low-end** hardware

Note:
Huge files + low traffic = You want to host your own server.

Use lighttpd, nginx... on a Raspberry Pi.

---

#### Mobile friendly

Note:
A mobile browser has already everything.

---

### Demo: *Sita Sings the Blues* DVD

A movie by Nina Paley published under

the Creative Commons <img src="img/cc-zero.svg" style="height: .8em; vertical-align: middle; margin-bottom: .5em;" alt="CC-0" title="CC-0"> license

Note:
Nina Paley is an animator and a free culture activist.

CC-0 = public domain

---

<iframe width="640" height="480" src="//www.youtube-nocookie.com/embed/CisFovxYE2Y" frameborder="0" allowfullscreen style="width: 80vw; height: 80vh;"></iframe>

---

### How?

<style>
.reveal table {
  margin: auto;
}
.reveal table th,.reveal table td {
  text-align: center;
}
td {
  white-space: nowrap;
}
</style>
<table>
    <tr class="fragment" data-fragment-index="0">
        <th>DVD feature</th>
        <th>Web platform</th>
    </tr>
    <tr>
        <td class="fragment" data-fragment-index="1">VOB files (video)</td>
        <td class="fragment" data-fragment-index="2">`<video>`</td>
    </tr>
    <tr>
        <td class="fragment" data-fragment-index="3">VOB files (subtitles)</td>
        <td class="fragment" data-fragment-index="4">`<track>` & WebVTT</td>
    </tr>
    <tr>
        <td class="fragment" data-fragment-index="5">Multi-angle and multi-audio</td>
        <td class="fragment" data-fragment-index="6">`MediaController`</td>
    </tr>
    <tr>
        <td class="fragment" data-fragment-index="7">Chapters</td>
        <td class="fragment" data-fragment-index="8">`<track kind="chapters">`</td>
    </tr>
    <tr class="fragment" data-fragment-index="5">
        <td class="fragment" data-fragment-index="9">Menu buttons</td>
        <td class="fragment" data-fragment-index="10">`<button>` & PNG</td>
    </tr>
    <tr>
        <td class="fragment" data-fragment-index="11">DVD VM</td>
        <td class="fragment" data-fragment-index="12">JavaScript</td>
    </tr>
</table>

Note:
Map DVD features to semantically equivalents web elements.

---

### DVD converter

<ol>
<li class="fragment" data-fragment-index="1">IFO files are parsed to **JSON**
<li class="fragment" data-fragment-index="2">Chapters are generated as **WebVTT**
<li class="fragment" data-fragment-index="3">NAV packets are extracted to **JSON**
<li class="fragment" data-fragment-index="4">The buttons size/position are saved to **CSS**
<li class="fragment" data-fragment-index="5">The menu still frames are saved to **PNG**
<li class="fragment" data-fragment-index="6">VM commands are compiled into **JavaScript**
<li class="fragment" data-fragment-index="7">The video is encoded to **Webm**
</ol>

---

### Playback

`<x-video>` a video player on steroids

[github.com/gmarty/x-video](https://github.com/gmarty/x-video/)

Note:
Web component

Can do chapters, playlist, menu...

---

## Lessons learned

**Browsers** can't play DVD on the fly

---

but the web platform is **powerful**

Note:
It can handle all the aspects of something as complex as a DVD-video.
 
---

JavaScript handles formats

* MP3
* PDF
* Flash
* now **DVD**!

Note:
We need more of these!

---

the web is **versatile**

Note:
Web elements can be easily recombined to create rich experience.

---

Combine web features for **complex applications**

* Video
* Audio
* Interactivity

Note:
The scope of its features is already wide.

---

the web can give a **2nd life** to old formats

Note:
like DVD.

---

### Where's the code?

<a href="https://github.com/gmarty/DVD.js">github.com/gmarty/DVD.js</a>

Note:
`converter` branch

---

### What's next?

Note:

* Still a WIP (any help is welcome).
* Optimize the playback application for mobiles and tablets.
* Ability to synchronise video locally to playback when offline.
* Play Blu-ray Discs?

---

### Bonus

<blockquote>Show me the code</blockquote>

Note:
A talk about DVD needs a DVD-like bonus!

---

<iframe src="//localhost:3000/player.html#/play/Sita%20Sings%20the%20Blues%20%28Unofficial%29" frameborder="0" allowfullscreen style="background: #808080; min-width: 50vw; height: 90vh;"></iframe>

---

<img src="img/dvd.svg" style="width: 25%;" alt="DVD" title="DVD">

### Guillaume C. Marty

<img src="img/twitter.svg" style="height: .8em; vertical-align: middle;" alt="Twitter" title="Twitter"> [@g_marty](https://twitter.com/g_marty)
<img src="img/github.svg" style="height: .8em; vertical-align: middle;" alt="Github" title="Github"> [gmarty](https://github.com/gmarty)

Note:
- All the clever guys at Mozilla London (Sole, Francisco, Mauro, Chris...)
- Thomas
