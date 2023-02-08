<template>
  <div class="modal">
    <div class="content">
      <label for="">Name</label>
      <input v-model="form.name" :class="{ error: errors.name }" type="text">

      <label for="">Amount</label>
      <input v-model.number="form.amount" :class="{ error: errors.amount }" type="text">

      <div class="buttons">
        <button @click="$emit('close')">Cancel</button>
        <button @click="addExpense()">Add Expense</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    categoryId: {
      type: Number,
      requred: true
    }
  },

  data () {
    return {
      form: {
        name: null,
        amount: null
      },

      errors: {
        name: false,
        amount: false
      }
    }
  },

  methods: {
    addExpense () {
      this.errors = {
        name: false,
        amount: false
      }

      if (!this.form.name) this.errors.name = true
      if (!this.form.amount) this.errors.amount = true

      if (this.errors.name || this.errors.amount) return

      this.$emit('add', {
        categoryId: this.categoryId,
        name: this.form.name,
        amount: this.form.amount
      })
    }
  }
}
</script>

<style lang="scss" scoped>
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgba(0,0,0,.8);
    .content {
      background-color: #fff;
      padding: 50px;
      border-radius: 10px;
      display: flex;
      flex-direction: column;
      input {
        padding: 15px 20px;
        font-size: 18px;
        width: 300px;
        outline: none;
        &.error {
          border-color: red;
        }
      }

      .buttons {
        display: flex;
        margin-top: 20px;
        button {
          flex: 1;
          height: 50px;
        }
      }
    }
  }
</style>
