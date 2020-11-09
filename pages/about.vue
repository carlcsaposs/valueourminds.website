<template>
  <div>
    <heading heading="About" />
    <h2>Our Purpose</h2>
    <p>
      To promote mental health and build community so that everyone can feel
      safe, valued, and understood.
    </p>
    <h2>Contact Us</h2>
    <p>
      Send us an email at
      <a href="mailto:valueourminds@gmail.com">valueourminds@gmail.com</a>.
    </p>
    <p>
      We appreciate hearing your feedback, learning about how this service has
      impacted you, answering your questions, helping you get involved in our
      movement, or hearing from you for another reason.
    </p>
    <h2>Open Source</h2>
    <p>
      The source code for this website is
      <a href="https://github.com/valueourminds/website">available on GitHub</a
      >. Contributions are welcome.
    </p>
  </div>
</template>

<script>
export default {
  head: {
    title: 'About | Value Our Minds',
    meta: [
      {
        name: 'description',
        content:
          'Our purpose is to promote mental health and build community so that everyone can feel safe, valued, and understood.',
      },
    ],
  },
}
</script>
