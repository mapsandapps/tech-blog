---
title: "Splitting a filename"
subtitle: ""
date: 2021-10-20T20:40:12-04:00
lastmod: 2021-10-20T20:40:12-04:00
draft: true
authorLink: ""
description: ""

tags: ["javascript", "typescript"]
categories: ["Web Dev"]

hiddenFromHomePage: false
hiddenFromSearch: false

featuredImage: "header.png"
featuredImagePreview: "header.png"

toc:
  enable: true
math:
  enable: false
lightgallery: false
license: ""
---

Ok, so it's pretty common to need to split a filename into its 'name' and 'extension' parts. But what we're going to do here is a little bit more than that. We're going to do that, but we also want to go one step further and handle a special case for specs, where we're basically considering `_spec` to be part of the extension, as this is a common naming convention for spec files.

So `blog_spec.ts` should be split into `blog` and `_spec.ts`.

<!--more-->


## The Code

Steps we will take:

1. Handle missing data
2. Strip directory from filename
3. Check for _spec.ext, since we’ll want all of that as one chunk (if we wanted the extension to be a separate item in our array, we could do it differently)
4. Check for the extension
5. Return split value and display it

### getFilenameParts()

```ts
// strips directory path and then
// '_spec' and any file extension should be split off from the main part of the filename
const getFilenameParts = (spec: string): [string, string] => {
  if (!spec) {
    return ['', '']
  }

  const specWithoutPath = spec.substr(spec.lastIndexOf('/') + 1)

  if (!specWithoutPath) {
    return [spec, '']
  }

  const specIndex = specWithoutPath.indexOf('_spec.')

  if (specIndex > -1) {
    return splitFilename[specWithoutPath.substr(0, specIndex), specWithoutPath.substr(specIndex)]
  }

  const dotIndex = specWithoutPath.indexOf('.')

  if (dotIndex < 0) return [spec, '']

  return splitFilename([specWithoutPath.substr(0, dotIndex), specWithoutPath.substr(dotIndex)])
}
```

The `.` is to prevent splitting it at `_spec` if `_spec` is in the middle of a filename. E.g. `header_spec_viz.js` should become `header_spec_viz` and `.js`, not `header` and `_spec_viz.js`.

## Refactoring

### splitFilename()

We can use the `splitFilename` helper function to perform the repetitive task of splitting the filename at the given index.

```ts
const splitFilename = (filename: string, index: number): [string, string] => {
  if (index < 0) {
    return [filename, '']
  }

  return [filename.substr(0, index), filename.substr(index)]
}
```


## Refactored

```ts
// strips directory path and then
// '_spec' and any file extension should be split off from the main part of the filename
const getFilenameParts = (spec: string): [string, string] => {
  if (!spec) {
    return ['', '']
  }

  const specWithoutPath = spec.substr(spec.lastIndexOf('/') + 1)

  if (!specWithoutPath) {
    return [spec, '']
  }

  const specIndex = specWithoutPath.indexOf('_spec.')

  if (specIndex > -1) {
    return splitFilename(specWithoutPath, specIndex)
  }

  const dotIndex = specWithoutPath.indexOf('.')

  if (dotIndex < 0) return [spec, '']

  return splitFilename(specWithoutPath, dotIndex)
}
```


{{< codepen pen="PoKGRoK" defaultTab="js" >}}

## Tests

![test results](tests.png)

{{< codepen pen="JjyRpGe" defaultTab="js" >}}


## Potential Adjustments
