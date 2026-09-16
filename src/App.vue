<script setup>
import { ref } from 'vue'

const formulario = ref({ nombre: '', correo: '', mensaje: '' })
const estado = ref('')

function enviarFormulario() {
  const { nombre, correo, mensaje } = formulario.value
  if (!nombre.trim() || !correo.trim() || !mensaje.trim()) {
    estado.value = 'error'
    return
  }
  estado.value = 'enviado'
  formulario.value = { nombre: '', correo: '', mensaje: '' }
}
</script>

<template>
  <header class="encabezado">
    <h1>PR_Testing</h1>
    <p class="subtitulo">Repositorio oficial de BolivianWorks</p>
  </header>

  <main class="contenido">
    <section class="contacto">
      <h2>Contacto</h2>
      <form class="contacto-formulario" @submit.prevent="enviarFormulario">
        <label>
          Nombre
          <input v-model="formulario.nombre" type="text" />
        </label>
        <label>
          Correo
          <input v-model="formulario.correo" type="email" />
        </label>
        <label>
          Mensaje
          <textarea v-model="formulario.mensaje" rows="4"></textarea>
        </label>
        <button type="submit" class="contacto-boton">Enviar</button>
      </form>
      <p v-if="estado === 'error'" class="contacto-error">Completa todos los campos.</p>
      <p v-if="estado === 'enviado'" class="contacto-exito">¡Mensaje enviado! Gracias por escribirnos.</p>
    </section>
  </main>
</template>
