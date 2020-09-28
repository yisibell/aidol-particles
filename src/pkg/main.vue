<template>
  <div :id="id" class="ai-particles" :style="[style]">
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
    // 容器背景色
    background: {
      type: String,
      default: ''
    },
    // 粒子连接线
    particlesLineLinked: {
      type: Object,
      default: () => ({
        enable: true, // 是否使用连接线
        distance: 300, // 链接距离
        color: "#ffffff", // 颜色
        opacity: 0.4, // 不透明度
        width: 1 // 粗细
      })
    },
    // 粒子数量
    particlesNumber: {
      type: Object,
      default: () => ({
        value: 30, // 粒子数量
        density: {
          enable: true,
          value_area: 800 // 粒子散布区域大小
        }
      })
    },
    // 粒子颜色
    particlesColor: {
      type: String,
      default: '#ffffff'
    },
    // 粒子形状
    particlesShape: {
      type: Object,
      default: () => ({
        // 粒子形状 {string | Array of string}
        // "circle" "edge" "triangle" "polygon" "star" "image" 
        // ["circle", "triangle", "image"]
        type: ['star', 'circle'],
        stroke: {
          width: 0, // 粒子边线粗细程度
          color: '#222222' // 粒子边线颜色
        },
        polygon: {
          nb_sides: 5 // 粒子多边形的边数，可以替代 type
        },
        image: { // 自定义粒子形状图片
          src: '',
          width: 100,
          height: 100
        }
      })
    },
    // 粒子不透明度
    particlesOpacity: {
      type: Object,
      default: () => ({
        value: 0.5, // 不透明度
        random: false, // 是否开启随机不透明度
        anim: {
          enable: true, // 是否开启渐变动画
          speed: 1, // 渐变动画速度
          opacity_min: 0.1, // 渐变动画最小不透明度
          sync: false // 是否开启同步渐变动画模式
        }
      })
    },
    // 粒子大小
    particlesSize: {
      type: Object,
      default: () => ({
        value: 6, // 粒子大小
        random: false, // 是否启用随机粒子大小
        anim: {
          enable: true, // 是否开启粒子大小渐变动画
          speed: 20, // 粒子大小渐变动画速度，值越大，越快
          size_min: 0.1, // 粒子大小渐变时的最小值
          sync: false // 是否开启同步变化
        }
      })
    },
    // 粒子移动效果
    particlesMove: {
      type: Object,
      default: () => ({
        enable: true, // 粒子是否开启移动效果
        speed: 4, // 粒子移动速度，值越大，速度越快
        // 粒子整体移动方向
        // "none" "top" "top-right" "right" "bottom-right" "bottom" "bottom-left" "left" "top-left"
        direction: 'none',
        random: false, // 移动方向是否随机
        straight: false, // 是否以笔直方式移动
        // 当粒子接触容器边缘时的处理方式
        // bounce 回弹 out 移出
        out_mode: "bounce",
        bounce: false,
        attract: {
          enable: false,
          rotateX: 600,
          rotateY: 1200
        }
      })
    },
    retinaDetect: {
      type: Boolean,
      default: true
    },
    interactivityDetectOn: {
      type: String,
      default: 'canvas'
    },
    // 定义互动事件
    interactivityEvents: {
      type: Object,
      default: () => ({
        // 鼠标移至粒子的效果
        onhover: {
          enable: true,
          // "grab"     抓取临近的
          // "bubble"   泡沫球效果
          // "repulse"  击退效果
          // ["grab", "bubble"]
          mode: 'grab'
        },
        // 鼠标点击粒子的效果
        onclick: {
          enable: false,
          mode: "push"
        },
        // 互动事件调整
        resize: true
      })
    },
    // 定义互动模式
    interactivityModes: {
      type: Object,
      default: () => ({
        // 抓取效果
        grab: {
          distance: 200, // 抓取范围
          line_linked: {
            opacity: 0.75
          }
        },
        // 泡沫效应
        bubble: {
          distance: 200, // 触发范围
          size: 20, // 泡沫增长大小
          duration: 2, // 动画持续时间
          opacity: 0.8, // 不透明度
          speed: 10 // 动画速度
        },
        // 击退效果
        repulse: {
          distance: 100, // 击退距离
          duration: 0.4 // 动画持续时间
        },
        // 插入粒子效果
        push: {
          particles_nb: 1 // 插入数量
        },
        // 减少粒子效果
        remove: {
          particles_nb: 1 // 减少数量
        }
      })
    }
  },
  data() {
    return {}
  },
  computed: {
    style() {
      const { background } = this
      return {
        background
      }
    },
    id() {
      return `ai-particles-${this._uid}`
    },
    form() {
      if (this.options) return this.options
      return {
        // 粒子
        "particles": {
          // 数量
          "number": this.particlesNumber,
          // 颜色
          "color": {
            "value": this.particlesColor
          },
          // 形状
          "shape": this.particlesShape,
          // 不透明度
          "opacity": this.particlesOpacity,
          // 大小
          "size": this.particlesSize,
          // 连接线
          "line_linked": this.particlesLineLinked,
          // 移动效果
          "move": this.particlesMove
        },
        // 互动
        "interactivity": {
          "detect_on": this.interactivityDetectOn,
          "events": this.interactivityEvents,
          "modes": this.interactivityModes
        },
        "retina_detect": this.retinaDetect
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
  background: linear-gradient(rgb(51, 14, 106) 0%, rgb(48, 200, 204) 99%) 0% 0% / auto repeat scroll padding-box border-box rgba(0, 0, 0, 0);
  background-repeat: no-repeat;
  background-size: cover;
  background-position: 50% 50%;
}
</style>