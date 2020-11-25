<template>
  <div>
    <heading heading="Feedback" />
    <b-form @submit="onSubmit">
      <b-form-group label="How did we do?">
        <b-form-radio-group
          id="input-1"
          v-model="form.isPositiveFeedback"
          required
          plain
        >
          <b-form-radio :value="true">
            <svg id="thumbs-up" aria-label="Thumbs up">
              <use href="~assets/images/feedback-thumb.svg#feedback-thumb" />
            </svg>
          </b-form-radio>
          <b-form-radio :value="false"
            ><svg id="thumbs-down" aria-label="Thumbs down">
              <use href="~assets/images/feedback-thumb.svg#feedback-thumb" />
            </svg>
          </b-form-radio>
        </b-form-radio-group>
      </b-form-group>
      <b-form-group
        label="Tell us what happened and how that impacted you"
        label-for="input-2"
        description="Please do not include information that could be used to identify you."
      >
        <b-form-textarea
          id="input-2"
          v-model="form.eventDescription"
          rows="3"
          required
        ></b-form-textarea>
      </b-form-group>
      <b-form-group
        label="Any comments or suggestions? (optional)"
        label-for="input-3"
      >
        <b-form-textarea
          id="input-3"
          v-model="form.suggestions"
        ></b-form-textarea>
      </b-form-group>
      <b-form-group
        label="Email address (optional)"
        label-for="input-4"
        description="Only used to follow up about your feedback. You must be at least 13 years of age to enter your email."
      >
        <b-form-input
          id="input-4"
          v-model="form.email"
          type="email"
        ></b-form-input>
      </b-form-group>
      <b-form-text id="privacy-agreement">
        By pressing submit, you agree to our
        <nuxt-link to="/privacy/" target="_blank" rel="noopener"
          >Privacy Policy</nuxt-link
        >.
      </b-form-text>
      <b-button
        id="submit-button"
        type="submit"
        variant="primary"
        aria-describedby="privacy-agreement"
        :disabled="uploading"
        >{{ uploading ? 'Submitting...' : 'Submit' }}</b-button
      >
    </b-form>
  </div>
</template>

<script>
export default {
  layout: 'no-footer',
  data() {
    return {
      previousPagePath: null,
      uploading: false,
      form: {
        isPositiveFeedback: null,
        eventDescription: '',
        suggestions: '',
        email: '',
      },
    }
  },
  computed: {
    formInput() {
      return (
        this.form.eventDescription !== '' ||
        this.form.suggestions !== '' ||
        this.form.email !== ''
      )
    },
  },
  mounted() {
    window.addEventListener('beforeunload', (event) => {
      if (this.formInput) {
        event.preventDefault()
        // For older browsers
        event.returnValue = 'Leave page? Your changes will be lost.'
      }
    })
  },
  methods: {
    onSubmit(event) {
      event.preventDefault()
      this.uploading = true
      if (window.location.hostname === 'www.valueourminds.com') {
        // Send data to Firestore
        const now = this.$fireModule.firestore.Timestamp.now().toMillis()
        // Save date instead of full timestamp to respect user privacy
        const date = now - (now % 86400000)
        this.$fire.firestore
          .collection('feedback_responses')
          .add({
            page_ref: this.previousPagePath,
            date: this.$fireModule.firestore.Timestamp.fromMillis(date),
            is_positive_feedback: this.form.isPositiveFeedback,
            event_description: this.form.eventDescription,
            suggestions: this.form.suggestions,
            email: this.form.email,
          })
          .then(
            function () {
              this.uploading = false
              this.resetForm()
              this.$router.push('/feedback/thanks/')
            }.bind(this)
          )
      }
    },
    resetForm() {
      this.form = {
        isPositiveFeedback: null,
        eventDescription: '',
        suggestions: '',
        email: '',
      }
    },
  },
  head: {
    title: 'Send feedback | Value Our Minds',
  },
  beforeRouteEnter(to, from, next) {
    next((vm) => {
      vm.previousPagePath = from.path
    })
  },
  beforeRouteLeave(to, from, next) {
    if (this.formInput) {
      const answer = window.confirm('Leave page? Your changes will be lost.')
      if (answer) {
        this.resetForm()
        next()
      } else {
        next(false)
      }
    } else {
      next()
    }
  },
}
</script>

<style lang="scss" scoped>
#submit-button {
  margin: 0.5rem 0;
}
#input-1 {
  display: flex;
  max-width: 20rem;
}
svg {
  fill: none;
  width: 100%;
  stroke-width: 40px;
  paint-order: stroke;
}
#thumbs-up {
  stroke: #007cbe;
}
#thumbs-down {
  stroke: #dc3545;
  transform: scale(-1); // Rotate 180 degrees (flip on x-axis and y-axis)
}
// Hide radio button circle
::v-deep input[type='radio'] {
  opacity: 0;
  width: 0;
  height: 0;
}
input[type='radio'] + label svg {
  cursor: pointer;
}
input[type='radio']:checked + label svg {
  &#thumbs-up {
    fill: #007cbe;
  }
  &#thumbs-down {
    fill: #dc3545;
  }
}
</style>
