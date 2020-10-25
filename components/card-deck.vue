<template>
  <div class="row row-cols-1 row-cols-md-2 row-cols-xl-3">
    <div v-for="card in cards" :key="card.title" class="col mb-4">
      <div class="card h-100">
        <div v-if="card.image">
          <img
            :src="require('@/assets/images/' + card.image.file)"
            :alt="card.image.alt"
            class="card-img-top"
          />
        </div>
        <div class="card-body">
          <h2 class="card-title"><span v-html="card.title"></span></h2>
          <p
            v-for="paragraph in card.description"
            :key="paragraph"
            class="card-text"
          >
            {{ paragraph }}
          </p>
          <div v-if="card.buttons" id="buttons">
            <b-button
              v-for="button in card.buttons"
              :key="button.text"
              :variant="button.style"
              :href="button.href"
              :to="button.to"
              >{{ button.text }}</b-button
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    cards: {
      type: Array,
      required: true,
    },
  },
}
</script>

<style lang="scss" scoped>
.btn {
  margin-right: 0.3rem;
  margin-bottom: 0.3rem;
  &:last-child {
    margin-right: 0;
  }
}
#buttons {
  margin-bottom: -0.3rem; // Removes margin on final row of buttons
}
.card img {
  object-fit: contain;
  padding: 0.75rem;
  padding-bottom: 0;
}
</style>
