<script setup lang="ts">
import { ref, reactive } from 'vue'

const usuario = reactive({
  nombre: '',
  email: '',
  contrasena: '',
  fechaNacimiento: '',
})

const mostrarDatos = ref(false)

const calcularEdad = () => {
  if (!usuario.fechaNacimiento) return ''
  const nacimiento = new Date(usuario.fechaNacimiento)
  const hoy = new Date()
  let edad = hoy.getFullYear() - nacimiento.getFullYear()
  const mes = hoy.getMonth() - nacimiento.getMonth()
  if (mes < 0 || (mes === 0 && hoy.getDate() < nacimiento.getDate())) {
    edad--
  }
  return edad
}

const crearUsuario = () => {
  alert(`Usuario creado con éxito:
  Nombre: ${usuario.nombre}
  Email: ${usuario.email}
  Edad: ${calcularEdad()} años`)
  mostrarDatos.value = true
  limpiarFormulario()
}

const limpiarFormulario = () => {
  usuario.nombre = ''
  usuario.email = ''
  usuario.contrasena = ''
  usuario.fechaNacimiento = ''
}
</script>

<template>
  <div id="app">
    <h1>Crear Nuevo Usuario</h1>
    <form @submit.prevent="crearUsuario">
      <label>
        Nombre de usuario:
        <input type="text" v-model="usuario.nombre" />
      </label>
      <label>
        Correo electrónico:
        <input type="email" v-model="usuario.email" />
      </label>
      <label>
        Contraseña:
        <input type="password" v-model="usuario.contrasena" />
      </label>
      <label>
        Fecha de nacimiento:
        <input type="date" v-model="usuario.fechaNacimiento" />
      </label>
      <button type="submit">Crear Usuario</button>
    </form>

    <div v-if="mostrarDatos">
      <h2>Datos del Usuario</h2>
      <p>Nombre: {{ usuario.nombre }}</p>
      <p>Email: {{ usuario.email }}</p>
      <p>Edad: {{ calcularEdad() }} años</p>
    </div>
  </div>
</template>


<style scoped>
/* Estilos generales */
.contenedor {
  max-width: 400px;
  margin: auto;
  padding: 20px;
  background: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  text-align: center;
}

/* Títulos */
h1 {
  color: #333;
  font-size: 1.5rem;
}

/* Formularios */
form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-top: 20px;
}

label {
  font-weight: bold;
  color: #555;
}

input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 1rem;
}

/* Botón */
button {
  background-color: #ff69b4;
  color: white;
  font-size: 1rem;
  padding: 10px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background 0.3s;
}

button:hover {
  background-color: #d14792;
}

/* Datos del usuario */
.datos-usuario {
  margin-top: 20px;
  padding: 15px;
  background: #fff;
  border-radius: 8px;
  box-shadow: 0px 3px 8px rgba(0, 0, 0, 0.1);
}

p {
  font-size: 1rem;
  color: #444;
}
</style>


