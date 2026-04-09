<template>
    <div class="filter">
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

    <select v-model="SortBy">
        <option value="title">Сортировка: название</option>
        <option value="rating">Сортировка: рейтинг</option>
        <option value="year">Сортировка: год</option>
    </select>

    <button @click="resetFilter()">Сброс</button>
    </div>
</template>