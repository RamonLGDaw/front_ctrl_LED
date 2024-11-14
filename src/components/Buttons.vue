<template>
    <div class="container-fluid d-flex flex-column justify-content-center align-items-center mx-0 p-5 bg-light">
        <h2>Funcionarà???</h2>
        <div class="container d-flex justify-content-center align-items-center m-auto mt-4 ">
            <button @click="enviarEstado('ON')" type="submit" class="btn btn-success m-3 fuente">ON</button>
            <button @click="enviarEstado('OFF')" type="submit" class="btn btn-danger m-3 fuente">OFF</button>
        </div>
    </div>
    <div class="container-fluid d-flex flex-column justify-content-center align-items-center mx-0 bg-light">
        <h3>El LED està: <span class="fuente2">{{ respuesta }}</span></h3>
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
import axios from 'axios';
import { ref } from 'vue';


let respuesta = ref(null)
let error = ref(null)

const enviarEstado = async(estado)=>{

    try {
        const response = await axios.post('https://conexion-led-python.vercel.app/led',{
            estado_led: estado
        });
        respuesta.value = response.data
        error.value = null
    } catch (err) {
        // Manejar errores
    respuesta.value = null; // Limpiar respuesta previa
    error.value = 'Hubo un error al enviar los datos: ' + err.message;
    }
}
</script>