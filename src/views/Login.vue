<template>
  <form @submit.prevent="submit">
    <h1 class="h3 mb-3 fw-normal">Please sign in</h1>
    <input
      name="username"
      type="text"
      class="form-control"
      placeholder="Username"
      required
    />
    <input
      name="password"
      type="password"
      class="form-control"
      placeholder="Password"
      required
    />
    <button class="w-100 btn btn-lg btn-primary" type="submit">Sign in</button>
  </form>
</template>

<script lang="ts">
import router from "@/router";
import axios from "axios";
export default {
  name: "Login",
   setup() {
      const submit = async (e: { target: HTMLFormElement | undefined; }) => {
         const form = new FormData(e.target);
         const inputs = Object.fromEntries(form.entries());

         const { data } = await axios.post('/login', inputs, { withCredentials: true });
         if (data.success) {
            axios.defaults.headers.common['Authorization'] = `Bearer ${data.token}`;
            await router.push('/');
         }
      };

      return {
         submit
      };
   }
};
</script>

<style scoped>
</style>