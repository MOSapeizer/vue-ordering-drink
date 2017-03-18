<template>
  <div class="app">
    <order-button v-for="drink in drinkList" @check="saveOrder" :name="drink"></order-button>
    <ol>
      <span>你點的是：</span>
      <li v-for="order in orderList">{{ print(order) }}</li>
    </ol>
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
      drinkList: ['觀音拿鐵', '紅豆拿鐵', '檸檬綠茶', '優格綠茶', '珍珠奶茶', '水果茶'],
      orderList: []
    }
  },
  methods: {
    saveOrder (order) {
      this.orderList.push({
        name: order.name,
        temperture: order.temperture,
        sugar: order.sugar
      })
    },
    print (order) {
      return `${order.name} ${order.temperture} ${order.sugar}`
    }
  }
}
</script>

<style scoped>
.order {
  display: inline-block;
}
</style>
