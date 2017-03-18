<template>
  <div class="order">
    <div class="normal">
      <span class="content">{{ name }}</span>
      <button v-for="type in typeList" @click="chooseType(type)" :class="type.class">{{ type.name }}</button>
      <scale v-if="scaleActive" :unit="scaleUnit" :class="levelBaseColor" @click="setOrder"></scale>
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
      scaleUnit: '',
      scaleActive: false,
      scaleBaseColor: '',
      typeList: [
        { name: '冰',
          scalable: true,
          class: 'half-left',
          backgroundColor: 'cold'
        },
        {
          name: '熱',
          scalable: false,
          class: 'half-right',
          backgroundColor: 'hot'
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
      this.scaleUnit = '糖'
      this.scaleActive = true
    },
    chooseType (type) {
      this.order.name = this.name
      if (type.name === '冰') {
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
        this.scaleActive = false
        this.$emit('check', this.order)
        this.reset()
      }
    },
    reset () {
      for (var key in this.order) {
        this.order[key] = ''
      }
    }
  },
  computed: {
    levelBaseColor () {
      return 'level-' + this.scaleBaseColor + '-base'
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

.normal:hover .half-left {
  opacity: 1;
  transition: opacity 0.3s ease;
}

.normal:hover .half-right {
  opacity: 1;
  transition: opacity 0.3s ease;
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
</style>
