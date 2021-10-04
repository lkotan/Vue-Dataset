<template>
  <div class="card">
    <header class="card__header">
      <img class="card__img" src="@/assets/user.png" alt="" />
      <h3 class="card__title">
        {{ item.name }}
      </h3>
      <Badge :badge="badge" />
    </header>
    <div class="card__content">
      <p>{{ item.email }}</p>
      <span>{{ item.phone }}</span>
    </div>
    <footer class="card__footer">
      <span>09-12-2020</span>
    </footer>
  </div>
</template>

<script>
import Badge from "./Badge.vue";

export default {
  name: "Card",
  components: {
    Badge,
  },
  props: {
    item: { required: true },
  },
  computed: {
    badge() {
      let arr = this.item.department.split(" ");
      let str = "";
      switch (arr.length) {
        case 1:
          str = arr[0][0];
          break;
        case 2:
          str = arr[0][0] + arr[1][0];
          break;
        case 3:
          str = arr[0][0] + arr[1][0] + arr[2][0];
          break;
        default:
          break;
      }
      return str;
    },
  },
};
</script>

<style scoped>
</style>
