<template>
  <b-navbar type="dark" variant="accent" sticky>
    <b-navbar-nav>
      <b-nav-item to="/">Get help</b-nav-item>
      <b-nav-item to="/the5/">Mind the 5</b-nav-item>
      <b-nav-item to="/join/">Join the movement</b-nav-item>
    </b-navbar-nav>
  </b-navbar>
</template>

<style lang="scss" scoped>
nav {
  margin-bottom: 10px;
}

.navbar {
  padding: 0;
}

.navbar-dark .navbar-nav .nav-link {
  padding: 1rem 0.7rem;
  color: $white;
  &:hover {
    color: $white;
    background-color: #007135;
  }
  &.nuxt-link-exact-active {
    color: $white;
    background-color: #00612d;
  }
}
</style>
