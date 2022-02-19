<template>
  <nav class="navbar navbar-expand-md navbar-dark bg-dark mb-4">
    <div class="container-fluid">
      <router-link to="/" class="navbar-brand">Home</router-link>
      <div>
        <ul class="navbar-nav me-auto mb-2 mb-md-0" v-if="!auth">
          <li class="nav-item">
            <router-link to="/login" class="nav-link active">Login</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/register" class="nav-link active">Register</router-link>
          </li>
        </ul>
        <ul class="navbar-nav me-auto mb-2 mb-md-0" v-if="auth">
          <li class="nav-item">
            <router-link to="/login" class="nav-link active" @click="logout">Logout</router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script lang="ts">
import axios from 'axios';
import { computed } from 'vue';
import store from '@/store';
import router from '@/router';
export default {
  name: "Nav",
  setup() {
     const auth = computed(() => store.state.authenticated);

     const logout = async () => {
        await axios.post('/logout', {}, { withCredentials: true });
        axios.defaults.headers.common['Authorization'] = '';
        await store.dispatch("setAuth", false);
        await router.push('/login');
     };

     return {
        auth,
        logout
     };
  }
};
</script>