
<template>
  <CargandoSpinner v-if="cargando"/>
  <div v-else class="container mt-5" >

    <h2>Mi Post Favorito: {{favorito}}</h2>
    <hr>
    <h2>Lista de Post</h2>

    <PaginatePost class="mb-3" 
      :inicio="inicio"
      :fin="fin"
      :tamano="posts.length"
      @siguiente="siguiente" 
      @previo="previo" 
    />

    <BlogPost v-for="post in posts.slice(inicio,fin)" :key="post.id"
      :title="post.title" 
      :id="post.id"
      :body="post.body"
      @cambiarFavoritoNombre="cambiarFavorito"
    />

  </div>
</template>


<script setup>
  import { ref, computed, onMounted } from "vue";
  import BlogPost from "./components/BlogPost.vue";
  import PaginatePost from "./components/PaginatePost.vue";
  import CargandoSpinner from "./components/CargandoSpinner.vue";

  const posts = ref([])
  const favorito = ref('')
  const cargando = ref(true)

  // para la paginacion
  const postxpagina = 10
  const inicio = ref(0)
  const fin = ref(postxpagina)

  const cambiarFavorito = (title) => {
    favorito.value = title
  }

  const siguiente = () => {
    if (fin.value < 100) {
      inicio.value = inicio.value + postxpagina
      fin.value = fin.value + postxpagina
    }
    else {
      alert ('NO hay mas elementos!')
    }
  }

  const previo = () =>  {
    if (inicio.value > 0) {
      inicio.value = inicio.value - postxpagina
      fin.value  = fin.value  - postxpagina 
    } else {
      alert ('NO hay mas elementos!')
    }
  }

  onMounted(async()=> {
    try {
        const res = await fetch('https://jsonplaceholder.typicode.com/posts');
        posts.value = await res.json();
    } catch (error) {
        console.log(error);
    } finally {
        cargando.value = false;
    }
  })

/*     fetch('https://jsonplaceholder.typicode.com/posts')
      .then( res => res.json())
      .then( data => { posts.value = data })
      .catch((e) => { console.log(e);})
      .finally(() => { cargando.value = false } ) */
  
</script>

