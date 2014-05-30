## Playing DVD<br> **on the fly**

---

* libdvdread
* libdvdnav

Note:
I ported these C libs to JavaScript manually.

---

### Experiment 1

* The browser reads the disc directly

---

Direct disc reading

<img src="img/architecture-0.svg" style="width: 50%;" alt="Reading DVD directly from the browser" title="Reading DVD directly from the browser">

---

#### Parsing IFO files

* Typed arrays
* DataView

Note:
That's easy!

---

#### Playing VOB files

Problems occur

---

#### Browsers can't play the codecs

* Mpeg 2
* AAC

Note:
Someone should convert a decoder to JavaScript using Emscripten.

---

#### Browsers can't handle huge files

VOB files can be as big as **1 Gb**

Note:
This may be solved by Streams in the future.

---

### Experiment 2

* Encode video on demand

Note:
Using a server written in Node.js.

Communicate with the browser via binary WebSockets.

---

Server in Node.js

<img src="img/architecture-1.svg" style="width: 50%;" alt="A server in Node.js encodes the video" title="A server in Node.js encodes the video">

---

#### That doesn't work

Playback is jerky

Note:
Encoding takes more time than reading.
Video can't be encoded bits per bits.

---

### Experiment 3

* Encode video beforehand to webm

Note:
Preencode the video.

---

Preencoded video

<img src="img/architecture-2.svg" style="width: 50%;" alt="A server in Node.js use preencoded video" title="A server in Node.js use preencoded video">

---

This kind of works, but...

---

* Server / client out of sync
* Needs a powerful configuration

Note:
The server is well ahead of the client.

Needs:

* Modern browser with experimental flags activated
* Powerful CPU client
* Powerful CPU server

This is a fragile implementation.

No mobile support

It needs to reimplement things already in the browser (video buffering...)

---

### But most of all

this isn't the **web**

Note:
= reimplementing image decoder on canvas.
