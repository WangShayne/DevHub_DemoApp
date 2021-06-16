<template>
  <div>
    <div v-if="!$auth.isAuthenticated">
        <nuxt-link to="/login" class="button--grey">Login</nuxt-link>
        <nuxt-link to="/register" class="button--green">Register</nuxt-link>
      </div>

      <!-- Authenticated -->
      <div v-else>
        <p>You're logged in as {{ $auth.email }}</p>
        <button @click="$store.dispatch('auth/logout')" class="button--grey">Logout</button>
      </div>
  </div>

</template>
<script>


export default {
  created() {
  },
  destroyed() {
  },
  methods: {
  }
}
</script>
