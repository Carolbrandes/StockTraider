<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <div class="container">
        <b-navbar-brand to="/">StockTraider</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <b-navbar-nav class="align-items-center">
              <b-nav-item v-if="!$store.state.loggedInUser" to="/login"
                >Login / Criar Conta</b-nav-item
              >
              <b-nav-item v-if="$store.state.loggedInUser" href="#"
                >Olá {{ $store.state.user.nome }} | Saldo:
                {{ $store.getters.saldo | money }}</b-nav-item
              >
              <b-nav-item v-if="$store.state.loggedInUser" to="/minhas-acoes"
                >Minhas Ações</b-nav-item
              >

              <b-nav-item v-if="$store.state.loggedInUser" href="#">
                <b-button @click="changeActions" variant="warning"
                  >Novo Dia</b-button
                >
              </b-nav-item>
            </b-navbar-nav>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
import { BNavbar } from "bootstrap-vue";

export default {
  components: {
    BNavbar,
  },

  methods: {
    changeActions() {
      console.log("alterar acoes");
      this.$store.dispatch("changeActionsPrice");
    },
  },
};
</script>

<style scoped lang="scss">
.nav-item {
  padding: 0 1rem;

  a {
    color: #fff !important;

    &:hover {
      color: #ffd000 !important;
    }
  }
}
</style>
