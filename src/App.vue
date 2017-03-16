<template>
  <div>
    <div class="normal">
      <button @click="clickLeft" class="half-left">冷</button>
      <button @click="clickRight" class="half-right">熱</button>
      <span class="content">{{ order.name }}</span>
      <scale unit="糖" :class="[{ hidden: scaleHidden }, levelBaseColor]" @click="setSugar"></scale>
      <!-- <div class="scale" :class="{ hidden: scaleHidden }">
        <span v-for="unit in scale" @click="chooseSugar(unit)" :class="[levelBaseColor, unit.level]">{{ unit.sugar }}</span>
      </div> -->
    </div>
    <p>{{ orderOutput }}</p>
  </div>
</template>

<script>
import Scale from '@/components/Scale'

export default {
  name: 'app',
  components: {
    Scale
  },
  data () {
    return {
      scaleBaseColor: '',
      scaleHidden: true,
      scale: [{ sugar: '無糖', level: 'level-1' },
                  { sugar: '微糖', level: 'level-2' },
                  { sugar: '半糖', level: 'level-3' },
                  { sugar: '少糖', level: 'level-4' },
                  { sugar: '全糖', level: 'level-5' }],
      order: {
        name: '蜂蜜紅茶',
        temperture: '',
        sugar: ''
      }
    }
  },
  methods: {
    clickLeft () {
      this.showUpScale('cold')
      this.order.temperture = '冰'
    },
    clickRight () {
      this.showUpScale('hot')
      this.order.temperture = '熱'
    },
    showUpScale (colorState) {
      this.scaleBaseColor = colorState
      this.scaleHidden = false
    },
    setSugar (unit) {
      this.scaleHidden = true
      this.order.sugar = unit
    }
  },
  computed: {
    levelBaseColor () {
      return 'level-' + this.scaleBaseColor + '-base'
    },
    orderOutput () {
      return `${this.order.name} ${this.order.temperture} ${this.order.sugar}`
    }
  }
}
</script>

<style scoped>

button {
  outline: none;
}

.normal {
  border-radius: 4px;
  background-color: #757575;
  border: none;
  color: #FFFFFF;
  cursor: pointer;
  font-size: 28px;
  margin: 5px;
  padding: 20px;
  position: relative;
  text-align: center;
  transition: all 0.5s;
  width: 200px;
}

.normal .half-left, .normal .half-right {
  border: none;
  color: #FFFFFF;
  cursor: pointer;
  font-size: 28px;
  opacity: 0;
  padding: 20px;
  position: absolute;
  text-align: center;
  top: 0px;
  width: 50%;
}

.half-left {
  background-color: #ff7575;
  border-radius: 4px 0 0 4px;
  display: inline-block;
  left: 0px;
}

.half-right {
  background-color: #7575cc;
  border-radius: 0 4px 4px 0;
  display: inline-block;
  right: 0px;
}

.normal:hover .half-left {
  opacity: 1;
  transition: opacity 0.3s ease;
}

.normal:hover .half-right {
  opacity: 1;
  transition: opacity 0.3s ease;
}

.hidden {
  display: none !important; 
}
</style>
