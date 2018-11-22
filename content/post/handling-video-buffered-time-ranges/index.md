---
title: "Handling Video Buffered Time Ranges"
description:
  "Giving users an indication about what part of a media might be useful. But
  can developers achieve this consistently, or do browsers get in the way?"
date: 2018-11-21T10:59:29+01:00
draft: false
---

When building a web media player, one may want to let the user know what part of
the media has been loaded.

Usually, it is displayed on top of the seekbar in a slightly more contrasted
tone:

![YouTube controls bar](youtube-controls-bar.png)  
![Vimeo controls bar](vimeo-controls-bar.png)

Actually, I honestly don't know what this information is good for, but not
having it feels like kind of weird. Of course I can still use a player without
this feature, but I believe I got used to having it on popular players and
expect to have it on every other player.

One of my colleague said that this was useful to him because he knew up to which
point in the video he could seek without having to wait for data to download.

Right or wrong, I wanted to try to implement it.

Basically, binding an event listener on the HTMLMediaElement (the superclass of
HTMLVideoElement and HTMLAudioElement) `progress` event, reading the `buffered`
property of the media, and then transforming it into a readable array of objects
with a `start` and an `end` property is how I did.

Sounds simple, right?

Well, kind of, but this is the result I ended up with on Chrome:

![Exemple of missing buffered ranges on Chrome](chrome-buffered-ranges.png)

I thought that these small holes in the buffer were a consequence of a poorly
coded way to render the information, so I looked for the plain text
representation of the `buffered` property and after seeking in the media.

```js
const media = document.querySelector("video");
for (let i = 0; i < media.buffered.length; i++) {
  console.log(
    `start: ${media.buffered.start(i)}, end: ${media.buffered.end(i)}`
  );
}
```

Result:

```text
start: 0, end: 20.734
start: 28.408107, end: 32.275737
start: 32.553, end: 51.936
start: 103.483107, end: 106.277733
start: 107.302, end: 124.305
start: 163.543107, end: 166.278095
start: 167.952, end: 185.68
start: 217.597107, end: 219.131973
start: 222.174, end: 223.86
```

What I could not figure at this point is, given a seeked time, why is the media
not being buffered in a continuous fashion?  
Why are there interruptions between the small initial ranges (i.e.
`start: 103.483107, end: 106.277733`) and the following ones (i.e.
`start: 107.302, end: 124.305`)?

I then tried on both Firefox and Safari, I got different results. None of the
browsers results were similar to the others, so I thought may be assuming
browsers were doing it right **and** consistently was a bad assumption in the
first place.

What looked like a satisfying answer for this behaviour came from the
[W3C embedded content about HTMLMediaElement](https://www.w3.org/TR/html50/embedded-content-0.html#best-practices-for-implementors-of-media-elements):

> For example, when implementing the buffered attribute, how precise an
> implementation reports the ranges that have been buffered depends on how
> carefully the user agent inspects the data. Since the API reports ranges as
> times, but the data is obtained in byte streams, a user agent receiving a
> variable-bit-rate stream might only be able to determine precise times by
> actually decoding all of the data. User agents aren't required to do this,
> however; they can instead return estimates (e.g. based on the average bit rate
> seen so far) which get revised as more information becomes available.
>
> As a general rule, user agents are urged to be conservative rather than
> optimistic. For example, it would be bad to report that everything had been
> buffered when it had not.

Basically, the `buffered` attribute implementation varies from a browser to
another, and beside reading every specification or testing all the browsers, one
cannot be sure the result will be consistent.

How handy.

Since I am not sure what this buffered representation brings to the user, I may
simply drop it to ensure experience is similar across browsers.
