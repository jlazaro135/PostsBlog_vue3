<script setup>


defineProps({
    id: Number,
    title: {
        type: String,
        default: 'Título por default'
    },
    body: {
        type: String,
        default: 'Descripción por default'
    }
})

const emit = defineEmits(['cambiarFavoritoEvento'])
</script>

<template>
<div class="card">
    <div class="card-body">
        <div class="card-title">
            <h2>{{id}}-{{title}}</h2>
        </div>
        <p>{{body}}</p>
        <button @click="emit('cambiarFavoritoEvento', title)" class="btn btn-outline-primary">Favorito</button>
    </div>
</div>
</template>

<style scoped>
</style>