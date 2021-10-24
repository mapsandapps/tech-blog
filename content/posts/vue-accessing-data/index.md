---
title: "Accessing ____ in ____ in Vue"
subtitle: ""
date: 2021-10-24T10:01:22-04:00
lastmod: 2021-10-24T10:01:22-04:00
draft: true
authorLink: ""

tags: ['vue', 'vuex']
categories: ['Web Dev']

hiddenFromHomePage: false
hiddenFromSearch: false

featuredImage: "vue-accessing-data.png"
featuredImagePreview: "vue-accessing-data.png"

toc:
  enable: true
math:
  enable: false
lightgallery: false
license: ""
---

I have a hard time remembering the syntax for sharing data within and between the store and components in Vue. Here's a guide to how to do all the combos of data sharing.

<!--more-->

## Store in Store

### State in Getters, Mutations (probably more)

```vue
getters: {
  colors(state) {
    return state.selectedColors.map(color => {
      return getClosestColor(color, state.colorStyles, state.threshold)
    })
  }
},
mutations: {
  setColorStyles(state, colors) {
    state.colorStyles = colors
  },
}
```


### Getters in Actions

```vue
actions: {
  replaceColors({ getters }) {
    each(getters.colors, color => {
      if (color.closestColorStyle) {
        parent.postMessage({ pluginMessage: { name: 'replaceColor', data: color }}, '*')
      }
    })
  }
}
```

TODO: more combos for store in store

## Component in Component

### Data in Computed
```vue
data() {
  return {
    swatchWidth: 48
  }
},
computed: {
  width: function() {
    return this.swatchWidth * 1.5 + 2
  }
}
```

### Props in Computed
```vue
props: {
  color: {
    type: Object,
    required: true
  }
},
computed: {
  textColor: function() {
    // if bg is dark, text is white
    // if bg is light, text is black
    return getLightVsDark(this.color.closestColorStyle?.hex || this.color.originalColor.hex) === LightDarkEnum.Light ? 'black' : 'white'
  }
}
```

TODO: more combos for component in component


## Store in Component

### State and Getters

State and getters come in to `computed` via `mapState` and `mapGetters`.

```vue
import { mapGetters, mapState } from 'vuex'
```

```vue
computed: {
  ...mapGetters(['colors']),
  ...mapState(['colorStyles'])
},
```

Then you can use these in the HTML of a component by using them directly:

```vue
<ColorListItem
  v-for="(color, index) of colors"
  :color="color"
  :key="'color-' + index" />
```

Or in the components' `computed` [etc?] by using `this`:

```vue
computed: {
  ...mapState(['colorStyles']),
  inputtedColorSwatches: function() {
    if (this.colorStyles.length === 0) return

    // ...
  }
}
```

### Mutations and Actions

Mutations and actions come in to `methods` via `mapMutations` and `mapActions`.

```vue
import { mapActions, mapMutations } from 'vuex'
```

```vue
methods: {
  ...mapMutations(['setColorStyles', 'setSelectedColors']),
  ...mapActions(['closePlugin', 'replaceColors']),
}
```

You can then use those in the HTML of a component by using them directly:

```vue
<button @click="replaceColors">Replace colors</button>
<button @click="closePlugin">Cancel</button>
```

Or in [e.g.?] `methods` via `this`:

(TODO: need a better example here)

```vue
methods: {
  ...mapMutations(['setColorStyles']),
  handleMessage() {
    onmessage = (event: any) => {
      this.setColorStyles(event.data.pluginMessage.data)
    }
  }
},
```



