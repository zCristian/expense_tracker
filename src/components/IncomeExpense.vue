<template>
    <div class="in_exContainer">
        <div class="plusDiv">
            <h4>Entrada</h4>
            <p id="plus-money" class="plusMoney">R$+{{income}}</p>
        </div>
        <div class="verticalline"></div>
        <div class="minusDiv">
            <h4>Saída</h4>
            <p id="minus-money" class="minusMoney">R${{ expenses }}</p>
        </div>
    </div>
</template>

<script setup>
    
    import {defineProps} from 'vue';
    
    const props = defineProps({

        income:{
            type:Number,
            required:true
        },

        expenses:{
            type:Number,
            required:true
        },
    })
console.log(props.income)
</script>

<style scoped>
    .in_exContainer{
        grid-row-start: 3;
        grid-column-start: 2;
        display: flex;
        justify-items: center;
        align-items: center;
        justify-content: space-around;
        background-color: white;
        color:#342E37;
        margin:10px;
        font-size: 18px;
        border-radius: 3px;
    }
    .verticalline{
        border-left: 1px solid #220C10;
        height: 80%;
        display: flex;
        flex-basis: 1;
        
    }
    p{
        margin: 0px 0px 30px 0px;
        flex-basis: 100%;
    }
    h4{
        margin: 25px 0px 5px 0px;
        flex-basis: 100%;
    }
    .plusDiv{
        display: flex;
        flex-wrap: wrap;
        flex-basis: 49%;
    }
    .minusDiv{
        display: flex;
        flex-wrap: wrap;
        flex-basis: 49%;
    }
    .minusMoney{
        color: #F95A10;
    }
    .plusMoney{
        color:#9FD356;
    }
</style>