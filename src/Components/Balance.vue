<script setup>
import {defineProps} from 'vue'


const props = defineProps({
  total: {
    type:Number,
    default:0.00,
    required:true
  }
})
</script>
<template>
       <h4>Your Balance</h4>
      <h1 id="balance">${{total}}</h1>
</template>