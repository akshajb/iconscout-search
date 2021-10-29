<template>
  <div class="search-container mx-3">
    <form class="w-100 position-relative" @submit.prevent="searchIcons()">
      <div class="input-group">
        <input
          v-model="search"
          placeholder="Search from 3.6 Million+ assets"
          type="text"
          required
          class="form-control search-field"
        />
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: '',
    }
  },
  methods: {
    searchIcons() {
      this.$router.push({
        path: `/icons/${this.search.toLowerCase()}`,
      })
    },
  },
}
</script>

<style scoped>
.search-container {
  width: 420px;
}

.form-control {
  padding: 20px;
  font-size: 16px;
}

.search-field {
  padding-left: 2.5rem;
  padding-bottom: 22px;
  background-color: #ebedf5;
  border-color: #ebedf5;
  border-radius: 8px;
  background-image: url(https://cdna.iconscout.com/img/1d3df10.svg);
  background-repeat: no-repeat;
  background-position: 10px;
  transition: background-color 0.2s linear, border-color 0.2s linear;
}

.search-field:focus {
  box-shadow: none;
  background-color: #fff;
  border-color: #d8dbeb;
}
</style>
