---
title: "Accessibility: Give Me That Content Already"
description: ""
date: 2018-01-03T09:21:02+01:00
draft: true
---

```html
<a href="#content" class="a11y-skip">Skip to content</a>

<!-- some boring navigation with tons of links -->

<main id="content">
  <!-- the content -->
</main>
```

Link should be made available as soon as possible. Just after the `body` opening tag is a good idea.

Now let's style it a bit.

```css
.a11y-skip {
  position: absolute;
  top: -1000px;
  left: -1000px;
  height: 1px;
  width: 1px;
  text-align: left;
  overflow: hidden;
}

.a11y-skip:active,
.a11y-skip:focus,
.a11y-skip:hover {
  left: 1rem;
  top: 1rem;
  width: auto;
  height: auto;
  padding: .5rem;
  overflow: visible;
  outline: 0;
  background-color: var(--palette-white);
  border: .5rem solid var(--palette-black);
}
```
