<template>
  <div>
    <div v-if="!$auth.isAuthenticated">
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
          <el-input v-model="registerForm.password"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="register">Register</el-button>
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
          <el-button type="primary" @click="confirm">confirm</el-button>
        </el-form-item>
      </el-form>

      <nuxt-link to="/login">Have an account? Login</nuxt-link>
    </div>

    <!-- Authenticated -->
    <div v-else>
      <Authenticated />
      <el-button @click="$store.dispatch('auth/logout')">Logout</el-button>
    </div>
  </div>
</template>

<script>
import Authenticated from "@/components/Authenticated.vue";

const steps = {
  register: 'REGISTER',
  confirm: 'CONFIRM'
}

export default {
  components: {
    Authenticated,
  },
  data: () => ({
    steps: { ...steps },
    step: steps.register,
    registerForm: {
      email: '',
      password: ''
    },
    confirmForm: {
      email: '',
      code: ''
    }
  }),
  methods: {
    async register() {
      try {
        await this.$store.dispatch('auth/register', this.registerForm)
        this.confirmForm.email = this.registerForm.email
        this.step = this.steps.confirm
      } catch (error) {
        console.log({ error })
      }
    },
    async confirm() {
      try {
        await this.$store.dispatch('auth/confirmRegistration', this.confirmForm)
        await this.$store.dispatch('auth/login', this.registerForm)
        this.$router.push('/')
      } catch (error) {
        console.log({ error })
      }
    }
  }
}
</script>