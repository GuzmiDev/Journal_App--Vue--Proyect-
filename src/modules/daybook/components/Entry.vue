<template>
  <div
    class="entry-container mb-3 pointer p-2"
    @click="$router.push({ name: 'entry', params: { id: entry.id } })"
  >
    <div class="entry-title d-flex">
      <span class="text-success fs-5 fw-bold">{{ entryDay }}</span>
      <span class="mx-1 fs-5">{{ entryMoth }}</span>
      <span class="mx-2 fw-light">{{ entryYear }}</span>
    </div>
    <div class="entry-description">
      {{ shortText }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    entry: {
      type: Object,
      required: true,
    },
  },
  computed: {
    shortText() {
      return this.entry.text.length > 130
        ? this.entry.text.substring(0, 130) + "..."
        : this.entry.text;
    },
    entryDay() {
      const day = new Date(this.entry.date).getDate();
      return day;
    },
    entryMoth() {
      const moth = new Date(this.entry.date).toLocaleString("default", {
        month: "long",
      });
      return moth;
    },
    entryYear() {
      const year = new Date(this.entry.date).toLocaleString("default", {
        year: "numeric",
        weekday: "long",
      });
      return year;
    },
  },
};
</script>

<style lang="scss" scoped>
.entry-container {
  border-bottom: 1px solid #2c3e50;
  transition: 0.2s all ease-in;

  &:hover {
    background-color: lighten($color: grey, $amount: 45);
    transition: 0.2s all ease-in;
  }
  .entry-description {
    font-size: 12px;
  }
}
</style>
