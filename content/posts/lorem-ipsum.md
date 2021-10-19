---
title: "Lorem Ipsum"
tags: ["temp"]
date: 2021-10-18T22:03:52-04:00
draft: true
---

## Running

Run with drafts visible: `hugo server -D`


Update theme: `git submodule update --remote --merge`


## New Post
hugo new posts/my-first-post.md

```
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



## Info

Theme: [Cupper](https://themes.gohugo.io/themes/cupper-hugo-theme/)

