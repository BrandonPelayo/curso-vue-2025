<script setup>
defineProps({
  titulo: String,
  contenido: String,
  imagen: String,
})
</script>

<template>
  <br />
  <div class="card card-text" style="width: 18rem">
    <img :src="imagen" class="card-img-top" alt="Imagen" />
    <div class="card-body">
      <h5 class="card-title">{{ titulo }}</h5>
      <p class="card-text">{{ contenido }}</p>
      <a href="#" class="btn btn-primary">Go somewhere</a>
    </div>
  </div>
</template>

<style scoped>
.card-text {
  overflow: hidden;

  /* Evita el desbordamiento en una sola línea */
  max-width: 100%; /* Asegura que respete el tamaño del contenedor */
}
</style>
