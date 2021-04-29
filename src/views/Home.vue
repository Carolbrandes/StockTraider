<template>
  <div class="home container">
    <div v-if="$store.state.acoes.length > 0">
      <Actions :actions="$store.state.acoes" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  components: {
    Actions: () => import("@/components/Actions.vue"),
  },
  created() {
    this.$store.dispatch("getActions");
  },
};
</script>
