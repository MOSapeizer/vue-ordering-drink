<template>
  <div :class="{ scale }">
    <span v-for="unit in scale" @click="chooseSugar(unit)" :class=" unit.level">{{ unit.sugar }}</span>
  </div>
</template>

<script>
export default {
  name: 'scale',
  props: ['unit', 'hidden'],
  data () {
    return {
      scale: [{ sugar: `無${this.unit}`, level: 'level-1' },
              { sugar: `微${this.unit}`, level: 'level-2' },
              { sugar: `半${this.unit}`, level: 'level-3' },
              { sugar: `少${this.unit}`, level: 'level-4' },
              { sugar: `全${this.unit}`, level: 'level-5' }]
    }
  },
  methods: {
    chooseSugar (unit) {
      this.hidden = false
      this.$emit('click', unit.sugar)
    }
  }
}
</script>

<style scoped>

.scale {
  background-color: white;
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 4px;
  top: 0;
  left: 0;
  display: flex;
  -webkit-align-items: center;
          align-items: center;
}

.scale span {
  align-self: stretch;
  flex: 1;
  display: flex;
  -webkit-align-items: center;
          align-items: center;
  -webkit-justify-content: center;
          justify-content: center;
}

.level-1 {
  opacity: 0.2;
  border-radius: 4px 0 0 4px;
}

.level-2 {
  opacity: 0.4;
}

.level-3 {
  opacity: 0.6;
}

.level-4 {
  opacity: 0.8;
}

.level-5 {
  border-radius: 0 4px 4px 0;
  opacity: 1;
}

.isHidden {
  display: none;
}

.level-cold-base span {
  background-color: #ff7575;
}

.level-hot-base span {
  background-color: #7575cc;
}
</style>
