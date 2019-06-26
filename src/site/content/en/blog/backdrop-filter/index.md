---
title: "CSS backdrop-filter"
subhead: |
  Enabled in Chrome 76
date: 2019-06-25
authors:
  - adamargyle
hero: hero.jpeg
alt: Women behind frosted glass
description: |
  CSS backdrop-filter was made famous by Apple's design team. It brings
  the ability for a background to apply a filter to the contents beneath.
  Creates a nice layering effect that keeps beneath elements in context.
tags:
  - post
  - CSS
  - backdrop-filter
---

Designers and developers alike can celebrate as a long awaited CSS feature [releases in Chrome 76](https://www.chromestatus.com/feature/5679432723333120): backdrop-filter. Frosted glass effects, video overlays, translucent navigation headers, inappropriate image censoring, image loading, and more, no longer require [hacks or workarounds](https://stackoverflow.com/questions/38145368/css-workaround-to-backdrop-filter).

You may recognize the effect from two popular operating systems: [Windows Vista](https://i.kinja-img.com/gawker-media/image/upload/s--9RLXARU4--/c_scale,dpr_2.0,f_auto,fl_progressive,q_80,w_800/trgz8yivyyqrpcnwscu5.png) and [iOS](https://static.businessinsider.com/image/51fd2822eab8eae16e00000b-750.jpg). Now [Chrome](https://www.chromestatus.com/feature/5679432723333120) can do it too.

The following video demonstrates `backdrop-filter` and each individual filter:

<figure class="w-figure w-figure--fullbleed">
  <video controls autoplay loop muted class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/backdrop-filter/backdrop_filter-kitchen_sink.mp4" type="video/mp4">
  </video>
  <figcaption class="w-figcaption w-figcaption--fullbleed">
    <a href="https://codepen.io/robinrendle/pen/LmzLEL" target="_blank">CodePen</a>
  </figcaption>
</figure>


## Technical Details
{% Aside 'key-term' %}
  backdrop refers to all painted content behind the element, except when the ancestor has filters, opacity or [a few other documented properties applied](https://drafts.fxtf.org/filter-effects-2/#BackdropRootTriggers).
{% endAside %}

CSS `backdrop-filter` applies one or more filters to the backdrop of an element, leaving the contents unchanged.

In order for the filter to apply any augmentations, some portion of the overlaying element needs to be transparent. Alternatively, consider that opaque elements will not produce a backdrop-filter effect while fully transparent elements produce a full filtered backdrop.

Backdrop-filter shares attributes with CSS filters in that they create a new [stacking context](https://www.w3.org/TR/CSS21/zindex.html) and/or [containing blocks](https://developer.mozilla.org/en-US/docs/Web/CSS/Containing_block) when the property is used properly, aka it's not 'none'. Note, only elements with absolute and fixed position decendants will get a containing block.

### Summary
1. Overlaying element OR it's background must be at least partially transparent
1. Overlaying element will get a new stacking context
1. Filters may be combined

{% Aside 'warning' %}
  The backdrop-filter feature is computationally intensive, as are filters in general, so it may impact the performance of sites using it.
{% endAside %}


## Using backdrop-filter
Get started in one line of CSS.

### Single Filter

```css
.blur-behind-me {
  backdrop-filter: blur(.5rem);
}
```

<figure class="w-figure">
  <video controls autoplay loop muted class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/backdrop-filter/backdrop_filter-rgb.mp4" type="video/mp4">
  </video>
  <figcaption class="w-figcaption">
    <a href="https://codepen.io/netsi1964/pen/JqBLPK" target="_blank">CodePen</a>
  </figcaption>
</figure>

### Combining Filters

```css
.brighten-saturate-and-blur-behind-me {
  backdrop-filter: brightness(150%) saturate(150%) blur(1rem);
}
```

<figure class="w-figure">
  <video controls autoplay loop muted class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/backdrop-filter/backdrop_filter-ambient_blur.mp4" type="video/mp4">
  </video>
  <figcaption class="w-figcaption">
    <a href="https://codepen.io/pepf/pen/GqZkdj" target="_blank">CodePen</a>
  </figcaption>
</figure>

### iOS Frosted Notifications

```css
.frost {
  backdrop-filter: blur(.25rem);
}
```

<figure class="w-figure">
  <video controls autoplay loop muted class="w-screenshot">
    <source src="https://storage.googleapis.com/web-dev-assets/backdrop-filter/backdrop_filter-ios_notifications.mp4" type="video/mp4">
  </video>
  <figcaption class="w-figcaption">
    <a href="https://s.codepen.io/robinrendle/pen/ZoXGgG" target="_blank">CodePen</a>
  </figcaption>
</figure>


## Conclusion
Better late than never! Safari's had this feature since 2015. Regardless, Chrome's excited to release it in 76. The [Chromium bug](https://crbug.com/497522) has **560+ stars** on it, clearly marking it as a desired web design capability.

Here's a final CSS API list and additional resources in case you're ready to start developing.

### Overview
```css
/* Keyword value */
backdrop-filter: none;

/* URL to SVG filter */
backdrop-filter: url(commonfilters.svg#filter);

/* <filter-function> values */
backdrop-filter: blur(2px);
backdrop-filter: brightness(60%);
backdrop-filter: contrast(40%);
backdrop-filter: drop-shadow(4px 4px 10px blue);
backdrop-filter: grayscale(30%);
backdrop-filter: hue-rotate(120deg);
backdrop-filter: invert(70%);
backdrop-filter: opacity(20%);
backdrop-filter: sepia(90%);
backdrop-filter: saturate(80%);

/* Multiple filters */
backdrop-filter: url(filters.svg#filter) blur(4px) saturate(150%);

/* Global values */
backdrop-filter: inherit;
backdrop-filter: initial;
backdrop-filter: unset;
```

### One more demo
A glimpse into the now possible in Chrome:

<figure class="w-figure w-figure--fullbleed">
  {% YouTube 'MWHBpReeAJ0' %}
  <figcaption class="w-figcaption">
    Demo by <a href="https://ferdychristant.com/please-help-make-backdrop-filter-a-reality-f81805ba3d52" target="_blank">Ferdy Christant</a>
  </figcaption>
</figure>

### Additional Resources
- [Specification](https://drafts.fxtf.org/filter-effects-2/#BackdropFilterProperty)
- [Proposal](https://github.com/w3ctag/design-reviews/issues/353)
- [GitHub](https://github.com/mfreed7/backdrop-filter-feature)
- [Chrome Platform Status](https://www.chromestatus.com/feature/5679432723333120)
- [Caniuse](http://caniuse.com/#feat=css-backdrop-filter)
- [API](https://developer.mozilla.org/en-US/docs/Web/CSS/backdrop-filter)
- [CSS Tricks](https://css-tricks.com/the-backdrop-filter-css-property/)
- [Codepens](https://codepen.io/tag/backdrop-filter/#)