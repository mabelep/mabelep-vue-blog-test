<script setup>
import { ref } from 'vue';
import BlogPost from './components/BlogPost.vue';
import PaginatorBar from './components/PaginatorBar.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

const listaPosts = ref([]);
const tituloPostFavorito = ref('');
const tamanoPagina = 10;
const inicio = ref(0);
const fin = ref(tamanoPagina);
const loading = ref(true);
const nextPageBtnEnabled = ref(true);

const marcarFavorito = (title) => {
  tituloPostFavorito.value = title;
};

const next = () => {
  inicio.value += tamanoPagina;
  fin.value += tamanoPagina;
  if (inicio.value + tamanoPagina >= listaPosts.value.length) {
    nextPageBtnEnabled.value = false;
  }
};

const previous = () => {
  if (inicio.value >= tamanoPagina) {
    inicio.value -= tamanoPagina;
    fin.value -= tamanoPagina;
  }
  nextPageBtnEnabled.value = true;
};

const fetchData = async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts');
    listaPosts.value = await res.json();
  } catch (error) {
    console.error('Error en onMounted:', error);
  } finally {
    // Simulamos la carga inicial con timeout para mostrar el spinner
    setTimeout(() => (loading.value = false), 400);
  }
};

fetchData();
</script>

<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else="!loading">
    <h1>App de blog</h1>
    <h2>Mi post favorito: {{ tituloPostFavorito }}</h2>

    <PaginatorBar
      @nextPage="next"
      @prevPage="previous"
      :nextPageBtnEnabled="nextPageBtnEnabled"
      :prevPageBtnEnabled="inicio > 0"
      class="mb-2"
    />
    <BlogPost
      v-for="post in listaPosts.slice(inicio, fin)"
      :key="post.id"
      :id="post.id"
      :title="post.title"
      :body="post.body"
      @favoritoClick="marcarFavorito"
      class="mb-2"
    >
    </BlogPost>
  </div>
</template>
