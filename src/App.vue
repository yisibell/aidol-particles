<template>
  <div id="app">
    <ai-particles />
  </div>
</template>

<script>
import AiParticles from './pkg/main'

export default {
  name: 'App',
  components: {
    AiParticles
  },
  data() {
    return {}
  },
  methods: {}
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
</style>
