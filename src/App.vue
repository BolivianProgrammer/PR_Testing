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
  </main>
</template>
