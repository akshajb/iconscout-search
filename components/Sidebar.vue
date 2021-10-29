<template>
  <div class="sidebar-container" :class="{ 'translate-out': !showFilter }">
    <div class="price-collapse">
      <b-button v-b-toggle.collapse-1 class="toggle-button">
        <span>Price</span>
        <svg
          width="24"
          height="24"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="currentColor"
          class="arrow-icon"
        >
          <path
            d="M17,9.17a1,1,0,0,0-1.41,0L12,12.71,8.46,9.17a1,1,0,0,0-1.41,0,1,1,0,0,0,0,1.42l4.24,4.24a1,1,0,0,0,1.42,0L17,10.59A1,1,0,0,0,17,9.17Z"
          ></path>
        </svg>
      </b-button>
      <b-collapse id="collapse-1" class="mt-2">
        <b-card>
          <div class="price-radio pl-4">
            <b-form-radio-group
              v-model="price"
              button-variant="indigo"
              :options="priceOptions"
              name="price"
              stacked
            ></b-form-radio-group>
          </div>
        </b-card>
      </b-collapse>
    </div>
    <div class="style-collapse">
      <b-button v-b-toggle.collapse-2 class="toggle-button">
        <span>Style</span>
        <svg
          width="24"
          height="24"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="currentColor"
          class="arrow-icon"
        >
          <path
            d="M17,9.17a1,1,0,0,0-1.41,0L12,12.71,8.46,9.17a1,1,0,0,0-1.41,0,1,1,0,0,0,0,1.42l4.24,4.24a1,1,0,0,0,1.42,0L17,10.59A1,1,0,0,0,17,9.17Z"
          ></path>
        </svg>
      </b-button>
      <b-collapse id="collapse-2" class="mt-2">
        <b-card>
          <div class="style-checkbox pl-4">
            <b-form-group v-slot="{ ariaDescribedby }">
              <b-form-checkbox-group
                v-model="styles"
                :options="styleOptions"
                :aria-describedby="ariaDescribedby"
                name="flavour-2a"
                stacked
              ></b-form-checkbox-group>
            </b-form-group>
          </div>
        </b-card>
      </b-collapse>
    </div>
    <div class="viewas-collapse">
      <b-button v-b-toggle.collapse-3 class="toggle-button">
        <span>View as</span>
        <svg
          width="24"
          height="24"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="currentColor"
          class="arrow-icon"
        >
          <path
            d="M17,9.17a1,1,0,0,0-1.41,0L12,12.71,8.46,9.17a1,1,0,0,0-1.41,0,1,1,0,0,0,0,1.42l4.24,4.24a1,1,0,0,0,1.42,0L17,10.59A1,1,0,0,0,17,9.17Z"
          ></path>
        </svg>
      </b-button>
      <b-collapse id="collapse-3" class="mt-2">
        <b-card>
          <div class="viewas-radio pl-4">
            <b-form-radio-group
              v-model="view"
              button-variant="indigo"
              :options="viewOptions"
              name="viewas"
              stacked
            ></b-form-radio-group>
          </div>
        </b-card>
      </b-collapse>
    </div>
    <div class="dimension-collapse">
      <b-button v-b-toggle.collapse-4 class="toggle-button">
        <span>Dimension</span>
        <svg
          width="24"
          height="24"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="currentColor"
          class="arrow-icon"
        >
          <path
            d="M17,9.17a1,1,0,0,0-1.41,0L12,12.71,8.46,9.17a1,1,0,0,0-1.41,0,1,1,0,0,0,0,1.42l4.24,4.24a1,1,0,0,0,1.42,0L17,10.59A1,1,0,0,0,17,9.17Z"
          ></path>
        </svg>
      </b-button>
      <b-collapse id="collapse-4" class="mt-2">
        <b-card>
          <div class="dimension-radio pl-4">
            <b-form-radio-group
              v-model="dimension"
              button-variant="indigo"
              :options="dimensionsOptions"
              name="dimension"
              stacked
            ></b-form-radio-group>
          </div>
        </b-card>
      </b-collapse>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    showFilter: {
      type: Boolean,
      default: () => false,
    },
  },

  data() {
    return {
      priceOptions: [
        { text: 'Free', value: 'free' },
        { text: 'Premium', value: 'premium' },
        { text: 'All', value: 'all' },
      ],
      viewOptions: [
        { text: 'Individual', value: 'item' },
        { text: 'Packs', value: 'pack', disabled: true },
      ],
      dimensionsOptions: [
        { text: '16x16', value: '16' },
        { text: '24x24', value: '24' },
        { text: '32x32', value: '32' },
        { text: '48x48', value: '48' },
        { text: '64x64', value: '64' },
        { text: '96x96', value: '96' },
        { text: '128x128', value: '128' },
        { text: '192x192', value: '192' },
        { text: '256x256', value: '256' },
        { text: '512x512', value: '512' },
      ],
      styleOptions: [
        { text: 'Line', value: 'line' },
        { text: 'Glyph', value: 'glyph' },
        { text: 'Flat', value: 'flat' },
        { text: 'Gradient', value: 'gradient' },
        { text: 'Dualtone', value: 'dualtone' },
        { text: 'Isometric', value: 'isometric' },
        { text: 'Rounded', value: 'rounded' },
        { text: 'Doodle', value: 'doodle' },
        { text: 'Colored Outline', value: 'colored-outline' },
      ],
      dimension: null,
      price: null,
      view: null,
      styles: [],
    }
  },

  watch: {
    price() {
      this.$emit('priceFilterChange', this.price)
    },
    dimension() {
      this.$emit('dimensionFilterChange', this.dimension)
    },
    view() {
      this.$emit('viewFilterChange', this.view)
    },
    styles() {
      this.$emit('stylesFilterChange', this.styles)
    },
  },
  mounted() {
    this.price = this.$route.query.price || 'all'
    this.view = this.$route.query.product_type || 'item'
    this.dimension = this.$route.query.icon_grid
  },
}
</script>

