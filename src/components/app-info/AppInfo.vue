<template>

    <div class="nav-container ">
        <div ><img class="logo" src="../../../public/images.png" alt="disnep"></div>
        <div class="app-info">
            <p class="total-movies">Barcha kinolar soni: {{ allMoviesCount }}</p>
            <p class="favourite-movies">Ko'rilgan kinolar soni: {{ favouriteMoviesCount }}</p>
        </div>
    </div>

</template>

<script>
export default {
    props: {
        allMoviesCount: {
            type: Number,
            required: true,
        },
        favouriteMoviesCount: {
            type: Number,
            required: true,
        }
    }
}
</script>

<style scoped>

.nav-container {
    display: flex;
    align-items: center;
    margin-top: -50px;
    position: relative;
}

.app-info {
    position: sticky;
    top: 0;
    padding: 5px;
    margin-left: 240px;
    z-index: 23;
    padding: 1.5rem;
    border-radius: 8px;
    background-color: #ffffff;
    box-shadow: 2px 4px 8px 8px rgba(0, 0, 0, 0.1);
    width: 50%;
    text-align: center;
}

.total-movies {
    font-size: 1.25rem;
    font-weight: 600;
    color: #333;
    margin-bottom: 0.5rem;
}

.favourite-movies {
    font-size: 1.125rem;
    font-weight: 400;
    color: #666;
}
</style>
