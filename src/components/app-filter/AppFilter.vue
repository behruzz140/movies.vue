<template>
  <div class="btn-group">
    <button :class="{ 'btn-active': filter === 'all', 'btn-inactive': filter !== 'all' }" class="btn" type="button"
      @click='filterHandler("all")'>
      Barcha kinolar
    </button>
    <button :class="{ 'btn-active': filter === 'popular', 'btn-inactive': filter !== 'popular' }" class="btn"
      type="button" @click='filterHandler("popular")'>
      Mashhur kinolar
    </button>
    <button :class="{ 'btn-active': filter === 'mostViewers', 'btn-inactive': filter !== 'mostViewers' }" class="btn"
      type="button" @click='filterHandler("mostViewers")'>
      Eng ko'p ko'rilgan kinolar
    </button>
  </div>
</template>

<script>
export default {
  props: {
    updateFilterHandler: {
      type: Function,
      required: true,
    }
  },

  data() {
    return {
      filter: 'all',
    }
  },
  methods: {
    filterHandler(filter) {
      this.filter = filter;
      this.updateFilterHandler(this.filter);
    },
  },
}
</script>

<style scoped>
.btn-group {
  display: flex;
  gap: 0.5rem;
}

.btn {
  border: 1px solid transparent;
  border-radius: 4px;
  padding: 0.5rem 1rem;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-active {
  background-color: #004d40;
  color: #fff;
  border-color: #004d40;
}

.btn-inactive {
  background-color: #fff;
  color: #004d40;
  border-color: #004d40;
}

.btn-active:hover,
.btn-inactive:hover {
  opacity: 0.8;
}
</style>
