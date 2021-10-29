<template>
  <button
    class="
      d-flex
      align-items-center
      btn btn-sm btn-default
      mr-3
      mt-sm-5-5 mt-3
      btn-rounded
      has-icon
      filter-remove-btn
    "
    type="button"
    @click.prevent="buttonClicked()"
  >
    {{ text }}
    <span>
      <svg
        width="20"
        height="20"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        fill="currentColor"
        class="ui-svg-inline ml-3"
      >
        <path
          d="M13.41,12l4.3-4.29a1,1,0,1,0-1.42-1.42L12,10.59,7.71,6.29A1,1,0,0,0,6.29,7.71L10.59,12l-4.3,4.29a1,1,0,0,0,0,1.42,1,1,0,0,0,1.42,0L12,13.41l4.29,4.3a1,1,0,0,0,1.42,0,1,1,0,0,0,0-1.42Z"
        ></path>
      </svg>
    </span>
  </button>
</template>

<script>
export default {
  props: {
    text: {
      type: String,
      required: true,
    },
  },
  methods: {
    buttonClicked() {
      this.$emit('buttonClicked')
    },
  },
}
</script>

<style scoped>
.filter-remove-btn {
  text-transform: capitalize;
}
</style>
