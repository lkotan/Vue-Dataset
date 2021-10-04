<template>
  <input
    type="text"
    placeholder="searh"
    :value="search"
    @keyup="$emit('changeSearch', $event.target.value)"
  />
</template>

<script>
export default {
  name:"Search",
  props: {
    search: { required: true },
  },
};
</script>

<style scoped>

</style>
