<template>
  <div class="home">
    <form action="" method="post" @submit.prevent="login">
      <div>
        <input type="email" name="email" id="email">
      </div>
      <div>
        <input type="password" name="password" id="password">
      </div>
      <div>
        <button type="submit">Login</button>
      </div> 
    </form>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'

axios.defaults.withCredentials = true;
axios.defaults.baseUrl = 'http://localhost:8000'

export default {
  name: 'Home',
  methods: {
    login() {
      axios.get('http://localhost:8000/sanctum/csrf-cookie').then(response => {
        axios.post('http://localhost:8000/login', {
          email:'admin@example.com',
          password:'12345678'
        })
        .then(response => {
          this.$router.push({ name: 'Dashboard'})
        })
      });
    }
  }
}
</script>
