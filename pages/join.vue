<template>
  <div>
    <h1>
      Imagine a world in which everyone can
      <span class="text-accent">feel accepted</span>,
      <span class="text-accent">safe</span>, and
      <span class="text-accent">understood</span>.
    </h1>
    <h1>
      To create that future, we work to
      <span class="text-primary">promote mental health</span> and
      <span class="text-primary">build community</span>.
    </h1>
    <h2>Interested in contributing?</h2>
    <p>If so, welcome aboard. You're a member of the Value Our Minds team.</p>
    <p>Here's how you can get involved:</p>
    <ol>
      <li>
        <p>Join our Twist community and introduce yourself</p>
        <b-button
          variant="primary"
          href="https://twist.com/j/a57ad48687d4db33b0c8b3fba3a08aee"
          >Join our Twist community</b-button
        >
      </li>
      <li>Contribute to an existing project or start a new one</li>
      <li>Speak up and share your experience, perspective, and ideas</li>
    </ol>
    <h2>Some of our projects:</h2>
    <card-deck :cards="cards" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      cards: [
        {
          image: {
            file: 'posters.svg',
            alt: 'Posters with mental health resources',
          },
          title: 'Posters',
          description: [
            'Posters to raise awareness of mental health resources',
          ],
        },
        {
          image: {
            file: 'id-card.svg',
            alt: 'Back side of ID card with mental health resources',
          },
          title: 'ID cards',
          description: [
            'Use the back of student ID cards to promote mental health resources',
          ],
        },
      ],
    }
  },
  head: {
    title: 'Join the movement | Value Our Minds',
    meta: [
      {
        name: 'description',
        content:
          'Our purpose is to promote mental health and build community so that everyone can feel accepted, safe, and understood.',
      },
      {
        name: 'twitter:card',
        content: 'summary_large_image',
      },
      {
        name: 'twitter:title',
        content: 'Join the movement',
      },
      {
        name: 'twitter:description',
        content:
          'Our purpose is to promote mental health and build community so that everyone can feel accepted, safe, and understood.',
      },
      {
        name: 'twitter:image',
        content:
          'https://www.valueourminds.com' +
          require('@/assets/images/link-cards/join.png'),
      },
      {
        property: 'og:title',
        content: 'Join the movement',
      },
      {
        property: 'og:image',
        content:
          'https://www.valueourminds.com' +
          require('@/assets/images/link-cards/join.png'),
      },
      {
        property: 'og:image:height',
        content: 2144,
      },
      {
        property: 'og:image:width',
        content: 4096,
      },
    ],
  },
}
</script>

<style lang="scss" scoped>
li p {
  margin-bottom: 0;
}
h1 {
  font-family: Cabin, sans-serif;
  margin-bottom: 3rem;
}
</style>
