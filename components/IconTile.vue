<template>
  <article
    v-if="icon"
    class="icon-tile"
    @mouseenter="showActions(icon.slug)"
    @mouseleave="hideActions(icon.slug)"
  >
    <a href="#">
      <div class="icon-image">
        <img :src="icon.urls.png_64" alt="" />
        <p class="title">{{ icon.name }}</p>
      </div>
    </a>

    <div :ref="icon.slug" class="actions">
      <button class="like-btn btn btn-default btn-icon btn-small">
        <svg
          width="1.2em"
          height="1.2em"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="#596080"
          class="ui-svg-inline"
        >
          <path
            d="M20.8,5.7c-2.1-2.8-6-3.4-8.8-1.3C9.5,2.5,6,2.8,3.8,5c-2.4,2.4-2.5,6.4,0,8.9l6.2,6.2c0.5,0.5,1.2,0.8,1.9,0.8c0.7,0,1.4-0.3,1.9-0.8l6.2-6.2C22.4,11.6,22.6,8.2,20.8,5.7z"
          ></path>
        </svg>
      </button>
      <button class="download-btn btn btn-default btn-icon btn-small">
        <svg
          width="1.2em"
          height="1.2em"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="#fff"
          class="ui-svg-inline"
        >
          <path
            d="M21,14a1,1,0,0,0-1,1v4a1,1,0,0,1-1,1H5a1,1,0,0,1-1-1V15a1,1,0,0,0-2,0v4a3,3,0,0,0,3,3H19a3,3,0,0,0,3-3V15A1,1,0,0,0,21,14Zm-9.71,1.71a1,1,0,0,0,.33.21.94.94,0,0,0,.76,0,1,1,0,0,0,.33-.21l4-4a1,1,0,0,0-1.42-1.42L13,12.59V3a1,1,0,0,0-2,0v9.59l-2.29-2.3a1,1,0,1,0-1.42,1.42Z"
          ></path>
        </svg>
      </button>
    </div>
  </article>
</template>

<script>
export default {
  props: {
    icon: {
      type: Object,
      default: () => {},
    },
  },

  methods: {
    showActions(slug) {
      this.$refs[slug].classList.add('action-show')
    },
    hideActions(slug) {
      this.$refs[slug].classList.remove('action-show')
    },
  },
}
</script>

<style scoped>
.icon-tile {
  min-width: 160px;
  min-height: 160px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  transition: box-shadow 0.2s ease-in;
}

.icon-tile:hover {
  background-color: #fff;
  box-shadow: 0 0 0 1px #d8dbeb;
}

.icon-tile a {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  text-decoration: none !important;
}
.icon-tile img {
  width: 64px;
}
.icon-tile .title {
  font-weight: 400;
  color: #596080;
  margin: 0.25rem auto 0;
  font-size: 0.85em;
  width: 64px;
  text-align: center;
  text-transform: capitalize;
}

.icon-tile .like-btn {
  position: absolute;
  top: 5px;
  right: 5px;
  padding: 1px 5px 5px 5px;
}

.icon-tile .download-btn {
  position: absolute;
  bottom: 5px;
  right: 5px;
  padding: 1px 5px 5px 5px;
  background: #26a5bf;
}

.icon-tile .download-btn:hover {
  background: #26a5bf;
}

.actions {
  opacity: 0;
  transition: opacity 0.2s ease-in;
}

.action-show {
  opacity: 1;
}
</style>
