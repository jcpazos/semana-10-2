<template>
    <div class="content-center">
      <label for="username">Username: </label>
      <input v-bind:value="username" v-on:input="onUsernameInput" name="username" id="username" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500  w-20">
      <br><br>
      <button v-on:click="onLogin" class="btn btn-secondary">Login!</button>
      <br><br>
    </div>
  </template>
  
  <script>
  export default {
    name: 'TodoLogin',
    props: {
    },
    data () {
        return {
            username: "",
        }
    },
    methods: {
        onUsernameInput(e) {
            this.loginAttempt = false;
            this.username = e.target.value;
        },
        onLogin() {
            sessionStorage.setItem('user', this.username);
            this.$emit('user-login');
        }
    }
  }

  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  </style>
  