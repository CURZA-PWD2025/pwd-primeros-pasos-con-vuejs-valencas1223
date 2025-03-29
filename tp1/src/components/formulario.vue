<script setup lang="ts">
import { computed, reactive } from "vue";

interface Usuario {
  apynom: string;
  email: string;
  password: string;
  fechaNacimiento: string;
  calcularEdad: () => number;
}

const usuario = reactive<Usuario>({
  apynom: "",
  email: "",
  password: "",
  fechaNacimiento: "",

  calcularEdad: function (): number {
    if (!this.fechaNacimiento) return 0;
    const fechaNac = new Date(this.fechaNacimiento);
    const hoy = new Date();
    let edad = hoy.getFullYear() - fechaNac.getFullYear();
    const mesDiff = hoy.getMonth() - fechaNac.getMonth();
    if (mesDiff < 0 || (mesDiff === 0 && hoy.getDate() < fechaNac.getDate())) {
      edad--;
    }
    return edad;
  },
});

const edadUsuario = computed(() => usuario.calcularEdad());

const registrarUsuario = () => {
  if (!usuario.apynom || !usuario.email || !usuario.password || !usuario.fechaNacimiento) {
    alert("Por favor, completa todos los campos.");
    return;
  }

  
  console.log("Usuario registrado:", {
    apynom: usuario.apynom,
    email: usuario.email,
    edad: edadUsuario.value,
  });

  alert(
    `✔️ Usuario creado correctamente!\n\n Nombre: ${usuario.apynom}\n Email: ${usuario.email}\n Edad: ${edadUsuario.value} años`
  );

  usuario.apynom = "";
  usuario.email = "";
  usuario.password = "";
  usuario.fechaNacimiento = "";
};
</script>

<template>
  <div class="formulario">
    <h2>Crear Nuevo Usuario</h2>
    <form @submit.prevent="registrarUsuario">
      <label for="nombre">Nombre y apellido:</label>
      <input type="text" id="nombre" v-model="usuario.apynom" required />

      <label for="email">Email:</label>
      <input type="email" id="email" v-model="usuario.email" required />

      <label for="password">Contraseña:</label>
      <input type="password" id="password" v-model="usuario.password" required />

      <label for="fechaNacimiento">Fecha de Nacimiento:</label>
      <input type="date" id="fechaNacimiento" v-model="usuario.fechaNacimiento" required />

      <button type="submit">Crear Usuario</button>
    </form>
  </div>
</template>

<style scoped>
.formulario {
  max-width: 400px;
  margin: auto;
  padding: 20px;
  border-radius: 8px;
  background-color: #f9f9f9;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
}

form {
  display: flex;
  flex-direction: column;
}

label {
  color: black;
  font-weight: bold;
  margin-top: 10px;
}

input {
  padding: 8px;
  margin-bottom: 10px;
  border: 1px solid #be2d2d;
  border-radius: 4px;
}

button {
  background-color: rgb(15, 56, 56);
  color: white;
  padding: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  transition: background 0.3s;
}

button:hover {
  background: #be2d2d;
}

h2 {
  color: black;
}
</style>
