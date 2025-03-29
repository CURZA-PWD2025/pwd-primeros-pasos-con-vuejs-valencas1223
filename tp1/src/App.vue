<script setup lang="ts">
import { ref } from "vue";
import FormularioUsuario from "./components/formulario.vue";

interface Usuario {
  nombre: string;
  email: string;
  edad: number | string;
}

const usuarios = ref<Usuario[]>([]);
const agregarUsuario = (usuario: Usuario) => {
  usuarios.value.push(usuario);
};


const curzita_foto = ref("/curza.jpg");
</script>

<template>
  <div :style="{ backgroundImage: `url(${curzita_foto})` }" class="container">
    <h1>Formulario</h1>
    <FormularioUsuario @usuario-creado="agregarUsuario" />

    <div v-if="usuarios.length" class="usuarios-registrados">
      <h2>Usuarios Registrados</h2>
      <ul>
        <li v-for="(usuario, index) in usuarios" :key="index">
          <strong>{{ usuario.nombre }}</strong> - {{ usuario.email }} -  {{ usuario.edad }} años
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh; 
  
  background-size: 100% 100%; 
  background-position: center; 
  background-repeat: no-repeat; 

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: white;
  text-shadow: 1px 1px 5px black;
  padding: 20px;
}

.usuarios-registrados {
  margin-top: 20px;
  padding: 10px;
  background: rgba(255, 255, 255, 0.8); 
  border-radius: 8px;
  color: black;
}

h2 {
  color: black;
}
</style>
