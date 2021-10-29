<template>
  <div class="filter d-flex">
    <div class="tabs d-flex align-items-baseline">
      <button
        class="filter-btn d-flex justify-content-between align-items-center"
        type="button"
        @click="toggleFilter()"
      >
        <span>
          <img
            class="mr-2"
            src="https://cdna.iconscout.com/img/ab9bae8.svg"
            alt=""
            width="24"
          />
          <span>Filters</span>
        </span>
        <span v-if="filter">
          <a href="#" class="no-hover text-dark">
            <svg
              width="20"
              height="20"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
              fill="currentColor"
              class="ui-svg-inline"
            >
              <path
                d="M13.41,12l4.3-4.29a1,1,0,1,0-1.42-1.42L12,10.59,7.71,6.29A1,1,0,0,0,6.29,7.71L10.59,12l-4.3,4.29a1,1,0,0,0,0,1.42,1,1,0,0,0,1.42,0L12,13.41l4.29,4.3a1,1,0,0,0,1.42,0,1,1,0,0,0,0-1.42Z"
              ></path>
            </svg>
          </a>
        </span>
      </button>
      <div class="custom-tab-indicators d-flex">
        <ul class="custom-tabs">
          <li>
            <NuxtLink to="/icons">Icons</NuxtLink>
          </li>
          <li>
            <a href="#">All Assets</a>
          </li>
          <li>
            <a href="#">3D Illustrations</a>
          </li>
          <li>
            <a href="#">Lottie Animations</a>
          </li>
          <li>
            <a href="#">Illustrations</a>
          </li>
        </ul>
      </div>
    </div>
    <div class="sort d-flex"></div>
  </div>
</template>

<script>
export default {
  props: {
    count: {
      type: Number,
      default: () => 0,
      required: true,
    },
  },
  data() {
    return { filter: false }
  },
  methods: {
    toggleFilter() {
      this.filter = !this.filter
      this.$emit('filterToggled', this.filter)
    },
  },
}
</script>

<style scoped>
.filter {
  padding: 1rem 2rem;
}
.filter-btn {
  border: none;
  background: none;
  padding: 0;
  outline: none;
  font-weight: 600;
  min-width: 8rem;
  max-width: 13rem;
  font-size: 1rem;
  width: 100%;
}
.tabs {
  width: 100%;
}
.custom-tabs {
  display: flex;
  padding-left: 0;
  margin-bottom: 0;
  list-style: none;
  margin-left: 2rem;
}

.custom-tabs li {
  margin-right: 1.5rem;
}
.custom-tabs a {
  color: #66f;
  font-weight: 600;
  padding-bottom: 1rem;
}

.custom-tabs a:hover {
  text-decoration: none;
}

.nuxt-link-active {
  border-bottom: 2px solid #000 !important;
  color: #000 !important;
}
</style>
