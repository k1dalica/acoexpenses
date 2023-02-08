<template>
  <div class="category" @click="$emit('click')">
    <div>{{ category.name }}</div>
    <div class="amount">$ {{ total }}</div>
  </div>
</template>

<script>
export default {
  props: {
    category: {
      type: Object,
      required: true
    },

    expenses: {
      type: Array,
      required: true
    }
  },

  computed: {
    total () {
      return this.expenses.reduce((acc, ex) => acc + ex.amount, 0)
    }
  }
}
</script>

<style lang="scss" scoped>
  .category {
    width: 150px;
    height: 150px;
    border-radius: 5px;
    border: 2px solid rgba(0,0,0,.2);
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    flex-direction: column;
    .amount {
      font-weight: 900;
      font-size: 24px;
      margin-top: 10px;
    }
    &:hover {
      border-color: aquamarine;
      transition: all ease .4s;
    }
  }
</style>
