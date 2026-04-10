<template>
    <div>
        <h3>Добавить фильма</h3>
    <input
        :value="title"
        @input="$emit('update:title',$event.target.value)"
    placeholder="Название"/>
    <input 
        :value="rating"
        @input="$emit('update:rating',$event.target.value)" 
        placeholder="Рейтинг(0-10)"/>
    <input 
        :value="year"
        @input="$emit('update:year',$event.target.value)"
        placeholder="Год"/>
  <button @click="$emit('add')">Добавить</button>
  
  <p v-if="error">{{error}}</p>

  <p v-if="filteredMovies.length === 0">Ничего не найдено</p>
  <ul v-else>
    <li v-for="movie in filteredMovies" :key="movie.id">
      {{movie.title}}
      {{movie.year}}
      {{movie.rating}}
      <button @click="$emit('toggle', movie)">{{movie.liked ? "❤":"🤍"}}</button>
      <button @click="$emit('remove', movie.id)">Удалить</button>
    </li>
  </ul>
    </div>
</template>

<script setup>
defineProps({
    title: String,
    year: String,
    rating: String,
    error: String,
    filteredMovies: Array
})

defineEmits([
    'update:title',
    'update:year',
    'update:rating',
    'add',
    'toggle',
    'remove'
])
</script>
