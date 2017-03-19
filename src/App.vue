<template>
  <div class="app">
    <div class="main">
      <category name="茶類">
        <order-button v-for="drink in drinkList" :key="drink.id" @check="saveOrder" :name="drink"></order-button>
      </category>
      <category name="茶類">
        <order-button v-for="drink in drinkList" :key="drink.id" @check="saveOrder" :name="drink"></order-button>
      </category>
      <category name="茶類">
        <order-button v-for="drink in drinkList" :key="drink.id" @check="saveOrder" :name="drink"></order-button>
      </category>
    </div>
    <div class="aside">
      <ol class="order-list">
        <span>清單：</span>
        <li v-for="order in orderList">
          <span :style="{ backgroundColor: orderColor(order) }" class="order">{{ print(order) }}</span>
          <button :style="{ backgroundColor: orderColor(order) }" @click="remove(order)" class="cancel">Ｘ</button>
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
import Category from '@/components/Category'
import OrderButton from '@/components/OrderButton'

export default {
  name: 'app',
  components: {
    Category,
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
      let lastId = this.lastOrder().id || 0
      this.orderList.push({
        id: lastId + 1,
        name: order.name,
        temperture: order.temperture,
        sugar: order.sugar
      })
    },
    lastOrder () {
      let lastOrder = this.orderList[this.orderList.length - 1]
      if (lastOrder) {
        return lastOrder
      }
      return {}
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

.app {
  display: flex;
  width: 100%;
}

.main {
  display: inline-block;
  flex: 7;
  margin: 1em;
}

.aside {
  display: inline-block;
  flex: 3;
}

button {
  outline: none;
}

ol {
  list-style: none;
}

.order {
  display: inline-block;
}

.order-list .order, .order-list .cancel {
  border-radius: 4px;
  border: none;
  color: #FFFFFF;
  font-size: 16px;
  padding: 4px 8px;
  position: relative;
  text-align: center;
}

.order-list li {
  margin: 5px 0;
}
</style>
