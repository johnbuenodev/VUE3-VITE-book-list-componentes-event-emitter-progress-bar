<script setup>

import { onMounted, computed, onUpdated, ref, reactive } from 'vue'

//criando o props
const props = defineProps(['items']);

let widthDoneTrue = reactive({'value': 0});
// widthDoneTrue.value = receber novo valor

//Se as variaveis que fazem parte da computed forem atualizadas vai ser re-calculado
const itemsDone = computed(() => {
  //resumido   return courses.filter(item => item.done).length; ele já verifica se o done é true. se não tiver nada é false
  //No codigo javascript precisa add o props.nome-definido
  return props.items.filter(item => item.isRead === true).length;
});

onUpdated(() => {
  console.log("Cycle Updated");
//   widthDoneTrue.value = props.items.filter(item => item.isRead === true).length;
});

onMounted(() => {
  console.log("Cycle Mounted");
//   widthDoneTrue.value = props.items.filter(item => item.isRead === true).length;
});

</script>

<template>

    <!-- No template não precisa a necessidade de add props.nome-definido --> 

    <span>Progress ({{ itemsDone }} / {{ items.length }})</span>

    <br>

    <progress :value="itemsDone" :max="items.length"></progress>
  
</template>

<style>
 .progressContainer {

 }
 .progressBar {
    border:1px solid gray; 
    /* position: relative; */
    /* overflow: hidden; */
    display: flex;
    flex-direction: row;
    height: 26px;
    align-self: flex-start;
    background-color: red;
    position: absolute;
 }
 .progressValue {
    background-color: rgb(73, 37, 156);
    display: flex; 
    flex-direction: row;
    align-self: flex-start;
    height: 26px;
    position: absolute; 
 }
</style>