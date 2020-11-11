Comment: Duplicate all changes to layouts/default.vue
<template>
  <div>
    <top-navbar />
    <div id="page-container" class="container-fluid">
      <Nuxt />
    </div>
  </div>
</template>

<style lang="scss">
html {
  height: 100%;
}

body {
  position: relative;
  min-height: 100%;
  overflow-wrap: break-word;
}

.btn {
  min-width: 5em;
}

h2 {
  font-size: 1.75rem;
}

h3 {
  font-size: 1.3rem;
}
</style>
