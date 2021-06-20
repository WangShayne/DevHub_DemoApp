<template>
  <div>
    <el-card style="width: 500px">
      <el-form
        v-if="step === steps.register"
        ref="registerForm"
        :model="registerForm"
        label-width="80px"
      >
        <el-form-item label="email">
          <el-input v-model="registerForm.email"></el-input>
        </el-form-item>
        <el-form-item label="password">
          <el-input type="password" v-model="registerForm.password" show-password></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="register" :loading="loadingReg"
            >Register</el-button
          >
        </el-form-item>
      </el-form>

      <el-form v-else ref="confirmForm" :model="confirmForm" label-width="80px">
        <el-form-item label="email">
          <el-input v-model="confirmForm.email"></el-input>
        </el-form-item>
        <el-form-item label="code">
          <el-input v-model="confirmForm.code"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="confirm" :loading="loadingCof"
            >confirm</el-button
          >
        </el-form-item>
      </el-form>

      <nuxt-link to="/login">Have an account? Login</nuxt-link>
    </el-card>
  </div>
</template>

<script>
import Authenticated from "@/components/Authenticated.vue";
import Card from "~/components/Card.vue";

const steps = {
  register: "REGISTER",
  confirm: "CONFIRM",
};

export default {
  components: {
    Authenticated,
    Card,
  },
  data: () => ({
    steps: { ...steps },
    step: steps.register,
    registerForm: {
      email: "",
      password: "",
    },
    confirmForm: {
      email: "",
      code: "",
    },
    loadingReg: false,
    loadingCof: false,
  }),
  methods: {
    async register() {
      this.loadingReg = true;
      try {
        await this.$store.dispatch("auth/register", this.registerForm);
        this.confirmForm.email = this.registerForm.email;
        this.step = this.steps.confirm;
        this.loadingReg = false;
      } catch (error) {
        this.loadingReg = false;
        console.log({ error });
      }
    },
    async confirm() {
      this.loadingCof = true;
      try {
        await this.$store.dispatch(
          "auth/confirmRegistration",
          this.confirmForm
        );
        await this.$store.dispatch("auth/login", this.registerForm);
        this.$router.push("/");
      } catch (error) {
        this.loadingCof = false;
        console.log({ error });
      }
    },
  },
};
</script>