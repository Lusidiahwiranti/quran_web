<script>
export default {
  name: "NavItem",
};
</script>

<template>
  <header>
    <div class="container">
      <nav
        class="navbar navbar-expand-lg bg-transparent justify-content-center"
      >
        <router-link
          :class="{ active: $route.name === 'home' }"
          class="y nav-link"
          to="/"
          >Home</router-link
        >
        <router-link
          :class="{ active: $route.name === 'read' }"
          class="y nav-link"
          :to="{ name: 'read', params: { id: 1 } }"
          >Read</router-link
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
  color: #a9a9a9;
}

.active {
  color: black !important;
}
</style>
