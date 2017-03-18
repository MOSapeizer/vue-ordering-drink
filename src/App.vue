<template>
  <div class="app">
    <order-button v-for="drink in drinkList" @check="saveOrder" :name="drink"></order-button>
    <ol class="order-list">
      <span>你點的是：</span>
      <li v-for="order in orderList">
        <span :style="{ backgroundColor: orderColor(order) }" class="order">{{ print(order) }}</span>
        <button :style="{ backgroundColor: orderColor(order) }" @click="remove(order)" class="cancel">Ｘ</button>
      </li>
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
    },
    remove (order) {
      let index = this.orderList.indexOf(order)
      this.orderList.splice(index, 1)
    },
    orderColor (order) {
      if (order.temperture.includes('冰')) {
        return '#ff7575'
      } else if (order.temperture.includes('熱')) {
        return '#7575cc'
      }
    }
  }
}
</script>

<style scoped>
button {
  outline: none;
}

.order {
  display: inline-block;
}

.order-list .order, .order-list .cancel {
  border-radius: 4px;
  border: none;
  color: #FFFFFF;
  font-size: 20px;
  padding: 4px 8px;
  position: relative;
  text-align: center;
}

.order-list li {
  margin: 5px 0;
}
</style>
