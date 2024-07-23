<template>
    <div class="movie-list-container">
        <ul class="movie-list list-group">
            <li v-for="index in 4" :key="index" class="movie-list-item">
                <MovieListItem v-if="movies[index - 1]" :movie="movies[index - 1]" @onToggle="$emit('onToggle', $event)"
                    @onRemove="$emit('onRemove', $event)" />
                <div v-else class="placeholder">Kinolar topilmadi😢</div>
            </li>
        </ul>
    </div>
</template>

<script>
import MovieListItem from '../movie-list-item/movieListItem.vue';

export default {
    components: { MovieListItem },
    props: {
        movies: {
            type: Array,
            required: true,
        }
    }
}
</script>

<style scoped>
.movie-list-container {
    max-height: 420px;

    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
    display: flex;
    flex-direction: column;
}

.movie-list {
    list-style-type: none;
    padding: 0;
    margin: 0;
}

.movie-list-item {
    position: relative;
    padding: 5px;
    margin-bottom: 1rem;
    background: #fff;
    border-radius: 4px;
    box-shadow: 4px 4px 8px rgba(0, 0, 0, 0.15);
}

.placeholder {
    height: 72px;

    display: flex;
    align-items: center;
    justify-content: center;
    background: #f9f9f9;
    border: 1px dashed #ddd;
    border-radius: 4px;
    color: #888;
    font-size: 1rem;
}
</style>

