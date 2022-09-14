
<template>
<div class="card mt-2">
  <div class="card-body">
    <h5 class="card-title">{{id}} - {{title}}</h5>
    <p class="card-text">{{body}}</p>
    <button 
        @click="emitir('cambiarFavoritoNombre',title)" 
        class="btn btn-outline-primary">
        <i class="fa fa-heart"></i>  Marcar como Favorito
    </button>
  </div>
</div>
</template>

<script setup>
import { ref } from "vue";

    const props = defineProps({
        title: String,
        id: Number,
        body: {
            type: String,
            default: 'Aún no tiene contenido el texto!'
        }
    })

    const emitir = defineEmits(['cambiarFavoritoNombre']);

</script>

<style lang="scss" scoped>

</style>