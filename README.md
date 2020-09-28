# aidol-particles

a particulate background component based on particles.js.

# Preview

![image](https://github.com/yisibell/aidol-particles/blob/master/docs/images/example.gif)

# Installation

``` bash
$ npm i @aidol/particles -S
```

# Usage

``` html
<template>
  <ai-particles>
    <div> some content </div>
  </ai-particles>
</template>
```

``` js
import AiParticles from '@aidol/particles'
export default {
  name: 'Login',
  components: {
    AiParticles
  },
  data() {
    return {}
  }
}
```