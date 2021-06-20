<template>
  <div>
    <el-card style="width:500px">
      <el-form ref="loginForm" :model="loginForm" label-width="80px">
        <el-form-item label="email">
          <el-input v-model="loginForm.email"></el-input>
        </el-form-item>
        <el-form-item label="password">
          <el-input v-model="loginForm.password" show-password></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="login" :loading="loading">login</el-button>
        </el-form-item>
      </el-form>

      <nuxt-link to="/register">Need an account? Register</nuxt-link>
    </el-card>
  </div>
</template>

<script>
import Authenticated from "@/components/Authenticated.vue";
export default {
  components: {
    Authenticated,
  },
  data: () => ({
    loginForm: {
      email: "",
      password: "",
    },
      loading: false,
  }),
  methods: {
    async login() {
      this.loading = true
      try {
        await this.$store.dispatch("auth/login", this.loginForm);
        this.$router.push("/");
      } catch (error) {
        this.loading = false
        console.log({ error });
      }
    },
  },
};
</script>