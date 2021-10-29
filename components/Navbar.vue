.
<template>
  <div class="navbar-container">
    <header class="menu-header">
      <nav>
        <ul class="nav-list">
          <li>
            <NuxtLink class="mr-3" to="/">
              <img src="https://cdna.iconscout.com/img/ae9f9fd.svg" alt="" />
            </NuxtLink>
          </li>
          <li>
            <SearchInput />
          </li>
          <li>
            <button class="btn-main button-link">
              <span>Explore</span>
            </button>
            <button class="btn-main button-link">
              <span>Tools</span>
            </button>
            <button class="btn-main button-link">
              <span>Resources</span>
            </button>
            <NuxtLink class="btn-main button-link" to="/icon-editor"
              >Icon Editor</NuxtLink
            >
          </li>
          <li class="pricing-list-item ml-auto d-sm-flex d-none">
            <a href="#">Pricing</a>
          </li>
          <li class="mx-3 d-sm-flex d-none">
            <button type="button" class="btn btn-default btn-rounded my-0">
              Login
            </button>
          </li>
          <li class="mx-3 d-sm-flex d-none">
            <button type="button" class="btn btn-primary btn-rounded">
              Sign up
            </button>
          </li>
        </ul>
      </nav>
    </header>
  </div>
</template>

<script>
export default {}
</script>

<style>
.navbar-container {
  position: sticky;
  top: 0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.08), 0 8px 12px rgba(0, 0, 0, 0.04);
  background: #fff;
  z-index: 1000;
}

.menu-header {
  box-sizing: border-box;
}

.nav-list {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1rem 1.5rem;
  margin-bottom: 0;
}

.nav-list li {
  list-style-type: none;
}

.pricing-list-item {
  margin-right: 1.5rem;
}

.pricing-list-item a {
  color: #2e334d;
}

.pricing-list-item a:hover {
  text-decoration: none;
  color: #66f;
}

.btn-main {
  border: none;
  background: none;
  outline: none;
}

.button-link {
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5rem;
  color: #2e334d;
  height: 76px;
  margin-top: -16px;
  margin-bottom: -16px;
  cursor: pointer;
  padding: 0.65rem;
}

.button-link:hover {
  text-decoration: none;
  color: #66f;
}

.btn-default {
  border-color: #d8dbeb;
  background: #fff;
  color: #000;
}

.btn-default:hover {
  background-color: #ebedf5;
  border-color: #d8dbeb;
}

.btn-primary {
  color: #fff;
  background-color: #66f;
  border-color: #66f;
  box-shadow: none;
}

.btn-primary:hover {
  background-color: #2929cc;
  border-color: #2929cc;
}

.btn-rounded {
  border-radius: 50px !important;
}

.btn {
  font-weight: 600;
  padding: 9px 19px;
  font-size: 1rem;
}
</style>
