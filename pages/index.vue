<template>
  <div>
    <div v-if="!$auth.isAuthenticated">
        <nuxt-link to="/login" class="button--grey">Login</nuxt-link>
        <nuxt-link to="/register" class="button--green">Register</nuxt-link>
      </div>

      <!-- Authenticated -->
      <div v-else>
        <!-- <p>You're logged in as {{ $auth.email }}</p> -->
        <button @click="$store.dispatch('auth/logout')" class="button--grey">Logout</button>
        <Authenticated />
      </div>
  </div>

</template>
<script>
import Authenticated from '@/components/Authenticated.vue'

export default {
  components:{
    Authenticated
  },
  created() {
  },
  destroyed() {
  },
  methods: {
  }
}
</script>
