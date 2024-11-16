<template>
    <div class="container-fluid d-flex flex-column justify-content-center align-items-center mx-0 p-5 bg-light">
      <h2>Opció 1</h2>

      <div class="container d-flex justify-content-center align-items-center m-auto mt-4 ">
        <button @click="enviarEstado('ON')" type="submit" class="btn btn-success m-3 fuente">ON</button>
        <button @click="enviarEstado('OFF')" type="submit" class="btn buttonRed m-3 fuente">OFF</button>
      </div>
    </div>
    <div class="container-fluid d-flex flex-column justify-content-center align-items-center mx-0 bg-light">
      <h3 class="fuente2">{{ respuesta }}</h3>
      <p v-if="error" class="text-danger">{{ error }}</p> <!-- Mostrar mensaje de error -->
    </div>
    <div class="container-fluid d-flex flex-column justify-content-center align-items-center mx-0 p-5 bg-light">
        <h2>Opció 2</h2>
        <div>
            <label class="switch m-5">
                <input type="checkbox" v-model="estadoSwitch" @change="enviarEstadoSwitch">
                <span class="slider round"></span>
            </label>
        </div>
    </div>
    <div class="container-fluid d-flex flex-column justify-content-center align-items-center mx-0 bg-light">
      <h3 class="fuente2">{{ respuesta }}</h3>
      <p v-if="error" class="text-danger">{{ error }}</p> <!-- Mostrar mensaje de error -->
    </div>
  </template>
  
  

  <script setup>
  import { ref } from 'vue';
  

  const respuesta = ref(null);
  const error = ref(null);
  const estadoSwitch = ref(false);  

  // Función para enviar el estado del LED
  const enviarEstado = async (estado) => {
    try {
      // Usamos fetch para enviar la solicitud POST
      const response = await fetch('https://back-ctrl-led.vercel.app/led', {
        method: 'POST',
        headers: {
          'Content-Type': 'text/plain',  
        },
        body: estado,  
      });
  
      if (!response.ok) {
        throw new Error(`Error: ${response.statusText}`);
      }
  
     
      const data = await response.text();  
      respuesta.value = data;
      error.value = null;
    } catch (err) {
      
      respuesta.value = null; // Limpiar respuesta previa
      error.value = 'Hubo un error al enviar los datos: ' + err.message;
    }
  };

  // Función para enviar el estado del LED desde el interruptor
const enviarEstadoSwitch = async () => {
  try {
    // El estado del switch es true (ON) o false (OFF)
    const estado = estadoSwitch.value ? 'ON' : 'OFF';
    
    const response = await fetch('https://back-ctrl-led.vercel.app/led', {
      method: 'POST',
      headers: {
        'Content-Type': 'text/plain',
      },
      body: estado,
    });

    if (!response.ok) {
      throw new Error(`Error: ${response.statusText}`);
    }

    const data = await response.text();
    respuesta.value = data;
    error.value = null;
  } catch (err) {
    respuesta.value = null;
    error.value = 'Hubo un error al enviar los datos: ' + err.message;
  }
};
  </script>

<style scoped>
.buttonRed{
  color: white;
  background-color: #e51b1b;
}
.fuente2 {
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
  color: rgb(36, 13, 164);
}

.fuente {
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}

/* The switch - the box around the slider */
.switch {
position: relative;
display: inline-block;
width: 60px;
height: 34px;
}

/* Hide default HTML checkbox */
.switch input {
opacity: 0;
width: 0;
height: 0;
}

/* The slider */
.slider {
position: absolute;
cursor: pointer;
top: 0;
left: 0;
right: 0;
bottom: 0;
background-color: #e51b1b;
-webkit-transition: .4s;
transition: .4s;
}

.slider:before {
position: absolute;
content: "";
height: 26px;
width: 26px;
left: 4px;
bottom: 4px;
background-color: white;
-webkit-transition: .4s;
transition: .4s;
}

input:checked + .slider {
background-color: #198754;
}

input:focus + .slider {
box-shadow: 0 0 1px #3cf418;
}

input:checked + .slider:before {
-webkit-transform: translateX(26px);
-ms-transform: translateX(26px);
transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
border-radius: 34px;
}

.slider.round:before {
border-radius: 50%;
} 
</style>
  