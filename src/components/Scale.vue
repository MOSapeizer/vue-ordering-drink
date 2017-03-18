<template>
  <div :class="{ scale }">
    <span v-for="unit in scale" @click="chooseLevel(unit)" :class="unit.class">{{ fullLevelName(unit) }}</span>
  </div>
</template>

<script>
export default {
  name: 'scale',
  props: ['unit'],
  data () {
    return {
      scale: [{ level: '無', class: 'level-1' },
              { level: '微', class: 'level-2' },
              { level: '半', class: 'level-3' },
              { level: '少', class: 'level-4' },
              { level: '全', class: 'level-5' }]
    }
  },
  methods: {
    chooseLevel (unit) {
      this.$emit('click', this.fullLevelName(unit))
    },
    fullLevelName (unit) {
      return unit.level + this.unit
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
