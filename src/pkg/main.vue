<template>
  <div :id="id" class="ai-particles">
    <slot name="default"></slot>
  </div>
</template>

<script>
import particlesJS from '../plugins/particles'

export default {
  name: 'AiParticles',
  props: {
    // 自定义配置
    options: {
      type: [Object, undefined],
      default: undefined
    },
    // 粒子形状
    shapeType: {
      type: String,
      default: 'star'
    },
    // 自定义粒子图片
    shapeImage: {
      type: Object,
      default: () => ({
        src: ''
      })
    }
  },
  data() {
    return {}
  },
  computed: {
    id() {
      return `ai-particles-${this._uid}`
    },
    form() {
      if (this.options) return this.options

      return {
        "particles": {
          "number": {
            "value": 30,
            "density": {
              "enable": true,
              "value_area": 800
            }
          },
          "color": {
            "value": "#ffffff"
          },
          "shape": {
            "type": "star",
            "stroke": {
              "width": 0,
              "color": "#000000"
            },
            "polygon": {
              "nb_sides": 5
            },
            "image": {
              "src": "img/github.svg",
              "width": 100,
              "height": 100
            }
          },
          "opacity": {
            "value": 0.5,
            "random": false,
            "anim": {
              "enable": false,
              "speed": 1,
              "opacity_min": 0.1,
              "sync": false
            }
          },
          "size": {
            "value": 10,
            "random": true,
            "anim": {
              "enable": false,
              "speed": 80,
              "size_min": 0.1,
              "sync": false
            }
          },
          "line_linked": {
            "enable": true,
            "distance": 300,
            "color": "#ffffff",
            "opacity": 0.4,
            "width": 2
          },
          "move": {
            "enable": true,
            "speed": 6,
            "direction": "none",
            "random": false,
            "straight": false,
            "out_mode": "out",
            "bounce": false,
            "attract": {
              "enable": false,
              "rotateX": 600,
              "rotateY": 1200
            }
          }
        },
        "interactivity": {
          "detect_on": "canvas",
          "events": {
            "onhover": {
              "enable": false,
              "mode": "repulse"
            },
            "onclick": {
              "enable": true,
              "mode": "push"
            },
            "resize": true
          },
          "modes": {
            "grab": {
              "distance": 800,
              "line_linked": {
                "opacity": 1
              }
            },
            "bubble": {
              "distance": 800,
              "size": 80,
              "duration": 2,
              "opacity": 0.8,
              "speed": 10
            },
            "repulse": {
              "distance": 400,
              "duration": 0.4
            },
            "push": {
              "particles_nb": 4
            },
            "remove": {
              "particles_nb": 2
            }
          }
        },
        "retina_detect": true
      }
    }
  },
  mounted() {
    this.init()
  },
  methods: {
    init() {
      particlesJS(this.id, this.form)
    }
  }
}
</script>

<style lang="scss" scoped>
.ai-particles {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: #b61924;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50% 50%;
}
</style>