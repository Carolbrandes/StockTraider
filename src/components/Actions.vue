<template>
  <div class="row my-5">
    <div
      class="col-md-4 col-12 mb-4"
      v-for="(action, index) in actions"
      :key="index"
    >
      <Action
        :nome="action.nome"
        :preco="action.preco"
        :id="action.id"
        :qtdAcoes="0"
        :acoesAdquiridas="0"
      >
        <b-button
          slot="button"
          variant="success"
          @click="
            buy({
              id: action.id,
              nome: action.nome,
              preco: action.preco,
            })
          "
          >Comprar</b-button
        >
      </Action>
    </div>
  </div>
</template>

<script>
export default {
  props: ["actions"],

  components: {
    Action: () => import("@/components/Action.vue"),
  },

  methods: {
    buy(acao) {
      if (!this.$store.state.loggedInUser) {
        this.$router.push("/login");
      } else {
        if (
          this.$store.state.acaoSelecionada.quantidade > 0 &&
          Number.isInteger(this.$store.state.acaoSelecionada.quantidade)
        ) {
          console.log("comprando acao");
          this.$store.commit("SET_ACAO_SELECIONADA", acao);
          this.$store.commit("CHANGE_SALDO", { buy: true });
          this.$store.dispatch("buyAction");
        }
      }
    },
  },
};
</script>

<style></style>
