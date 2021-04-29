<template>
  <div class="login container my-5">
    <div class="row">
      <div class="col-md-6 col-12 pb-3 divisor-forms">
        <div class="mb-3">
          <label for="email">E-mail</label>
          <b-form-input id="email" type="email" v-model="email"></b-form-input>
        </div>

        <div class="mb-3">
          <label for="senha">Senha</label>
          <b-form-input
            id="senha"
            type="password"
            v-model="senha"
          ></b-form-input>
        </div>

        <b-button variant="dark" @click="login">Entrar</b-button>

        <b-alert v-if="errorlogin" show variant="danger"
          >E-mail e/ou senha inválidos</b-alert
        >
      </div>

      <div class="col-md-6 col-12 pb-3">
        <div class="mb-3">
          <label for="nome">Nome</label>
          <b-form-input id="nome" type="text"></b-form-input>
        </div>
        <div class="mb-3">
          <label for="email">E-mail</label>
          <b-form-input id="email" type="email"></b-form-input>
        </div>

        <div class="mb-3">
          <label for="senha">Senha</label>
          <b-form-input id="senha" type="password"></b-form-input>
        </div>

        <b-button variant="dark">Cadastrar</b-button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import api from "../apiBase";

export default {
  data() {
    return {
      errorlogin: false,
    };
  },
  computed: {
    email: {
      get() {
        return this.$store.state.user.email;
      },

      set(value) {
        this.$store.commit("SET_USER", { email: value });
      },
    },

    senha: {
      get() {
        return this.$store.state.user.senha;
      },

      set(value) {
        this.$store.commit("SET_USER", { senha: value });
      },
    },
  },
  methods: {
    login() {
      axios.get(`${api.apiBase}/usuarios`).then((res) => {
        console.log(res.data);
        console.log(this.$store.state.user);

        const usuario = res.data.find(
          (user) =>
            user.email === this.$store.state.user.email &&
            user.senha === this.$store.state.user.senha
        );
        console.log(usuario);

        if (usuario) {
          this.$store.commit("SET_LOGGED_IN_USER", true);
          this.$router.push("/");
        } else {
          this.errorlogin = true;
        }
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.divisor-forms {
  border-bottom: 2px solid;

  @media (min-width: 720px) {
    border-bottom: none;
    border-right: 2px solid;
  }
}
</style>
