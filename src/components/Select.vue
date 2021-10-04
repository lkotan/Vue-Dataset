<template>
  <select @change="$emit('changeDepartment', $event.target.value)">
    <option disabled selected>Please Select Department</option>
    <option :value="item" v-for="(item, index) in department" :key="index" >
      {{ item }}
    </option>
  </select>
</template>

<script>
export default {
  name:"Select",
  props: {
    department: { type: Array, required: true },
  },
};
</script>

<style scoped>
</style>
