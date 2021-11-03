---
title: "How to use Percy-specific CSS"
subtitle: "and not ship it in your build"
date: 2021-11-02T18:40:19-04:00
lastmod: 2021-11-02T18:40:19-04:00
draft: false
authorLink: ""
description: "How to use Percy-specific CSS and not ship it in your build"

tags: ["css", "cypress", "percy", "javascript", "visual diffing"]
categories: ["Web Dev"]

hiddenFromHomePage: false
hiddenFromSearch: false

featuredImage: "blog-header@2x.png"
featuredImagePreview: "blog-header@2x.png"

toc:
  enable: false
math:
  enable: false
lightgallery: false
license: ""
---

Percy snapshots can be kind of flaky sometimes. Animations, unpredictable popup locations, and more can cause Percy to snapshot an incorrect DOM state.

<!--more-->

You also might need to do a bit of tweaking to get Percy to capture a full-page screenshot correctly instead of just the vertically-limited viewport of Cypress or whatever you're using to capture your Percy snapshots.

## Percy media queries

There are [multiple ways to get CSS to apply to just Percy snapshots](https://docs.percy.io/docs/percy-specific-css).

My favorite are [Percy media queries](https://docs.percy.io/docs/percy-specific-css#percy-css-media-query), since you can write them just like you write other CSS.

```css
@media only percy {
  // insert your CSS here
}
```

### Examples

Hiding an element entirely:

```css
@media only percy {
  #element-a {
    visibility: hidden;
    display: none;
  }
}
```

Hiding an element entirely and replacing it with some text so you'll know why it isn't showing in the snapshot:

```css
@media only percy {
  .element-b {
    visibility: hidden;
    &::before {
      content: 'Hidden from Percy';
      visibility: visible;
    }
  }
}
```

Disabling all CSS animations across all elements for the whole site:

```css
@media only percy {
  * {
    animation: none !important;
    transition: none !important;
  }
}
```

Making sure an element extends a certain height and doesn't get cut off where the viewport does:

```css
@media only percy {
  .element-c {
    height: 900px;
    overflow: hidden;
  }
}
```

## Excluding Percy-specific CSS from your build

Even though Percy-specific CSS won't affect your built app by hiding elements, preventing animations, and whatever else your custom CSS does, there's still no reason to ship it in your build. There are many different ways you could exclude it, based on your build config, but here's one I've done in the past:

In your main component file, e.g. where your router is:s
```js
if (window.Cypress) {
  import('./lib/percy.scss')
}
```

Obviously, this is specific to using Percy in Cypress, but there's probably something similar you could do for other testing frameworks.

You can also keep your Percy CSS [in your `.percy.yml` file or in your tests](https://docs.percy.io/docs/percy-specific-css#snapshot-options--sdk-options) instead of in a CSS file.

```yml
snapshot:
  percy-css: |
    iframe {
      display: none;
    }
```

```js
cy.percySnapshot('Snapshot name', {
  percyCSS: `iframe { display: none; }`
})
```

This last approach can be handy if you have CSS that you only want to apply to one or more snapshots but not all of them.

## Conclusion:

These two steps:

1. Making sure that the CSS only gets included when snapshotting and
1. Making sure that the CSS only applies for Percy (e.g. by using a Percy media query or including the CSS in your `.percy.yml` file)

means that the CSS only gets used when Percy is snapshotting and won't affect your production build or even your tests.
