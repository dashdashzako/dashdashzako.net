---
title: "Web Accessibility: Give Me That Content Already"
description: "This article describes a good practice to help improve your website accessibility by adding a way to get directly to the website content"
date: 2018-01-03T09:21:02+01:00
draft: true
---

What if the waiter in a restaurant was always repeating the name of the
restaurant, its address, and the whole table of content before giving you the
description of the wine you are pointing to? That sounds pretty annoying, right?

Well, the exact same thing happens if your website doesn't provide a way to skip
all that repetitive stuff.

I can personnaly skip these elements and jump to the main content immediately. I
can also figure pretty much easily where the content is, unless a website looks
like [LINGsCARS'](https://www.lingscars.com/).

However, screen readers users will most likely rely on the shortcuts made
available to them. If no shortcut is provided, the whole page is read. And this
is why an easy way to get access to the content should be provided.  
Semantic HTML tags can be used to help screen-readers discover content more efficiently,
but we can do better.

If your website has a reasonable amount of content before the main content (no
menu at all, or a very small one), well, I think this may not really be
necessary. However, if you run a marketplace, I bet your menu is a non
neglectable part of the generated HTML page (and code).

@TODO: CDISCOUNT EXAMPLE  
@TODO: AMAZON  
@TODO: RAKUTEN

@TODO: EBAY does it the good way

@TODO: RATIO MENU/CODE

```html
<a href="#content" class="a11y-skip">Skip to content</a>

<!-- navigation with tons of links -->

<main id="content">
  <!-- the interesting content -->
</main>
```

Link should be made available as soon as possible. Just after the `body` opening
tag is a good idea.

Now let's style it a bit.

```css
.a11y-skip {
  position: absolute;
  height: 1px;
  width: 1px;
  overflow: hidden;
  clip: rect(1px, 1px, 1px, 1px);
  text-align: left;
  z-index: 1000;
}

.a11y-skip:active,
.a11y-skip:focus,
.a11y-skip:hover {
  left: 1rem;
  top: 1rem;
  width: auto;
  height: auto;
  padding: 0.5rem;
  overflow: visible;
  outline: 0;
  background-color: var(--palette-white);
  border: 0.5rem solid var(--palette-black);
}
```
