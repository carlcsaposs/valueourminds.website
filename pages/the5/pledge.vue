<template>
  <div>
    <heading heading="Welcome to team #mindthe5" />
    <p>You are the {{ ordinalNumber }} person to take the pledge.</p>
    <p>
      By pledging to take care of your mental health and ask for help when you
      need it, you will inspire others to do the same.
    </p>
    <p>
      Together, if each of us take care of our mental health, we can create a
      future in which everyone can feel safe, valued, and understood.
    </p>
    <p>Thank you for contributing to that future.</p>
    <h2>Share</h2>
    <p class="before-button">
      If you found this resource helpful, please consider sharing it with
      others.
    </p>
    <div v-show="!canShareText">
      <b-button
        variant="primary"
        href="https://out.valueourminds.com/the5/pledge/twitter"
        >Twitter</b-button
      >
      <b-button
        variant="primary"
        href="https://out.valueourminds.com/the5/pledge/facebook"
        >Facebook</b-button
      >
    </div>
    <div v-show="canShareText">
      <b-button variant="primary" @click="share">Share</b-button>
    </div>
    <h3>Message template</h3>
    <blockquote id="message-template" class="before-button">
      {{ shareText }}
    </blockquote>
    <b-button
      variant="secondary"
      :disabled="copyButtonDisabled"
      aria-describedby="message-template"
      @click="copyTemplate"
      >{{ copyButtonText }}</b-button
    >
    <h3>{{ canShareFiles ? 'Share' : 'Download' }} images</h3>
    <b-tabs>
      <b-tab v-for="platform in platforms" :key="platform.id">
        <template #title>
          <img
            :id="platform.id === 'twitter' ? 'twitter' : false"
            :src="
              require(`@/assets/images/pages/the5/pledge/${platform.id}/icon.svg`)
            "
            :alt="platform.name"
          />
        </template>
        <b-alert v-if="platform.linkImage" show
          >{{ platform.name }} automatically shows the "5 steps" image if no
          image is uploaded.</b-alert
        >
        <div id="image-downloads">
          <div
            v-for="image in platform.images"
            :key="image.alt"
            class="image-download"
          >
            <img :src="image.svg" :alt="image.alt" />
            <div v-show="!canShareFiles">
              <b-button variant="secondary" :href="image.png" download
                >Download</b-button
              >
            </div>
            <div v-show="canShareFiles">
              <b-button variant="secondary" @click="shareFile(image.png)"
                >Share</b-button
              >
            </div>
          </div>
        </div>
      </b-tab>
    </b-tabs>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pledgeCounter: null,
      canShareText: false, // Web Share API available
      canShareFiles: false, // Web Share API w/files available
      copyButtonDisabled: false,
      shareText:
        'I pledged to #mindthe5 and take care of my mental health. Will you join me? Click here: https://www.valueourminds.com/the5/',
      platforms: [
        {
          id: 'instagram',
          name: 'Instagram',
          images: [
            {
              svg: require('@/assets/images/pages/the5/pledge/instagram/steps.svg'),
              png: require('@/assets/images/pages/the5/pledge/instagram/steps.png'),
              alt: 'Mind the 5 steps',
            },
            {
              svg: require('@/assets/images/pages/the5/pledge/instagram/heart.svg'),
              png: require('@/assets/images/pages/the5/pledge/instagram/heart.png'),
              alt: 'I heart my mind',
            },
          ],
          linkImage: false,
        },
        {
          id: 'twitter',
          name: 'Twitter',
          images: [
            {
              svg: require('@/assets/images/pages/the5/pledge/twitter/heart.svg'),
              png: require('@/assets/images/pages/the5/pledge/twitter/heart.png'),
              alt: 'I heart my mind',
            },
          ],
          linkImage: true,
        },
        {
          id: 'facebook',
          name: 'Facebook',
          images: [
            {
              svg: require('@/assets/images/pages/the5/pledge/facebook/heart.svg'),
              png: require('@/assets/images/pages/the5/pledge/facebook/heart.png'),
              alt: 'I heart my mind',
            },
          ],
          linkImage: true,
        },
      ],
    }
  },
  computed: {
    copyButtonText() {
      return this.copyButtonDisabled ? 'Copied' : 'Copy text'
    },
    ordinalNumber() {
      if (this.pledgeCounter === null) {
        return 'latest'
      }
      const i = this.pledgeCounter
      const j = i % 10
      const k = i % 100
      if (j === 1 && k !== 11) {
        return i + 'st'
      }
      if (j === 2 && k !== 12) {
        return i + 'nd'
      }
      if (j === 3 && k !== 13) {
        return i + 'rd'
      }
      return i + 'th'
    },
  },
  beforeMount() {
    if (navigator.share) {
      this.canShareText = true

      if (navigator.canShare) {
        const imagePath = this.platforms[0].images[0].png
        fetch(imagePath)
          .then(function (response) {
            return response.blob()
          })
          .then(
            function (myBlob) {
              const fileName = imagePath.split('/').pop()
              const file = new File([myBlob], fileName, {
                type: 'image/png',
              })
              const filesArray = [file]
              if (navigator.canShare({ files: filesArray })) {
                this.canShareFiles = true
              }
            }.bind(this)
          )
      }
    }
  },
  mounted() {
    // Check query string for pledge count
    if (this.$route.query.count) {
      this.pledgeCounter = parseInt(this.$route.query.count, 10) + 1
    }
    // Remove query string
    window.history.replaceState(null, null, window.location.pathname)

    if (window.location.hostname === 'www.valueourminds.com') {
      // Increment count
      this.$fire.firestore
        .collection('counters')
        .doc('mindthe5')
        .update({ count: this.$fireModule.firestore.FieldValue.increment(1) })
    }
  },
  methods: {
    share() {
      navigator.share({ text: this.shareText })
    },
    copyTemplate() {
      if (navigator.clipboard) {
        navigator.clipboard.writeText(this.shareText)
      } else {
        // Fallback if Clipboard API is not available
        const textArea = document.createElement('textarea')

        // Style for minimal visual impact
        textArea.style.position = 'fixed'
        textArea.style.top = 0
        textArea.style.left = 0
        textArea.style.width = '2em'
        textArea.style.height = '2em'
        textArea.style.padding = 0
        textArea.style.border = 'none'
        textArea.style.outline = 'none'
        textArea.style.boxShadow = 'none'
        textArea.style.background = 'transparent'

        textArea.value = this.shareText
        document.body.appendChild(textArea)
        textArea.focus()
        textArea.select()
        try {
          document.execCommand('copy')
        } catch {}
        document.body.removeChild(textArea)
      }

      // Disable button for 2 seconds
      this.copyButtonDisabled = true
      setTimeout(
        function () {
          this.copyButtonDisabled = false
        }.bind(this),
        4000
      )
    },
    shareFile(imagePath) {
      fetch(imagePath)
        .then(function (response) {
          return response.blob()
        })
        .then(function (myBlob) {
          const fileName = imagePath.split('/').pop()
          const file = new File([myBlob], fileName, {
            type: 'image/png',
          })
          const filesArray = [file]
          navigator.share({
            files: filesArray,
            text:
              'I pledged to #mindthe5 and take care of my mental health. Will you join me? Click here: https://www.valueourminds.com/the5/',
          })
        })
    },
  },
  head: {
    title: 'Pledge to #mindthe5 | Value Our Minds',
    meta: [
      {
        name: 'robots',
        content: 'noindex',
      },
    ],
  },
}
</script>

<style lang="scss" scoped>
.btn {
  margin-top: 0.3rem;
  margin-bottom: 1rem;
}
.before-button {
  margin-bottom: 0;
}
blockquote {
  background: #f9f9f9;
  border-left: 0.5em solid #ccc;
  padding: 0.5em;
}
.nav-link img {
  width: 32px;
  margin: 16px;
  &#twitter {
    // Twitter SVG already has 25% margin
    width: 48px;
    margin: 8px;
  }
}
::v-deep .nav-tabs .nav-link {
  width: 64px;
  height: 64px;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.tab-pane {
  margin-top: 0.5rem;
}
.image-download {
  display: flex;
  align-items: center;
  min-width: 0;
  & img {
    flex-grow: 1;
    min-width: 0;
    max-height: 15rem;
    max-width: 15rem;
  }
  & button {
    flex-shrink: 0;
  }
}
#image-downloads {
  display: flex;
  flex-wrap: wrap;
}
</style>
