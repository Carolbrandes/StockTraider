<template>
  <div id="app">
    <Header />
    <router-view />
  </div>
</template>

<script>
export default {
  components: {
    Header: () => import("@/components/Header.vue"),
  },
};
</script>

<style lang="scss"></style>
