<script setup>
import { defineProps } from 'vue'
const props = defineProps({
  income: {
    type: Number,
    default: 0.00,
    required: true
  },
  expense: {
    type: Number,
    default: 0.00,
    required: true
  }
})
</script>

<template>
     <div class="inc-exp-container">
        <div>
          <h4>Income</h4>
          <p id="money-plus" class="money plus">${{income}}</p>
        </div>
        <div>
          <h4>Expense</h4>
          <p id="money-minus" class="money minus">${{expense}}</p>
        </div>
      </div>
</template>