<script setup>
import {ref, computed, onMounted} from 'vue';
import BlogPost from './components/BlogPost.vue';
import Pager from './components/Pager.vue';
import Spinner from './components/Spinner.vue';

const posts = ref([])
const postXPage = 10
const inicio = ref(0)
const fin = ref(postXPage)
const loading = ref(true)

const favorito = ref("")

function next(){
  inicio.value += postXPage
  fin.value += postXPage
}

function previous(){
  inicio.value += -postXPage
  fin.value += -postXPage
}

const cambiarFavorito = (title) => {
  favorito.value = title
}

const maxLength = computed(() => posts.value.length)

async function fetchData(){
  try{
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    const data = await res.json()
    posts.value = data
    loading.value = false
  }catch{

  }
}

onMounted(fetchData())

</script>

<template>
  <Spinner class="mt-5" v-if="loading"></Spinner>
  <div class="container" v-else>
    <h2>Mi post favorito: {{favorito}}</h2>

    <Pager class="mb-2" @next="next" @prev="previous" :inicio="inicio" :fin="fin" :maxLength="maxLength"></Pager>

    <BlogPost
    v-for="post in posts.slice(inicio, fin)"
    :key="post.id"
    :title="post.title"
    :id="post.id"
    :body="post.body"
    @cambiarFavoritoEvento="cambiarFavorito"
    class="mb-2"
    ></BlogPost>
  </div>
</template>

<style scoped>

</style>
