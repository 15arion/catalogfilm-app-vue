<script setup>

import {ref,computed} from 'vue'

const movies = ref([
  {id:1,title:"Чарли и шоколадная фабрика", year: 2012, rating:9.2, liked: false},
  {id:2,title:"Матрица", year: 2004, rating: 8.2, liked: false},
  {id:3,title:"Годзилла", year: 1999, rating:7.5, liked: false},
  {id:4,title:"Мстители", year: 2014, rating:9.9, liked: false},
])


const search = ref('');
const onlyLiked = ref(false);
const onlyNewer = ref(false);
const SortBy = ref('title');

const filteredMovies = computed(()=>{
  const q = search.value.toLowerCase()

  let list = movies.value
        .filter(m => m.title.toLowerCase().includes(q))
        .filter(m => !onlyNewer.value  || m.year > 2010)
        .filter(m=> !onlyLiked.value || m.liked)

  return list
})

function toggleLike(movie){
  movie.liked = !movie.liked;
}

</script>

<template>
 
<div>
  <h1>Каталог фильмов</h1>
  <p>
    Всего:  | Избранные: | Показано: 
  </p>

  <input type="text" placeholder="Поиск фильма" v-model="search">

  <label>
    <input type="checkbox" v-model="onlyLiked">Только избранные
  </label>

  <label>
    <input type="checkbox" v-model="onlyNewer" >Только после 2010
  </label>

  <select>
    <option>Сортировка: название</option>
    <option>Сортировка: рейтинг</option>
    <option>Сортировка: год</option>
  </select>

  <button>Сброс</button>

  <h3>Добавить фильма</h3>
  <input type="text" placeholder="Название">
  <input type="text" placeholder="Рейтинг(0-10)">
  <input type="text" placeholder="Год">
  <button>Добавить</button>

  <p v-if="filteredMovies.length ===0">Ничего не найдено</p>
  <ul v-else>
    <li v-for="movie in filteredMovies" :key="movie.id">
      {{movie.title}}
      {{movie.year}}
      {{movie.rating}}
      <button @click="toggleLike(movie)">{{movie.liked ? "❤":"🤍"}}</button>
    </li>
  </ul>
</div>

</template>

<style scoped>
</style>
