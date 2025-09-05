<script setup>
defineProps({
  nextPageBtnEnabled: false,
  prevPageBtnEnabled: false,
});
const emit = defineEmits(['prevPage', 'nextPage']);
</script>
<template>
  <div class="btn-group" role="group" aria-label="Paginador de posts">
    <button
      type="button"
      class="btn btn-outline-primary"
      @click="emit('prevPage')"
      :disabled="!prevPageBtnEnabled"
    >
      Previous
    </button>
    <button
      type="button"
      class="btn btn-outline-primary"
      @click="emit('nextPage')"
      :disabled="!nextPageBtnEnabled"
    >
      Next
    </button>
  </div>
</template>
