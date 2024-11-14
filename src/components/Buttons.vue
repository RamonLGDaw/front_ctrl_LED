<template>
    <div class="container-fluid d-flex flex-column justify-content-center align-items-center mx-0 p-5 bg-light">
        <h2>Funcionarà??? Quin misteri...</h2>
        <div class="container d-flex justify-content-center align-items-center m-auto mt-4 ">
            <button @click="mostrarON()" type="button" class="btn btn-success m-3 fuente">ON</button>
            <button @click="mostrarOFF()" type="button" class="btn btn-danger m-3 fuente">OFF</button>
        </div>
    </div>
    <div class="container-fluid d-flex flex-column justify-content-center align-items-center mx-0 bg-light">
        <h3>El LED està: <span class="fuente2">{{ estado_led }}</span></h3>
        <div class="container d-flex justify-content-center align-items-center m-auto mt-3 ">
            
        </div>

    </div>


</template>

<style scoped>
.fuente2{
    font-family:cursive;
    color: rgb(36, 13, 164);
   
}
.fuente{
    font-family:cursive;
   
}
</style>

<script setup>
import { ref } from 'vue';

let estado_led = ref(' OFF')

function mostrarON(){
    console.log('funciona ==> ON')
    estado_led.value = '  ON... !!'

}

const mostrarOFF = () =>{
    console.log('funciona ==> OFF')
    estado_led.value = '  OFF... !!'
}
</script>