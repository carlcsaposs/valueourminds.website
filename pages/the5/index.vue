<template>
  <div>
    <heading heading="Mind the 5" subheading="Steps to support mental health" />
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
            file: 'pages/the5/index/mindthe5-1.svg',
            alt: 'Person eating, sleeping, and exercising',
          },
          title: '1. Take care of <b class="text-accent">BODY</b>',
          bullets: [
            'Eat a diet that gives you energy',
            'Move your body in ways that feel good to you',
            'Try to get uninterrupted sleep on a consistent schedule (8-10 hours for teens, 7-9 hours for adults)',
            'Go outside',
            'Take breaks',
          ],
        },
        {
          image: {
            file: 'pages/the5/index/mindthe5-2.svg',
            alt: 'Unbalanced scale',
          },
          title: '2. <b class="text-primary">YOU</b> first',
          bullets: [
            'Take care of yourself before helping others',
            'Exercise kindness and compassion to yourself',
            'Create structure and personal boundaries',
            'Set aside time to do something you enjoy',
          ],
        },
        {
          image: {
            file: 'pages/the5/index/mindthe5-3.svg',
            alt: 'Hands holding a heart',
          },
          title: '3. Recognize and accept <b class="text-accent">FEELINGS</b>',
          bullets: [
            'Take a moment to name what you feel and sit with it for a couple minutes',
            'Accept how you feel and that you may not have control over how you feel',
            'Turn off your screen while you do this activity',
          ],
        },
        {
          image: {
            file: 'pages/the5/index/mindthe5-4.svg',
            alt: 'Group of people',
          },
          title: '4. <b class="text-primary">CONNECT</b> with others',
          bullets: [
            'We need each other to survive and thrive',
            'Talk with someone. Share how you’re honestly feeling.',
            'Check in on a friend. Listen. Look out for each other.',
          ],
        },
        {
          image: {
            file: 'pages/the5/index/mindthe5-5.svg',
            alt: 'Two hands reaching out to each other',
          },
          title: '5. Ask for <b class="text-accent">HELP</b>',
          bullets: [
            'Asking for help is brave and responsible. We all need help from each other.',
            'Your experiences are real and important. Each of us are uniquely affected by our experiences.',
            'Click the button below to talk with someone. You will choose from a list of resources that are available 24/7.',
            'It’s always better to ask for help sooner rather than later',
          ],
          buttons: [
            {
              to: '/',
              style: 'primary',
              text: 'Get help',
            },
          ],
        },
        {
          title: 'Take the pledge',
          description:
            'Several people have pledged to #mindthe5 and take care of their mental health. Will you join them?',
          buttons: [
            {
              to: '/the5/pledge/',
              style: 'secondary',
              text: 'Take the pledge',
            },
          ],
        },
      ],
    }
  },
  head: {
    title: 'Mind the 5 | Value Our Minds',
    meta: [
      {
        name: 'description',
        content:
          '5 simple steps to support mental health. Take the pledge to #mindthe5',
      },
      {
        name: 'twitter:card',
        content: 'summary_large_image',
      },
      {
        name: 'twitter:title',
        content: 'Mind the 5',
      },
      {
        name: 'twitter:description',
        content:
          '5 simple steps to support mental health. Take the pledge to #mindthe5',
      },
      {
        name: 'twitter:image',
        content:
          'https://www.valueourminds.com' +
          require('@/assets/images/link-cards/the5.png'),
      },
      {
        property: 'og:title',
        content: 'Mind the 5',
      },
      {
        property: 'og:image',
        content:
          'https://www.valueourminds.com' +
          require('@/assets/images/link-cards/the5.png'),
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
::v-deep .card img {
  max-height: 7rem;
}
</style>
