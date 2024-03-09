<template>
    <h4>Seu saldo</h4>
    <h1 id="balance">R${{ total }}</h1>
</template>

<script setup>
    import { defineProps } from 'vue';

    const props = defineProps({

        total:{
            type:Number,
            required:true
        },

    });
    console.log(props)
</script>

<style scoped>
h4{
    text-align: left;
    grid-column-start: 2;
    grid-row-start: 2;
    margin : 10px;
}
h1{
    text-align: left;
    margin:30px 10px 10px 10px;
    grid-column-start: 2;
    grid-row-start: 2;
    
}
</style>