<script setup>
import { ref } from 'vue'
import {defineProps} from 'vue'


const props = defineProps({
  transactions: {
    type:Array,
    default:()=>[],
    required:true
  }
})

const emits = defineEmits(['transactionDeleted'])
const handleDelete = id =>{
  emits('transactionDeleted',id)
}


</script>

<template>
     <h3>History</h3>
      <ul id="list" class="list">
        <li :key="trans.id" v-for="trans in transactions" :class="trans.amount > 0 ? 'plus':'minus' ">
          {{ trans.text }} <span>${{ trans.amount }}</span>
          <button @click="handleDelete(trans.id)" class="delete-btn">x</button>
        </li>
      </ul>
</template>