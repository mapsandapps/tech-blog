---
title: "Adjusting whether a snippet will be open or closed in the LoveIt Hugo theme"
subtitle: ""
date: 2021-10-19T20:45:22-04:00
lastmod: 2021-10-19T20:45:22-04:00
draft: true
authorLink: ""
description: ""
summary: "Shown on home page"

tags: ["hugo", "loveit"]
categories: ["Misc"]

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

You might have noticed that some of your snippets (aka code blocks) are open while others are closed when using the [LoveIt](https://hugoloveit.com/) Hugo theme.

<!--more-->



TODO: figure out how to adjust per snippet


{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=199" >}}
here is
some code
isn't
it nice?
{{< / highlight >}}




```toml
    [params.page.code]
      # whether to show the copy button of the code block
      copy = true
      # the maximum number of lines of displayed code by default
      maxShownLines = 10
```
You can also adjust whether or not a copy button shows in the top right of the code block.
