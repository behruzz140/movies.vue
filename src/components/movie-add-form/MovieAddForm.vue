<template>
    <div class="movie-add-form">
        <h3>Yangi kino qo'shish</h3>
        <form class="add-form d-flex gap-3 flex-div " @submit.prevent="addMovie">


            <div class="input-container">
                <input type="text" class="new-movie-label mt-3" placeholder="" :value="name"
                    @input="name = $event.target.value">
                <label class="input-label mt-2">Film nomi</label>
            </div>

            <div class="input-container">
                <input type="text" class="new-movie-label mt-3" placeholder="" :value="viewers"
                    @input="viewers = $event.target.value">
                <label class="input-label mt-2">Ko'rilganlar soni</label>
            </div>

            <button class="btn btn-outline-dark mt-3" type="submit">Qo'shish</button>
        </form>
    </div>
</template>
<script>
export default {
    data() {
        return {
            name: '',
            viewers: '',
        }
    },
    methods: {



        addMovie() {
            if (!this.name || !this.viewers) return;

            const newMovie = {
                name: this.name,
                viewers: this.viewers,
                favourite: false,
                like: false,
                id: Date.now(),
            }
            this.$emit("createMovie", newMovie);
            this.name = '';
            this.viewers = '';
        }
    }
}
</script>
<style scoped>
.movie-add-form {
    margin-top: 2rem;
    padding: 2rem;
    background-color: #fcfaf5;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    position: relative;
}

h3 {
    font-family: 'Roboto', sans-serif;
    font-weight: 700;
    margin-bottom: 1.5rem;
    color: #004d40;
}

.add-form {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 1rem;
}

.input-container {
    position: relative;
    width: 40%;
}

.new-movie-label {
    width: 100%;
    padding: 0.75rem;
    border: 2px solid #004d40;
    border-radius: 5px;
    font-size: 1rem;
    transition: all 0.3s ease;
}

.new-movie-label:focus {
    border-color: #37ae37;
    outline: none;
}

.input-label {
    position: absolute;
    top: 50%;
    left: 10px;
    transform: translateY(-50%);
    font-size: 17px;
    color: #004d40;
    transition: all 0.3s ease;
    pointer-events: none;
}

.new-movie-label:focus+.input-label,
.new-movie-label:not(:placeholder-shown)+.input-label {
    top: -10px;
    left: 5px;
    font-size: 15px;
    color: #37ae37;
}

.btn-outline-dark {
    padding: 0.75rem 1.5rem;
    border: 2px solid #004d40;
    border-radius: 5px;
    background: transparent;
    color: #004d40;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
}

.btn-outline-dark:hover {
    background-color: #004d40;
    color: #fff;
}
</style>
