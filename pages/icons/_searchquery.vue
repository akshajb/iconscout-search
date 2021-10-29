<template>
  <main class="search-page">
    <SubHeader
      :count="iconCount"
      :search-string="searchString"
      :style-text="styleText"
      :para-text="subHParaText"
    />
    <div class="filter-container d-none d-md-block">
      <SearchFilterBar
        :count="iconCount"
        @filterToggled="filterToggled($event)"
      />
    </div>
    <section class="d-flex">
      <Sidebar
        :show-filter="filterStatus"
        @priceFilterChange="priceChanged($event)"
        @dimensionFilterChange="dimensionChanged($event)"
        @viewFilterChange="viewChanged($event)"
        @stylesFilterChange="stylesChanged($event)"
      />
      <div class="results-container">
        <div class="filter-capsules d-flex align-items-center flex-wrap mb-3">
          <FilterButton
            v-if="$route.query.price && $route.query.price !== 'all'"
            :text="$route.query.price"
            @buttonClicked="priceChanged(null)"
          />

          <FilterButton
            v-if="$route.query.icon_grid"
            :text="`${$route.query.icon_grid}x${$route.query.icon_grid}`"
            @buttonClicked="dimensionChanged(null)"
          />

          <div v-if="$route.query.styles" class="style-buttons d-flex">
            <FilterButton
              v-for="style in $route.query.styles"
              :key="style"
              :text="style"
              @buttonClicked="
                stylesChanged(
                  $route.query.styles.filter((item) => item !== style)
                )
              "
            />
          </div>
        </div>
        <div
          v-if="viewFilter === 'item' && !$fetchState.pending"
          class="results"
        >
          <div v-for="icon in icons" :key="icon.slug">
            <IconTile :icon="icon" />
          </div>
        </div>
        <div v-else-if="$fetchState.pending" class="results">
          <div v-for="i in pageCount" :key="i">
            <article class="icon-tile-loader card-loader card-loader--tabs">
              <a href="#">
                <div class="icon-image">
                  <p class="title bg-white"></p>
                </div>
              </a>
            </article>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  data() {
    return {
      icons: [],
      packs: [],
      currentPage: null,
      priceFilter: null,
      dimensionFilter: null,
      viewFilter: 'item',
      stylesFilter: null,
      iconCount: 0,
      filterCapsules: [],
      searchString: '',
      pageCount: 60,
      filterStatus: false,
      subHParaText: `This home icon is in Glyph icon style. This icon is available on
        Iconscout web as well as accessible from Iconscout plugin for Sketch
        app, Adobe Illustrator, Adobe Photoshop, Adobe XD, Google Docs, Google
        slide, Microsoft Word and PowerPoint. Download this royalty free icon
        and use it in personal or commercial purpose.`,
    }
  },

  async fetch() {
    const reqQuery = { ...this.$route.query }
    if (typeof reqQuery.styles === 'string') {
      reqQuery.styles = [reqQuery.styles]
    }

    if (reqQuery.price === 'all') {
      reqQuery.price = null
    }
    const data = await this.$axios({
      url: '/v3/search',
      headers: { 'Client-Id': '198175844506907' },
      params: {
        query: this.$route.params.searchquery,
        ...reqQuery,
      },
    })
    this.viewFilter = reqQuery.product_type || 'item'
    if (this.viewFilter === 'item') {
      this.icons = data.data.response.items.data
      this.iconCount = data.data.response.items.total
    }
    this.priceFilter = reqQuery.price
  },

  computed: {
    styleText() {
      if (this.$route.query.styles && this.$route.query.styles.length === 1) {
        return this.$route.query.styles[0]
      }
      return ''
    },
  },

  watch: {
    '$route.query': '$fetch',
  },

  created() {
    this.searchString = this.$route.params.searchquery
  },

  methods: {
    filterToggled(e) {
      this.filterStatus = e
    },

    priceChanged(e) {
      this.priceFilter = e

      const query = {
        ...this.$route.query,
      }
      query.price = this.priceFilter

      this.$router.push({
        path: `/icons/${this.$route.params.searchquery}`,
        query,
      })
    },
    dimensionChanged(e) {
      this.dimensionFilter = e

      const query = {
        ...this.$route.query,
      }
      query.icon_grid = this.dimensionFilter

      this.$router.push({
        path: `/icons/${this.$route.params.searchquery}`,
        query,
      })
    },
    viewChanged(e) {
      this.viewFilter = e

      const query = {
        ...this.$route.query,
      }
      query.product_type = this.viewFilter
      this.$router.push({
        path: `/icons/${this.$route.params.searchquery}`,
        query,
      })
    },

    stylesChanged(e) {
      this.stylesFilter = e
      const query = {
        ...this.$route.query,
      }
      query.styles = this.stylesFilter
      this.$router.push({
        path: `/icons/${this.$route.params.searchquery}`,
        query,
      })
    },
  },
}
</script>

<style scoped>
.filter-container {
  position: sticky;
  background: #fafafc;
  top: 4.75rem;
  z-index: 1000;
  font-size: 14px;
}
.results-container {
  margin: 1rem 0;
  padding: 0 3rem;
  flex-grow: 1;
}
.results {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
}
.sub-header {
  padding-top: 2.5rem;
  background: #fafafc;
  font-size: 14px;
}

.sub-header .heading {
  font-weight: 700;
  font-size: 2.15rem;
  letter-spacing: -0.015em;
  text-transform: capitalize;
}

.icon-tile-loader {
  width: 132px;
  height: 132px;
  box-shadow: 0 0 0 1px #bec6f3 10px;
  margin: 1rem;
}
.card-loader {
  background-color: #fff;
  padding: 8px;
  position: relative;
  border-radius: 2px;
  margin-bottom: 0;
  overflow: hidden;
}
.card-loader:only-child {
  margin-top: 0;
}
.card-loader:before {
  content: '';
  height: 110px;
  display: block;
  background-color: hsl(240, 73%, 97%);
  box-shadow: -48px 78px 0 -48px #ededed, -51px 102px 0 -51px #ededed;
  border-radius: 10px;
}
.card-loader:after {
  content: '';
  background-color: #333;
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  animation-duration: 1s;
  animation-iteration-count: infinite;
  animation-name: loader-animate;
  animation-timing-function: linear;
  background: -webkit-linear-gradient(
    left,
    rgba(255, 255, 255, 0) 0%,
    rgba(255, 255, 255, 0.6) 30%,
    rgba(255, 255, 255, 0) 81%
  );
  background: -o-linear-gradient(
    left,
    rgba(255, 255, 255, 0) 0%,
    rgba(255, 255, 255, 0.6) 30%,
    rgba(255, 255, 255, 0) 81%
  );
  background: linear-gradient(
    to right,
    rgba(255, 255, 255, 0) 0%,
    rgba(255, 255, 255, 0.6) 30%,
    rgba(255, 255, 255, 0) 81%
  );
}

@keyframes loader-animate {
  0% {
    transform: translate3d(-100%, 0, 0);
  }
  100% {
    transform: translate3d(100%, 0, 0);
  }
}
</style>
