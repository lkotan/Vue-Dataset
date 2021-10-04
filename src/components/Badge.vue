<template>
  <div class="card__badge">
    <span>{{ badge }}</span>
  </div>
</template>

<script>
export default {
  name: "Badge",
  props: {
    badge: { required: true },
  },
};
</script>

<style scoped>

</style>
