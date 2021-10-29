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
        <div v-if="viewFilter === 'item'" class="results">
          <div v-for="icon in icons" :key="icon.slug">
            <IconTile :icon="icon" />
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
</style>
