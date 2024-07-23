<template>
  <div class="app">
    <div class="content">
      <AppInfo :allMoviesCount="movies.length" :favouriteMoviesCount="movies.filter(c => c.favourite).length" />

      <div class="app-search-panel">
        <SearchPanel @update:term="updateTermHandler" />
        <AppFilter :updateFilterHandler="updateFilterHandler" class="filter-search-panel" />
      </div>

      <MovieList :movies="paginatedMovies" @onToggle="onToggleHandler" @onRemove="onRemoveHandler" />

      <div class="pagination-controls">
        <button @click="previousPage" :disabled="currentPage === 1">Previous</button>
        <span>Page {{ currentPage }} of {{ totalPages }}</span>
        <button @click="nextPage" :disabled="currentPage === totalPages">Next</button>
      </div>

      <MovieAddForm @createMovie="createMovie" />
    </div>
  </div>
</template>
<script>
import MovieAddForm from '@/components/movie-add-form/MovieAddForm.vue'
import MovieList from '@/components/movie-list/MovieList.vue'
import AppFilter from '@/components/app-filter/AppFilter.vue'
import SearchPanel from '@/components/search-panel/SearchPanel.vue'
import AppInfo from '@/components/app-info/AppInfo.vue'

export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm,
  },

  data() {
    return {
      movies: [
     
        { name: "A Beautiful Mind", viewers: 890, favourite: true, like: false, id: 4 },
        { name: "The Last Samurai", viewers: 723, favourite: false, like: true },
        { name: "The Great Gatsby", viewers: 342, favourite: false, like: true, id: 5 },
        { name: "Omar", viewers: 219, favourite: true, like: true, id: 1 },
        { name: "Empire of Osman", viewers: 546, favourite: false, like: false, id: 2 },
        { name: "Harry Poter", viewers: 693, favourite: true, like: false, id: 3 },
      ],
      term: '',
      filter: 'all',
      currentPage: 1,
      moviesPerPage: 4
    }
  },
  computed: {
    filteredMovies() {
      const filteredBySearch = this.onSearchHandler(this.movies, this.term);
      return this.onFilterHandler(filteredBySearch, this.filter);
    },
    totalPages() {
      return Math.ceil(this.filteredMovies.length / this.moviesPerPage);
    },
    paginatedMovies() {
      const start = (this.currentPage - 1) * this.moviesPerPage;
      const end = start + this.moviesPerPage;
      return this.filteredMovies.slice(start, end);
    }
  },
  methods: {




    createMovie(item) {
      this.movies.push(item);
    },
    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map(item => {
        if (item.id === id) {
          return { ...item, [prop]: !item[prop] };
        }
        return item;
      });
    },
    onRemoveHandler(id) {
      this.movies = this.movies.filter(c => c.id !== id);
    },
    onFilterHandler(arr, filter) {
      switch (filter) {
        case 'popular':
          return arr.filter(c => c.like);
        case 'mostViewers':
          return arr.filter(c => c.viewers > 500);
        default:
          return arr;
      }
    },
    onSearchHandler(arr, term) {
      if (term.length === 0) {
        return arr;
      }
      return arr.filter(c => c.name.toLowerCase().includes(term.toLowerCase()));
    },
    updateTermHandler(newTerm) {
      this.term = newTerm;
    },
    updateFilterHandler(newFilter) {
      this.filter = newFilter;
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage += 1;
      }
    },
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage -= 1;
      }
    }
  }
}
</script>


<style>
/* main styles */
.filter-search-panel{
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  
}


.app {
  height: 100vh;
  color: #000;
}

.content {
  width: 1000px;
  min-height: 700px;
  background: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}

.app-search-panel {
  width: 100%;
  margin-top: 15px;
  padding: 1.5rem;
  background: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}

/* end of main styles */
.pagination-controls {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 1rem;
  position: relative;
}

.pagination-controls button {
  margin: 0 0.5rem;
  padding: 0.5rem 1rem;
  border: 2px solid #007bff;
  background-color: transparent;
  color: #007bff;
  border-radius: 50%;
  cursor: pointer;
  transition: all 0.3s;
  position: relative;
}

.pagination-controls button:disabled {
  border-color: #d6d6d6;
  color: #d6d6d6;
  cursor: not-allowed;
}

.pagination-controls button:hover:not(:disabled) {
  background-color: #007bff;
  color: white;
}

.pagination-controls button::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 123, 255, 0.2);
  border-radius: 50%;
  transform: translate(-50%, -50%);
  transition: opacity 0.3s;
  opacity: 0;
}

.pagination-controls button:hover::before {
  opacity: 1;
}

.pagination-controls span {
  align-self: center;
  margin: 0 1rem;
  font-size: 1rem;
  font-weight: bold;
  color: #007bff;
}
</style>