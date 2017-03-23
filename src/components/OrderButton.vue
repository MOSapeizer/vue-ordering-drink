<template>
  <div class="order">
    <div class="normal">
      <span class="content">{{ name }}</span>
      <button v-for="type in typeList" @click="chooseType(type)" :class="type.class" :style="{ backgroundColor: type.backgroundColor }">{{ type.name }}</button>
      <scale v-if="scaleActive" :unit="scaleUnit" :levels="scale" :color="scaleBaseColor" @click="setOrder"></scale>
      <button v-if="scaleActive" @click="reset" class="cancel">x</button>
    </div>
  </div>
</template>

<script>
import Scale from '@/components/Scale'

export default {
  name: 'orderButton',
  components: {
    Scale
  },
  props: ['name'],
  data () {
    return {
      scale: [],
      scaleUnit: '',
      scaleActive: false,
      scaleBaseColor: 'inherit',
      typeList: [
        { name: '冰',
          scalable: true,
          class: 'half-left',
          backgroundColor: '#ff7575'
        },
        {
          name: '熱',
          scalable: false,
          class: 'half-right',
          backgroundColor: '#5493B2'
        }
      ],
      sugarScaleHidden: true,
      order: {
        name: '',
        temperture: '',
        sugar: ''
      }
    }
  },
  methods: {
    showSugarScale () {
      this.scale = ['無', '微', '半', '少', '全']
      this.scaleUnit = '糖'
      this.scaleActive = true
    },
    chooseType (type) {
      this.order.name = this.name
      if (type.name === '冰') {
        this.scale = ['去', '微', '半', '少', '全']
        this.scaleUnit = type.name
        this.scaleBaseColor = type.backgroundColor
        this.scaleActive = true
      } else if (type.name === '熱') {
        this.order.temperture = type.name
        this.scaleBaseColor = type.backgroundColor
        this.showSugarScale()
      }
    },
    setOrder (message) {
      if (this.order.temperture === '') {
        this.order.temperture = message
        this.showSugarScale()
      } else {
        this.order.sugar = message
        this.$emit('check', this.order)
        this.reset()
      }
    },
    reset () {
      for (var key in this.order) {
        this.order[key] = ''
      }
      this.scaleActive = false
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
  font-size: 20px;
  margin: 8px;
  padding: 20px;
  position: relative;
  text-align: center;
  transition: all 0.5s;
  min-width: 120px;
}

.cancel {
  border-radius: 16px;
  border: none;
  background-color: #cc3333;
  color: white;
  position: absolute;
  right: -10px;
  top: -12px;
  font-size: 20px;
  padding: 0px 8px 4px;
  text-align: center;
}

.normal .half-left, .normal .half-right {
  border: none;
  color: #FFFFFF;
  cursor: pointer;
  font-size: 20px;
  opacity: 0;
  padding: 20px;
  position: absolute;
  text-align: center;
  top: 0px;
  width: 50%;
}

.normal:hover .half-left {
  opacity: 1;
  transition: opacity 0.3s ease;
}

.normal:hover .half-right {
  opacity: 1;
  transition: opacity 0.3s ease;
}

.half-left {
  border-radius: 4px 0 0 4px;
  display: inline-block;
  left: 0px;
}

.half-right {
  border-radius: 0 4px 4px 0;
  display: inline-block;
  right: 0px;
}
</style>
