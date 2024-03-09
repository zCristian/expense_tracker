<template>
  <div class="content">
    <BaseHeader/>
    <BalanceSection :total="total"/>
    <IncomeExpense :income="+income" :expenses="+expenses"/>
    <HistorySection @transactionDeleted="handleTransactionDeleted" :transactions="transactions"/>
    <AddTransaction @transactionAdded=" handleTransactionAdded"/>
  </div>
</template>

<script setup>
import BaseHeader  from './components/BaseHeader';
import AddTransaction from './components/AddTransaction';
import BalanceSection from './components/BalanceSection.vue';
import HistorySection from './components/HistorySection.vue'
import IncomeExpense from './components/IncomeExpense.vue';

import {ref,computed, onMounted} from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast();

const transactions= ref([]);

onMounted(()=>{
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if(savedTransactions){
     transactions.value = savedTransactions;
  }
})

const total = computed(()=>{
  return transactions.value.reduce((acc, transaction)=>{
    return acc + transaction.amount;
  },0);
});

const income = computed(()=>{
    return transactions.value.filter((transaction)=>transaction.amount>0)
        .reduce((acc,transaction)=>{
          return acc + transaction.amount;
        },0).toFixed(2);
});


const expenses = computed(()=>{
    return transactions.value.filter((transaction)=>transaction.amount<0)
        .reduce((acc,transaction)=>{
          return acc + transaction.amount;
        },0).toFixed(2);
});

const handleTransactionAdded = (transactionData) =>{
  transactions.value.push({
    id:generateId(),
    text:transactionData.text,
    amount:transactionData.amount,
    showBtn:false
  });
  savedTransactionsToLocalStorage();

  toast.success('Operação adicionada')
};

const generateId=() =>{
  return Math.floor(Math.random()*1000)
};

const handleTransactionDeleted= (id)=>{
  transactions.value = transactions.value.filter((transaction)=>
  transaction.id !== id);
  savedTransactionsToLocalStorage();

  toast.success("Operação removida");
};


const savedTransactionsToLocalStorage = () =>{
  localStorage.setItem('transactions', JSON.stringify(transactions.value));

}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap');
  @media screen and (max-width: 900px){
      .content{
      text-align: center;
      font-family: Roboto;
      display:inline-grid;
      grid-template-columns: [first] 15% [second] 70% [third] 15%;
      grid-template-rows: [first] 60px [second] 80px  [third] 100px  [fourth] auto [fifth] 270px; 
      margin: 0;
      width: 100%;
      color: #342E37;
    }
  }

  @media screen and (min-width: 950px){
      .content{
      text-align: center;
      font-family: Roboto;
      display:inline-grid;
      grid-template-columns: [first] 35% [second] auto [third] 35%;
      grid-template-rows: [first] 60px [second] 80px  [third] 100px  [fourth] auto [fifth] 270px; 
      margin: 0;
      width: 100%;
      color: #342E37;
    }
  }

  
  
</style>