# Nuxt Usage

If you are using [**Nuxt**](https://nuxtjs.org/), this package has a specific implementation that makes the declaration of custom directives even easier.

It is shipped with `@vueuse/motion` and is importable via `@vueuse/motion/nuxt`.

It should work with `nuxt3` and `@nuxt/bridge`.

## Installation

Add `@vueuse/motion/nuxt` to the `modules` section of `nuxt.config.js`:

```javascript
{
  // nuxt.config.js
  modules: ['@vueue/motion/nuxt']
}
```

Then, configure your animations 🤹:

```javascript
{
  // nuxt.config.js
  motions: {
    directives: {
      'pop-bottom': {
        initial: {
          scale: 0,
          opacity: 0,
          y: 100
        },
        visible: {
          scale: 1,
          opacity: 1,
          y: 0
        },
      }
    }
  }
}
```

## SSR Support

`@vueuse/motion` supports SSR via directives.

SSR support for animations mainly consists in resolving `initial` variant from your component bindings.

Once resolve, this `initial` value gets merged with your component `style` attribute.

```vue
<template>
  <div
    v-motion="{
      initial: {
        y: 100,
        opacity: 0
      },
      enter: {
        y: 0,
        opacity: 1
      }
    }"
  >
    Hello
  </div>

  <!-- OR -->

  <div
    v-motion
    :initial="initial"
    :enter="enter"
  >
    Hello
  </div>
</template>

<script setup>
const initial = ref({
  y: 100,
  opacity: 0,
})

const enter = ref({
  y: 0,
  opacity: 1,
})
</script>
```

This div will have be rendered server-side as:

```html
<div style="opacity:0;transform:translate3d(0px,100px,0px);">Hello</div>
```

You can obviously imagine plenty of implementations with this, always knowing that your animations will be properly server-side rendered.
