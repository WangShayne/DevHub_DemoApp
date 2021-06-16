<template>
  <div>
    <div v-if="!$auth.isAuthenticated">
      <el-form ref="loginForm" :model="loginForm" label-width="80px">
        <el-form-item label="email">
          <el-input v-model="loginForm.email"></el-input>
        </el-form-item>
        <el-form-item label="password">
          <el-input v-model="loginForm.password"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="login">login</el-button>
        </el-form-item>
      </el-form>

      <nuxt-link to="/register">Need an account? Register</nuxt-link>
    </div>

    <!-- Authenticated -->
    <div v-else>
      You're logged in as {{ $auth.email }}.
      <el-button @click="$store.dispatch('auth/logout')">Logout</el-button>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    loginForm: {
      email: "",
      password: "",
    },
  }),
  methods: {
    async login() {
      try {
        await this.$store.dispatch("auth/login", this.loginForm);
        this.$router.push("/");
      } catch (error) {
        console.log({ error });
      }
    },
  },
};
</script>