
<template>
    <form @submit.prevent="submit">
      <label for="username">username</label>
        <input type="text" v-model="username"> 
        <label for="username">password</label>
         <input type="text" v-model="password"> 
         <button type="submit">
            Login
        </button>
    </form>
</template>
<script>
import axios from 'axios';

export default {
   data() {
     return{
       username : '',
       password: ''
     }
   },
   methods : {
      submit(){
          axios.post('http://localhost:8080/login',
          {
            headers: { "Access-Control-Allow-Origin": "*" },
          },
          {
            username: this.username,
            password: this.password,

          })
          .then(res => {
              console.log(res.message);
          })
          .catch(err => {
            console.log(err.message);
         })
      }
  },
  mounted () {

  },
  components: {

  }
}
</script>

