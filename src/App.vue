<script setup>
import { ref, computed } from 'vue'

const categorias = ['Todos', 'Web', 'Móvil', 'Juegos']
const categoriaActiva = ref('Todos')

const proyectos = [
  { nombre: 'Tienda en línea', categoria: 'Web' },
  { nombre: 'Portal universitario', categoria: 'Web' },
  { nombre: 'App de delivery', categoria: 'Móvil' },
  { nombre: 'Juego de plataformas', categoria: 'Juegos' },
  { nombre: 'Recorrido virtual', categoria: 'Juegos' },
]

const proyectosFiltrados = computed(() =>
  categoriaActiva.value === 'Todos'
    ? proyectos
    : proyectos.filter((proyecto) => proyecto.categoria === categoriaActiva.value)
)

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
    <section class="proyectos">
      <h2>Proyectos</h2>
      <div class="proyectos-filtros">
        <button
          v-for="categoria in categorias"
          :key="categoria"
          :class="['proyectos-boton', { 'proyectos-boton-activo': categoria === categoriaActiva }]"
          @click="categoriaActiva = categoria"
        >
          {{ categoria }}
        </button>
      </div>
      <div class="proyectos-lista">
        <article v-for="proyecto in proyectosFiltrados" :key="proyecto.nombre" class="proyectos-tarjeta">
          <h3>{{ proyecto.nombre }}</h3>
          <span class="proyectos-categoria">{{ proyecto.categoria }}</span>
        </article>
      </div>
    </section>

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
