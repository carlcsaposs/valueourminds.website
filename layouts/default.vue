<template>
  <div>
    <top-navbar />
    <div id="page-container" class="container-fluid">
      <Nuxt />
    </div>
    <bottom-navbar />
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

<style lang="scss" scoped>
#page-container {
  padding-bottom: 3.3rem; // Footer height + footer margin top + footer margin bottom
}
</style>
