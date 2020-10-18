<template>
  <v-app>
    <!-- <v-navigation-drawer app></v-navigation-drawer> -->

    <v-toolbar app color="red" dark fixed>
      <v-toolbar-title class="mr-4">Projects Manager</v-toolbar-title>
       <v-toolbar-items class="hidden-sm-and-down">
        <v-btn v-if="token" flat to="/">
          <v-icon class="mr-2">playlist_add_check</v-icon>
          Projects
        </v-btn>
      </v-toolbar-items>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-btn v-if="!token" flat to="/register">
          Register
        </v-btn>
        <v-btn v-if="!token" flat to="/login">
          Login
        </v-btn>
        <v-btn v-if="token" flat @click="logout">
          <v-icon class="mr-2">exit_to_app</v-icon>
          Logout
        </v-btn>
      </v-toolbar-items>
    </v-toolbar>

    <v-content>
      <v-container fluid>
        <router-view></router-view>
      </v-container>
    </v-content>
    <v-footer app></v-footer>
  </v-app>
</template>

<script>
import { mapState, mapMutations } from 'vuex';
import router from './router';

export default {
  computed: {
    ...mapState('authentication', [
      'token',
    ]),
  },
  methods: {
    ...mapMutations('authentication', [
      'setToken',
    ]),
    logout() {
      this.setToken(null);
      router.push('/login');
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #b41f1f;
}
</style>
