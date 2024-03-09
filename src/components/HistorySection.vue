<template>
    <div class="historycontainer">
        <h3>Histórico</h3>
            <hr class="horizontalline">
            <ul id="list" class="list">

                <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount<0? 'minus':'plus'" @mouseover="showBtn=true" @mouseleave="showBtn=true" >
                   
                    <button v-show="showBtn" @click="deleteTransaction(transaction.id)" class="deleteBtn">x</button>
                    <p>{{ transaction.text }}</p>
                    <span>  R${{ transaction.amount }}</span>
                    
                </li>
            </ul>
        </div>
</template>

<script setup>
    import { ref,defineProps, defineEmits} from 'vue';

    const emit = defineEmits(['transctionDeleted']);
    const showBtn = ref(false);
    const props = defineProps({
        transactions:{
            type:Array,
            required:true
        }
    });

    const deleteTransaction = (id)=>{
        emit('transactionDeleted',id)
    }    
    console.log(props)
    
</script>

<style scoped>
    .historycontainer{
        grid-column-start: 2;
        grid-row-start:4 ;
        margin: 10px;
        display: flex;
        flex-wrap: wrap;
        justify-items: center;
    }
    h3{
        margin: 10px 0px 0px 0px;
        text-align: left;
        flex-basis: 100%;
    }
    ul{
        
        margin: 35px 0px 10px 0px;
        list-style-type: none;
        padding: 0px;
        flex-basis: 100%;
        color: black;
    }
    li{
        display: flex;
        align-items: center;
        justify-content: space-between;
        background-color: white;
        margin-bottom: 10px;
        height: 30px;
        padding: 5px 10px 5px 10px;
        flex-basis: 100%;


    }
    .horizontalline{
        flex-basis: 100%;
        padding: 0px;
        margin: 0px 0px 0px 0px;
    }
    .deleteBtn{
        background-color: #F95A10;
        color: white;
        padding: 4px 8px 5px 8px;
        font-size: 15px;
        flex-basis: 1%;
        border-radius: 3px;
        border: 0px;
        justify-content: left;
    }
    p{
        display: flex;
        flex-basis: 40%;
    }
    span{
        display: flex;
        flex-basis: 50%;
        justify-content: right;
    }
    .plus{
        border-right: 7px solid #9FD356;
        border-radius: 2px;
    }
    .minus{
        border-right: 7px solid #F95A10;
        border-radius: 2px;
    }
    li:hover{
        background-color: #C6C6E7;
    }
</style>