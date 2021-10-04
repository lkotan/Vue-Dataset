<template>
  <button @click="$emit('buttonClick')">{{name}}</button>
</template>

<script>
export default {
    name:"Button",
    props:{
        name:{required:true}
    }
}
</script>

<style scoped>

</style>