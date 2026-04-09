<script setup>

import {ref,computed} from 'vue'

const movies = ref([
  {id:1,title:"Чарли и шоколадная фабрика", year: 2012, rating:9.2, liked: false},
  {id:2,title:"Матрица", year: 2004, rating: 8.2, liked: false},
  {id:3,title:"Годзилла", year: 1999, rating:8.5, liked: false},
  {id:4,title:"Мстители", year: 2014, rating:9.9, liked: false},
])


const search = ref('')
const onlyLiked = ref(false)
const onlyNewer = ref(false)
const SortBy = ref('title')

const error = ref('')

const newTitle = ref('')
const newYear = ref('')
const newRating = ref('')

const filteredMovies = computed(()=>{
  const q = search.value.toLowerCase()

  let list = movies.value
        .filter(m => m.title.toLowerCase().includes(q))
        .filter(m => !onlyNewer.value  || m.year > 2010)
        .filter(m=> !onlyLiked.value || m.liked)
  
  if (SortBy.value ==='title'){
    list = [...list].sort((a,b) => a.title.localeCompare(b.title))
  }
   if (SortBy.value ==='year'){
    list = [...list].sort((a,b) => b.year-a.year)
  }
     if (SortBy.value ==='rating'){
    list = [...list].sort((a,b) => b.rating-a.rating)
  }
  
  return list
})

function toggleLike(movie){
  movie.liked = !movie.liked;
}

function removeMovie(id){
  movies.value = movies.value.filter(m => m.id!==id)
}

function addMovie(){
  error.value = ''
  if(!newTitle.value){
    error.value = "Введите название"
    return
  }

  const id = movies.value.length ===0 ? 1: movies.value.length + 1

  movies.value.push({
    id,
    title : newTitle.value,
    year: newYear.value,
    rating: newRating.value,
    liked: false
  })
  newTitle.value = ''
  newRating.value =''
  newYear.value =''
}
function resetFilter(){
  SortBy.value = 'title'
  search.value = ''
  onlyLiked.value = false
  onlyNewer.value = false
}

</script>

<template>
 
<div>
  <h3>Добавить фильма</h3>
  <input type="text" placeholder="Название" v-model="newTitle">
  <input type="text" placeholder="Рейтинг(0-10)" v-model="newRating">
  <input type="text" placeholder="Год" v-model="newYear">
  <button @click="addMovie()">Добавить</button>
  
  <p v-if="error">{{error}}</p>

  <p v-if="filteredMovies.length ===0">Ничего не найдено</p>
  <ul v-else>
    <li v-for="movie in filteredMovies" :key="movie.id">
      {{movie.title}}
      {{movie.year}}
      {{movie.rating}}
      <button @click="toggleLike(movie)">{{movie.liked ? "❤":"🤍"}}</button>
      <button @click="removeMovie(movie.id)">Удалить</button>
    </li>
  </ul>
</div>

</template>

<style scoped>
</style>
