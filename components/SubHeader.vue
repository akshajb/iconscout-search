<template>
  <div class="sub-header">
    <div class="sub-header-content px-sm-8 pb-sm-7 px-5 pb-5">
      <h1 class="heading">
        {{ count }} {{ searchString }}
        {{ styleText }}
        Icons
      </h1>
      <p>
        {{ paraText }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    paraText: {
      type: String,
      default: () => '',
    },

    count: {
      type: Number,
      default: () => 0,
    },

    styleText: {
      type: String,
      default: () => '',
    },

    searchString: {
      type: String,
      default: () => '',
    },
  },
}
</script>

<style>
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
