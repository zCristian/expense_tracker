<template>
    <div class="addSection">
        <h3>Nova Transação</h3>
        <hr class="horizontalline">
        <form id="form" @submit.prevent="onAdd">
            <div class="formSection">
                <label for="text">Texto</label>
                <input type ="text" id="text" placeholder="" v-model="text">
            </div>
            <div class="formSection">
                <label for="amount">Valor</label>
                <input type="text" id="amount" placeholder="" v-model="amount">
            </div>
            <button class="btn">Adicionar</button>
        </form>
    </div>
</template>

<script setup>
    import {ref, defineEmits} from 'vue';
    import { useToast } from 'vue-toastification';
    const text = ref('');
    const amount = ref('');


    const toast = useToast();
    const emit = defineEmits(['transactionAdded']);


    const onAdd=()=>{
        if(!text.value || !amount.value){
            toast.error('Os campos devem ser preenchidos!')
            return;
        }

        const transactionData = {
            text: text.value,
            amount: parseFloat(amount.value)
        }

        emit('transactionAdded', transactionData);

        text.value='';
        amount.value='';
    };

        
</script>

<style scoped>
    .addSection{
        grid-row-start: 5;
        grid-column-start: 2;
        margin: 10px 10px 10px 10px;
    }
    
    h3{
        
        text-align: left;
        margin: 10px 0px 0px 0px;
    }
    .horizontalline{
        flex-basis: 100%;
        padding: 0px;
        margin: 0px 0px 0px 0px;
    }

    form{
        margin-top: 20px;
        text-align: left;
    }
    .formSection{
        display: flex;
        margin-bottom: 20px;
        flex-wrap: wrap;
    }
    input{
        font-size: 15px;
        flex-basis: 100%;
        height: 25px;
        border-width: 1px;
        border: 1 solid black;
        border-radius: 2px;
        box-shadow: none;
    }
    .btn{
        width: 100%;
        height: 35px;
        background-color: #4949AB;
        box-shadow: none;
        border-style: none;
        color: #F4F6F6;
        font-size: 18px;
        font-weight:600 ;
        appearance: none;
        border-radius: 1px;
    }
</style>