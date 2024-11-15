<template>
    <div class="container-fluid d-flex flex-column justify-content-center align-items-center mx-0 p-5 bg-light">
      <h2>Funcionarà???</h2>
      <p>Petición fetch</p>
      <div class="container d-flex justify-content-center align-items-center m-auto mt-4 ">
        <button @click="enviarEstado('ON')" type="submit" class="btn btn-success m-3 fuente">ON</button>
        <button @click="enviarEstado('OFF')" type="submit" class="btn btn-danger m-3 fuente">OFF</button>
      </div>
    </div>
    <div class="container-fluid d-flex flex-column justify-content-center align-items-center mx-0 bg-light">
      <h3>El LED està: <span class="fuente2">{{ respuesta }}</span></h3>
      <p v-if="error" class="text-danger">{{ error }}</p> <!-- Mostrar mensaje de error -->
    </div>
  </template>
  
  <style scoped>
  .fuente2 {
    font-family: cursive;
    color: rgb(36, 13, 164);
  }
  
  .fuente {
    font-family: cursive;
  }
  </style>

  <script setup>
  import { ref } from 'vue';
  
  // Definir las referencias reactivas
  const respuesta = ref(null);
  const error = ref(null);
  
  // Función para enviar el estado del LED
  const enviarEstado = async (estado) => {
    try {
      // Usamos fetch para enviar la solicitud POST
      const response = await fetch('http://127.0.0.1:8000/led', {
        method: 'POST',
        headers: {
          'Content-Type': 'text/plain',  // Aseguramos que enviamos un string
        },
        body: estado,  // Enviamos el estado directamente como string
      });
  
      if (!response.ok) {
        throw new Error(`Error: ${response.statusText}`);
      }
  
      // Si todo sale bien, procesamos la respuesta
      const data = await response.text();  // Recibimos la respuesta como texto
      respuesta.value = data;
      error.value = null;
    } catch (err) {
      // Si ocurre un error, lo mostramos
      respuesta.value = null; // Limpiar respuesta previa
      error.value = 'Hubo un error al enviar los datos: ' + err.message;
    }
  };
  </script>
  