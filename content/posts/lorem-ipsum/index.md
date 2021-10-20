---
title: "Lorem Ipsum"
tags: ["temp"]
date: 2021-10-18T22:03:52-04:00
lastmod: 2021-10-19T19:34:52-04:00
draft: true
categories: ["JavaScript"]
summary: "Animi placeat suscipit repellendus ut quia veritatis exercitationem odio."

featuredImage: "lorem-ipsum.png"
featuredImagePreview: "lorem-ipsum.png"
---

## Running

Run with drafts visible: `hugo server -D`


Update theme: `git submodule update --remote --merge`


## New Post
hugo new posts/my-first-post.md

```html
<main id="main">
  <h1>{{ .Title }}</h1>
  {{ if site.Params.search }}
  <input
    id="search"
    type="text"
    placeholder="{{ T "search_placeholder" }}"
    aria-label="{{ T "search_aria_label" }}"
  />
  {{ end }}
</main>
```

```js
function getColorsFromLocalStyles() {
    const colors = []
    const styles = figma.getLocalPaintStyles()

    for (const style of styles) {
        for (const paint of style.paints) {
            if (paint.type == 'SOLID') {
                const paintHEX = chroma.gl(...Object.values(paint.color)).hex()
                if (!colors.includes(paintHEX)) {
                    colors.push(paintHEX)
                }
            }
        }
    }
    return colors
}
```



## Info

Theme: [Cupper](https://themes.gohugo.io/themes/cupper-hugo-theme/)

