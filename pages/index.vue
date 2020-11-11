<template>
  <div>
    <heading
      heading="You are not alone"
      subheading="These resources are here for you 24/7"
    />
    <div class="row row-cols-1 row-cols-md-2 row-cols-xl-3">
      <card v-for="card in cards" :key="card.title" :card="card" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cards: [
        {
          title: 'Crisis Text Line',
          description:
            'For any crisis, painful emotion, or anytime you need support.',
          buttons: [
            {
              href: 'sms:741741?&body=HOME',
              style: 'primary',
              text: 'Text',
            },
          ],
        },
        {
          title: 'Suicide Prevention Lifeline',
          description:
            'For anyone who is depressed, going through a hard time, needs to talk, or is thinking about suicide.',
          buttons: [
            {
              href: 'tel:1-800-273-8255',
              style: 'primary',
              text: 'Call',
            },
            {
              href: 'https://suicidepreventionlifeline.org/chat/',
              style: 'secondary',
              text: 'Online Chat',
            },
          ],
        },
        {
          title: '911',
          description: 'For life-threatening emergencies.',
          buttons: [
            {
              href: 'tel:911',
              style: 'danger',
              text: 'Call 911',
            },
          ],
        },
        {
          title: 'The Trevor Project',
          description:
            'For LGBTQ individuals who are in crisis, feeling suicidal, or in need of a safe and judgment-free place to talk.',
          buttons: [
            {
              href: 'tel:1-866-488-7386',
              style: 'primary',
              text: 'Call',
            },
            {
              href: 'sms:678678?&body=START',
              style: 'secondary',
              text: 'Text',
            },
            {
              href: 'https://www.thetrevorproject.org/get-help-now/',
              style: 'secondary',
              text: 'Online Chat',
            },
          ],
        },
        {
          title: 'Domestic Violence Hotline',
          description:
            'For anyone who is experiencing domestic violence, seeking resources or information, or questioning unhealthy aspects of their relationship.',
          buttons: [
            {
              href: 'tel:1-800-799-7233',
              style: 'primary',
              text: 'Call',
            },
            {
              href: 'https://www.thehotline.org/get-help/',
              style: 'secondary',
              text: 'Online Chat',
            },
          ],
        },
        {
          title: 'Disaster Distress Helpline',
          description:
            'For anyone who is experiencing emotional distress related to any natural or human-caused disaster.',
          buttons: [
            {
              href: 'tel:1-800-985-5990',
              style: 'primary',
              text: 'Call',
            },
          ],
        },
      ],
    }
  },
  head: {
    title: 'Get help | Value Our Minds',
    meta: [
      {
        name: 'description',
        content: 'Mental health resources, here for you 24/7.',
      },
      {
        name: 'twitter:card',
        content: 'summary_large_image',
      },
      {
        name: 'twitter:title',
        content: 'Get help',
      },
      {
        name: 'twitter:description',
        content: 'Mental health resources, here for you 24/7.',
      },
      {
        name: 'twitter:image',
        content:
          'https://www.valueourminds.com' +
          require('@/assets/images/link-cards/index.png'),
      },
      {
        property: 'og:title',
        content: 'Get help',
      },
      {
        property: 'og:image',
        content:
          'https://www.valueourminds.com' +
          require('@/assets/images/link-cards/index.png'),
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
