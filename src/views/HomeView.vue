<template>
  <div class="home">
    <VueLoading :active="isLoading" />
    <h1>Hello, This is Home Page.</h1>
    <hr>
    <!-- <HelloWorld /> -->
  </div>
</template>

<script>
// import HelloWorld from '@/components/HelloWorld.vue';

export default {
  data() {
    return {
      isLoading: true,
    };
  },
  mounted() {
    setTimeout(() => {
      this.isLoading = false;
    }, 1000);
  },
  // components: {
  //   HelloWorld,
  // },
};
</script>

<style scoped>
</style>
