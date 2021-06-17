<template>
  <div>
    <div v-show="!$auth.isAuthenticated">
        <nuxt-link to="/login" class="button--grey">
          Login
        </nuxt-link>
        <nuxt-link to="/register" class="button--green">
          Register
        </nuxt-link>
      </div>

      <!-- Authenticated -->
      <div v-show="$auth.isAuthenticated">
        <Authenticated />
        <button @click="$store.dispatch('auth/logout')" class="button--grey">Logout</button>
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
