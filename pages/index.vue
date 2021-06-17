<template>
  <div class="home">
    <el-container style="height: 100vh">
      <el-aside width="250px">
        <Aside />
      </el-aside>

      <el-container>
        <el-header>
          <h3>Completed Bookings</h3>
        </el-header>
        <el-main>
          <div v-for="o in 4" :key="o" style="margin-bottom: 20px">
            <Card :title="title" :information="info" :paid="paid" />
          </div>
        </el-main>
      </el-container>
    </el-container>

    <!-- <div v-show="!$auth.isAuthenticated">
        <nuxt-link to="/login" class="button--grey">
          Login
        </nuxt-link>
        <nuxt-link to="/register" class="button--green">
          Register
        </nuxt-link>
      </div>

      <div v-show="$auth.isAuthenticated">
        <Authenticated />
        <button @click="$store.dispatch('auth/logout')" class="button--grey">Logout</button>
      </div> -->
  </div>
</template>
<script>
import Aside from "@/components/Aside.vue";
import Card from "@/components/Card.vue";
import Authenticated from "@/components/Authenticated.vue";

const info = [
  { name: "Contact Name", value: "Tom Bruce" },
  { name: "Contact Number", value: "0488 888 888" },
  { name: "Service Address", value: "12 West St, Canley Vale, NSW 2166" },
  { name: "Service Time", value: "Morning 8AM-11AM, 11 December 2019" },
];

const paid = [
  { name: "Amount Paid", value: "50" },
  { name: "Refunded", value: "50" },
];

export default {
  components: {
    Aside,
    Card,
    Authenticated,
  },
  data() {
    return {
      title: "Interior Lightning Service",
      info,
      paid,
    };
  },
  created() {},
  destroyed() {},
  methods: {},
};
</script>

<style>
.home {
  padding: 20px;
}
</style>
