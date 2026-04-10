<template>
    <div class="filter">
        <h1>Каталог фильмов</h1>
    <p>
        Всего:  | Избранные: | Показано: 
    </p>

    <input 
        :value="search" 
        @input="$emit('update:search', $event.target.value)" 
        placeholder="Поиск фильма"/>

    <label>
        <input type="checkbox"
        :checked = "onlyLiked"
        @change="$emit('update:onlyLiked',$event.target.checked)"/>
        Только избранные
    </label>

    <label>
        <input type="checkbox"
        :checked = "onlyNewer"
        @change="$emit('update:onlyNewer',$event.target.checked)"/>
        Только после 2010
    </label>

    <select :value="sortBy" 
    @change="$emit('update:sortBy',$event.target.value)">
        <option value="title">Сортировка: название</option>
        <option value="rating">Сортировка: рейтинг</option>
        <option value="year">Сортировка: год</option>
    </select>

    <button @click="$emit('reset')">Сброс</button>
    </div>
</template>

<script setup>

defineProps({
    search: String,
    onlyLiked: Boolean,
    onlyNewer: Boolean,
    sortBy: String
})

defineEmits([
    'update:search',
    'update:onlyLiked',
    'update:onlyNewer',
    'update:sortBy',
    'reset'
])
</script>
