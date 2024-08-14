<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpense from './components/IncomeExpense.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'
import { ref , computed , onMounted, watch } from 'vue'
import { useToast } from "vue-toastification";


const toast = useToast();

const transactions = ref([])

//Get total
const total = computed(()=>{
  return transactions.value.reduce((acc, item) => (acc += item.amount), 0).toFixed(2)
})

//Get income
const income = computed(()=>{
  return transactions.value
    .filter(item => item.amount > 0)
    .reduce((acc, item) => (acc += item.amount), 0)
    .toFixed(2)

})

//Get expense
const expense = computed(()=>{
  return transactions.value
    .filter(item => item.amount < 0)
    .reduce((acc, item) => (acc += item.amount), 0)
    .toFixed(2)
})

const handletransactionAdded = (transaction_data)=>{
  transactions.value.push({
    id: transactions.value.length + 1,
    text: transaction_data.text,
    amount: transaction_data.amount
  })
  toast.success("Transaction added successfully",{
    timeout:3000
  })
}
const handletransactionDeleted = (id)=>{
  transactions.value = transactions.value.filter(transaction => transaction.id !== id)
  toast.success("Transaction deleted successfully",{
    timeout:3000
  })
}

onMounted(()=>{
  const savedTransaction = JSON.parse(localStorage.getItem('transactions'))
  if(savedTransaction){
    transactions.value = savedTransaction
  }

})

const saveLocal = ()=>{
  localStorage.setItem('transactions',JSON.stringify(transactions.value))
}
watch(transactions, ()=>{
  saveLocal()
},{deep:true})

</script>

<template>
  <Header />
  <div class="container">
      <Balance :total="+total" />
      <IncomeExpense :income="+income" :expense="+expense" />
      <TransactionList @transactionDeleted="handletransactionDeleted" :transactions="transactions" />
      <AddTransaction @transactionAdded="handletransactionAdded" />

  </div>
</template>


