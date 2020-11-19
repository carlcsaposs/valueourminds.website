Comment: Duplicate all changes to layouts/default.vue
<template>
  <div>
    <top-navbar />
    <div id="page-container" class="container-fluid">
      <Nuxt />
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    // Check query string for QR code referral
    // Each QR code we distribute (e.g. on a poster) has a unique ID
    const qrId = this.$route.query.qr || null
    // Remove query string
    window.history.replaceState(null, null, window.location.pathname)
    if (window.location.hostname === 'www.valueourminds.com') {
      // Send data to Firestore
      const now = this.$fireModule.firestore.Timestamp.now().toMillis()
      // Save date instead of full timestamp to respect user privacy
      const date = now - (now % 86400000)
      this.$fire.firestore.collection('page_loads').add({
        qr_ref: qrId,
        date: this.$fireModule.firestore.Timestamp.fromMillis(date),
        page_path: this.$route.path,
      })
    }

    // Track link clicks
    document.addEventListener(
      'click',
      function (event) {
        if (!event.target.matches('a')) {
          return
        }
        if (
          window.location.hostname === 'www.valueourminds.com' &&
          new URL(event.target.href).hostname !== window.location.hostname
        ) {
          // Prevent redirect
          event.preventDefault()
          // Send click event to database
          const now = this.$fireModule.firestore.Timestamp.now().toMillis()
          // Save date instead of full timestamp to respect user privacy
          const date = now - (now % 86400000)
          this.$fire.firestore
            .collection('link_clicks')
            .add({
              href: event.target.href,
              date: this.$fireModule.firestore.Timestamp.fromMillis(date),
              page_path: this.$route.path,
            })
            .then(function () {
              // Redirect
              window.location.href = event.target.href
            })
        }
      }.bind(this)
    )
  },
}
</script>

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