<style scoped>
.sidebar-container {
  width: 16.125rem;
  flex: 0 0 16.125rem;
  transform: translateX(0);
  transition: transform 0.2s linear;
  will-change: transform;
  position: sticky;
  top: 7.25rem;
  height: calc(100vh - 7.25rem);
  overflow-y: auto;
  border-right: 1px solid #ebedf5;
}

.translate-out {
  transform: translateX(-16rem);
  width: 0;
  flex: 0;
}

.sidebar-container .toggle-button {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #000;
  padding: 1.25rem 1.5rem 1.25rem 3rem;
  width: 100%;
  text-decoration: none;
  -webkit-appearance: none;
  appearance: none;
  border: none;
  background-color: initial;
  cursor: pointer;
  outline: none !important;
}

.sidebar-container .toggle-button:focus {
  box-shadow: none;
}

.sidebar-container .toggle-button:active {
  color: #000;
  background: none;
  border: none;
}

.sidebar-container .toggle-button:active:focus {
  box-shadow: none;
}

.sidebar-container .card {
  border: none;
  border-bottom: 1px solid #ebedf5;
}

.arrow-icon {
  opacity: 0.3;
  transition: all 0.2s ease-in-out;
}

.collapsed .arrow-icon {
  transform: rotate(0deg);
}
.not-collapsed .arrow-icon {
  transform: rotate(180deg);
}

.price-radio,
.viewas-radio,
.dimension-radio,
.style-checkbox {
  font-size: 14px;
}
</style>
<style>
.custom-control {
  margin-bottom: 8px !important;
}
.custom-control-input:checked ~ .custom-control-label::before {
  /* color: #ffff; */
  background-color: #66f;
  box-shadow: none;
  border-color: #66f;
}
.custom-control-input:checked ~ .custom-control-label::before {
  color: #66f;
  box-shadow: none;
  border-color: #66f;
}
</style>
