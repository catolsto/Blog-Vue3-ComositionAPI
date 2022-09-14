
<template>
    <div>
        <div class="btn-group" role="group" aria-label="Basic example">
            <button @click="emitir('previo')" 
            :disabled = "props.inicio <= 0"
            class="btn btn-outline-primary">Anterior
            </button>
            <button @click="emitir('siguiente')" 
            :disabled = "props.fin >= props.tamano"
            class="btn btn-outline-primary">Siguiente
            </button>
        </div>
        <p>Paginas: {{props.inicio}} -  {{props.fin}}</p>
    </div>
</template>

<script setup>
    const props = defineProps(['inicio','fin','tamano'])
    const emitir = defineEmits(['siguiente','previo']);
</script>

<style lang="scss" scoped>

</style>