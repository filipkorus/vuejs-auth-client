<template>
  <form @submit.prevent="submit">
    <h1 class="h3 mb-3 fw-normal">Please register</h1>
    <input
      name="username"
      type="text"
      class="form-control"
      placeholder="Username"
      required
    />
    <input
      name="email"
      type="email"
      class="form-control"
      placeholder="Email"
      required
    />
    <input
      name="password"
      type="password"
      class="form-control"
      placeholder="Password"
      required
    />
    <button class="w-100 btn btn-lg btn-primary" type="submit">Submit</button>
  </form>
</template>

<script lang="ts">
import router from "@/router";
import axios from "axios";
export default {
  name: "Register",
  setup() {
    const submit = async (e: { target: HTMLFormElement | undefined; }) => {
      const form = new FormData(e.target);
      const inputs = Object.fromEntries(form.entries());

      const { data } = await axios.post('/register', inputs);
      if (data.success) {
         await router.push('/login');
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