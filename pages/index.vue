
<template>
  <v-layout column>
    <template v-if="$store.state.loggedIn">
      <v-flex>
        <v-btn color="primary" @click="logout()">
          <p>logout</p>
        </v-btn>
      </v-flex>
    </template>

    <template v-else>
      <v-flex>
        <v-alert
          :value="$route.query.showMessage"
          color="warning"
          icon="priority_high"
          outline
        >
          <p>ログイン認証してください。</p>
        </v-alert>
      </v-flex>

      <v-flex>
        <v-btn color="primary" @click="login()">
          <p>login</p>
        </v-btn>
      </v-flex>
    </template>
  </v-layout>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  },
  data() {
    return {
      newItem: '',
      todos: []
    }
  },
  methods: {
    addItem: function(event) {
      var todo = {
        item: this.newItem
      };
    this.todos.push(todo);
    },
    login() {
      this.$store.commit('login')

      // URL のクエリにリダイレクトが存在する場合はリダイレクトします。
      if (this.$route.query.redirect) {
        this.$router.push(this.$route.query.redirect)
      }
    },
    logout() {
      this.$store.commit('logout')
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
