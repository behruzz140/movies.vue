<template>
    <div class="search-panel">
        <input type="text" class="form-control search-input" placeholder="Kinolarni qidirish.. 🔎" :value="term"
            @input="changeHandler">
    </div>
</template>

<script>
export default {
    data() {
        return {
            term: '',
        }
    },
    methods: {
        changeHandler(e) {
            this.$emit('update:term', this.term)
            this.term = e.target.value
        }
    }
}
</script>

<style scoped>
/* .search-panel {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 17px;
    background:#1B4D3E;
    border: 1px solid #b0a895; 
    border-radius: 12px;
    box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.2), 0 4px 8px rgba(0, 0, 0, 0.2);
    font-family: cursive, serif;
} */
 

.search-input {
    width: 100%;
    padding: 1rem;
    font-size: 17px;
    color: #4a3a2b;
    background: #fff;
    border: 2px solid #4a3a2b;
    border-radius: 8px;
    box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

.search-input::placeholder {
    color: #8c7365;
    font-style: italic;
}

.search-input:focus {
    outline: none;
    background: #fff;
    border-color: #6b4f3e;
    box-shadow: inset 0 0 8px rgba(0, 0, 0, 0.2);
}
</style>
