<template>
  <div class="pagination">
    <div v-for="page in totalPage" :key="page">
      <Button v-if="page == 1" :disabled="currentPage == page ? true : false" @buttonClick="currentPage--,$emit('changePage', currentPage)" name="Prev"/>
      <Button :name="page" :class="[initialPage == page ? 'active' : '']"
        @buttonClick="(currentPage = page), $emit('changePage', currentPage)"/>
      <Button name="Next" v-if="page == totalPage"  :disabled="currentPage == totalPage ? true : false" @buttonClick="currentPage++,$emit('changePage', currentPage)"/>
    </div>
  </div>
</template>

<script>
import Button from "./Button.vue"
export default {
  name: "Pagination",
  components:{
    Button,
  },
  props: {
    totalPage: { required: true },
    perPage: { required: true },
    initialPage: { required: true },
  },
  data(){
    return{
      currentPage:this.initialPage
    }
  }
};
</script>

<style scoped>

</style>
