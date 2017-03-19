<template>
	<div class="order-category">
    <div class="category-label">
      {{ name }}
    </div>
    <div class="category-items">
      <slot>
        這個類別沒東西，嫩。
      </slot>
    </div>
  </div>
</template>

<script>
export default {

  name: 'Category',
  props: ['name'],
  data () {
    return {

    }
  }
}
</script>

<style lang="css" scoped>

.order-category {
  align-items: stretch;
  background-color: #eee;
  display: flex;
  margin-bottom: 1em;
}

.order-category .category-label {
  align-items: center;
  background-color: #757575;
  border-radius: 4px 0 0 4px;
  color: white;
  display: flex;
  font-size: 2.5em;
  padding: 0 0.2em;
  text-align: center;
}

.order-category .category-items {
  align-items: center;
  display: flex;
  flex-flow: wrap;
  justify-content: center;
}

</style>
