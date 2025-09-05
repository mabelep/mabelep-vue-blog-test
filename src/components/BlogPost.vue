<script setup>
defineProps({
    title: {
        type: String,
    },
    id: {
        type: Number,
    },
    body: {
        type: String,
        default: 'Contenido por defecto',
    },
});
const emit = defineEmits(['favoritoClick']);
</script>

<template>
    <div class="container">
        <div class="card">
            <div class="card-body">
                <div class="card-title title">{{ id }} - {{ title }}</div>
                <p>{{ body }}</p>
                <button
                    @click="emit('favoritoClick', title)"
                    class="btn btn-outline-primary"
                >
                    ⭐ Favorito
                </button>
            </div>
        </div>
    </div>
</template>

<style scoped>
.title {
    font-weight: bold;
    font-size: 1rem;
}

</style>
