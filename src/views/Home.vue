<template>{{ message }}</template>

<script lang="ts">
import router from "@/router";
import store from "@/store";
import axios from "axios";
import {onMounted, ref} from "vue";
export default {
  name: "Home",
  setup() {
    const message = ref('You are not logged in!');

   onMounted(async () => {
      try {
         const {data} = await axios.get('/user');

         if (data.success) {
            await store.dispatch("setAuth", true);
            message.value = `Hi ${data.user.username}`;
         }
      } catch (e) {
         await store.dispatch("setAuth", false);
         await router.push('/login');
      }
   });

    return {
      message
    };
  },
};
</script>

<style scoped>
</style>