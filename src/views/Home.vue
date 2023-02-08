<template>
  <div class="home">
    <div class="expenses">
      <ExpenseCategoryView
        v-for="category in expenseCategories"
        :key="category.id"
        :category="category"
        :expenses="getCategoryExpenses(category.id)"
        @click="openAdd(category.id)" />
    </div>

    <ul>
      <li v-for="(expense, index) in expenses" :key="index">
        <span>{{ expense.name }} ({{ getCategoryName(expense.categoryId) }})</span>
        <div>
          <span class="amount">${{ expense.amount }}</span>
          <button class="delete" @click="deleteExpense(index)">X</button>
        </div>
      </li>
    </ul>

    <add-expense
      v-if="addingExpenseInProgress"
      :categoryId="addingExpenseInProgress"
      @close="addingExpenseInProgress = null"
      @add="addExpense($event)" />
  </div>
</template>

<script>
import AddExpense from '@/components/AddExpense'
import ExpenseCategoryView from '@/components/ExpenseCategoryView'

export default {
  name: 'Home',

  components: {
    AddExpense,
    ExpenseCategoryView
  },

  data () {
    return {
      expenses: [],

      addingExpenseInProgress: null,

      expenseCategories: [
        {
          id: 1,
          name: 'Prodavnica'
        },
        {
          id: 2,
          name: 'Shopping'
        },
        {
          id: 3,
          name: 'Transport'
        },
        {
          id: 4,
          name: 'Racuni'
        }
      ]
    }
  },

  methods: {
    deleteExpense (index) {
      this.expenses.splice(index, 1)
    },

    addExpense (expense) {
      this.expenses.unshift(expense)
      this.addingExpenseInProgress = null
    },

    openAdd (categoryId) {
      this.addingExpenseInProgress = categoryId
    },

    getCategoryName (categoryId) {
      const category = this.expenseCategories.find(category => category.id === categoryId)
      return category.name
    },

    getCategoryExpenses (categoryId) {
      return this.expenses.filter(expense => expense.categoryId === categoryId)
    }
  }
}
</script>

<style lang="scss" scoped>
  .home {
    width: 800px;
    margin: 0 auto;
    display: flex;
    padding: 100px 0;
    flex-direction: column;
    .expenses {
      display: flex;
      justify-content: space-between;
    }

    ul {
      margin: 0;
      margin-top: 50px;
      padding: 0;
      list-style: none;
      li {
        padding: 15px 0;
        border-top: 1px solid rgba(0,0,0,.2);
        display: flex;
        justify-content: space-between;
        .amount {
          font-weight: bold;
        }
        .delete {
          background: red;
          color: #fff;
          margin-left: 15px;
        }
      }
    }
  }
</style>
