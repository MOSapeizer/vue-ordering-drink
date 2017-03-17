<template>
  <div class="app">
    <order-button name="蜂蜜紅茶"></order-button>
  </div>
</template>

<script>
import OrderButton from '@/components/OrderButton'

export default {
  name: 'app',
  components: {
    OrderButton
  },
  data () {
    return {
      orderList: []
    }
  }
}
</script>

<style scoped>

</style>
