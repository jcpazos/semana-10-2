<template>
  <img alt="TODOs logo" src="./assets/todos-icon.png">
  <HelloWorld msg="Welcome to your TODOs app"/>
  <TodoLogin @user-login="onUserLogin" v-if="!loggedIn"></TodoLogin>
  <TodoMain v-if="loggedIn"></TodoMain>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import TodoMain from './components/TodoMain.vue'
import TodoLogin from './components/TodoLogin.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    TodoMain,
    TodoLogin
  },
  data () {
    return {
      loggedIn: false
    }
  },
  created() {
    if (sessionStorage.getItem('user')) {
      this.loggedIn = true;
    }
  },
  methods: {
    onUserLogin() {
      this.loggedIn = true;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
