<template>
  <div class="container my-5">
   {{$store.state.acaoSelecionada}}
    <div class="row">
      <div v-for="action in  $store.getters.userAcoes" :key="action.id" class="col-md-4 col-12 mb-4">
        <Action :nome="action.nome" :preco="action.preco" :acoesAdquiridas="action.quantidade">
           <b-button
          slot="button"
          variant="success"
          @click="
            venderAcao({
              id: action.id,
              nome: action.nome,
              preco: action.preco,
              acoesObtidas:action.quantidade
            })
          "
          >Vender</b-button
        >
        </Action>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {
    Action: () => import("@/components/Action.vue"),
  },

  methods: {
    venderAcao(acao){
      console.log("vamos vender")
       this.$store.commit("SET_ACAO_SELECIONADA", acao);
        if (
          this.$store.state.acaoSelecionada.quantidade > 0 &&
          Number.isInteger(this.$store.state.acaoSelecionada.quantidade) && this.$store.state.acaoSelecionada.quantidade <= acao.acoesObtidas
        ) {
          console.log("vendendo acao");
          
         if( this.$store.state.acaoSelecionada.quantidade < acao.acoesObtidas){
            this.$store.dispatch("sellAction", {sell: "algumas"})
         }

          if( this.$store.state.acaoSelecionada.quantidade == acao.acoesObtidas){
            console.log("vendi todas")
            this.$store.dispatch("sellAction", {sell: "todas"})
         }

        }
    }
  }
};
</script>

<style></style>
