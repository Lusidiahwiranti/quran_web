<script>
export default {
  name: "NavItem",
};
</script>

<template>
  <header>
    <div class="container">
      <nav
        class="navbar navbar-expand-lg bg-body-tertiary-center"
      >
          <a class="navbar-brand" href="#">MY AL-QURAN</a>
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
              <span class="navbar-toggler-icon"></span>
          </button>

          <router-link
          :class="{ active: $route.name === 'home' }"
          class="y nav-link"
          to="/"
          >Home</router-link
        >
          <router-link
                  :class="{ active: $route.name === 'search' }"
                  class="y nav-link"
                  to="/search"
          >Search</router-link
          >
        <router-link
          :class="{ active: $route.name === 'about' }"
          class="y nav-link"
          to="/about"
          >About Us</router-link
        >
      </nav>
    </div>
  </header>
</template>

<style scoped>
.y {
  color: rgb(23, 21, 21);

    align-items: center;
    list-style: none;
    margin-left: 10px;
    text-decoration: none;
    float: left;
}
.navbar-expand-lg {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    text-align: center;
    background-color: rgba(115, 107, 107, 0.93);
    margin-top: 60px;
    display: flex;
    justify-content: space-between;
    padding: 5px 10px ;

}
.y:hover {
    color: #06060b;
    font-size: 20px;
    transition: .2s;
    background-color: rgb(255, 240, 240);
}

.active {
  color: black !important;
    text-align: center;
    padding: 5px;
}
</style>
