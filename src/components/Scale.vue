<template>
  <div class="scale">
    <span v-for="level in levels" @click="chooseLevel(level)" class="level" :style="{ backgroundColor: levelOpacity(level) }">
      {{ fullLevelName(level) }}
    </span>
  </div>
</template>

<script>
export default {
  name: 'scale',
  props: {
    unit: {
      type: String,
      required: true,
      default: ''
    },
    levels: {
      type: Array,
      default: function () {
        return []
      }
    },
    color: {
      type: String,
      default: 'black'
    }
  },
  methods: {
    chooseLevel (level) {
      this.$emit('click', this.fullLevelName(level))
    },
    fullLevelName (level) {
      return level + this.unit
    },
    levelOpacity (level) {
      let proportion = (this.levels.indexOf(level) + 1) / this.levels.length
      let rgbColor = this.hexToRGB(this.color)
      return `rgba(${rgbColor}, ${proportion})`
    },
    hexToRGB (hex) {
      let shorthandRegex = /^#?([a-f\d])([a-f\d])([a-f\d])$/i
      hex = hex.replace(shorthandRegex, (m, r, g, b) => {
        return r + r + g + g + b + b
      })

      var result = /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(hex)
      if (result.length >= 4) {
        let r = parseInt(result[1], 16)
        let g = parseInt(result[2], 16)
        let b = parseInt(result[3], 16)

        return `${r}, ${g}, ${b}`
      }

      return result
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

.scale .level {
  align-self: stretch;
  flex: 1;
  display: flex;
  -webkit-align-items: center;
          align-items: center;
  -webkit-justify-content: center;
          justify-content: center;
}

.level:before {
  background-color: white;
  width: 100%;
  height: 100%;
}

.level:first {
  border-radius: 4px 0 0 4px;
}

.level:last {
  border-radius: 0 4px 4px 0;
}

.level .level-text {
  opacity: 1;
}
</style>
