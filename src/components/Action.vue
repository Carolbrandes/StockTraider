<template>
  <b-card
    bg-variant="light"
    text-variant="dark"
    :header="nome"
    class="text-center"
  >
    <b-card-text>
      <h3 class="mb-4 text-primary">
        <b>{{ preco | money }}</b>
      </h3>
      <p v-if="$route.name === 'MinhasAcoes'">
        Número de Ações: {{ acoesAdquiridas }}
      </p>
      <b-col md="4" sm="6" class="mx-auto mb-4">
        <b-form-input
          type="number"
          placeholder="Qtd"
          v-model.number="qtdAcoes"
          min="0"
          :max="$route.name === 'MinhasAcoes' ? acoesAdquiridas : 20"
          @input="changeQuantify"
        ></b-form-input>
      </b-col>

      <b-col md="6" sm="12" class="mx-auto mb-4">
        <slot name="button"></slot>
      </b-col>
    </b-card-text>
  </b-card>
</template>

<script>
export default {
  props: ["id", "nome", "preco", "acoesAdquiridas"],

  data(){
    return{
      qtdAcoes: 0
    }
  },

  methods: {
    changeQuantify() {
      console.log("alterou a quantidade")
      this.$store.commit("SET_ACAO_SELECIONADA", { quantidade: this.qtdAcoes });
    },
  },
};
</script>

<style></style>
