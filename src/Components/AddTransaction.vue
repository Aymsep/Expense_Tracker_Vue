<script setup>
import { ref } from 'vue'
import { useToast } from "vue-toastification";


const toast = useToast();
const text = ref('')
const amount = ref(0)

const emit  = defineEmits(['transactionAdded'])

const onSubmit = e =>{
  if(!text.value || !amount.value){
    toast.warning("Please add a text and amount",{
      timeout:3000
    })
    return
  }
  const transaction_data = {
    text: text.value,
    amount: +amount.value
  }
  emit('transactionAdded',transaction_data)
  text.value = ""
  amount.value = 0

}

</script>

<template>
    <h3>Add new transaction</h3>
      <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
          <label for="text">Text</label>
          <input v-model="text" type="text" id="text" placeholder="Enter text..." />
        </div>
        <div class="form-control">
          <label for="amount"
            >Amount <br />
            (negative - expense, positive - income)</label
          >
          <input v-model="amount" type="text" id="amount" placeholder="Enter amount..." />
        </div>
        <button class="btn">Add transaction</button>
      </form>
</template>