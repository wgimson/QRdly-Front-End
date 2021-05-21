<template>
    <Login />
</template>
<script>
// @ is an alias to /src
import Login from '@/components/login.vue'
const API_URL = "http://localhost:8080/login";
export default {
  name: 'loginComponent',
  Components: {
    Login
  },
  methods: {
    addMessage() {
      console.log(this.message);
      fetch(API_URL, {
        method: "POST",
        body: JSON.stringify(this.message),
        headers: {
          "content-type": "application/json"
        }
      })
        .then(response => response.json())
        .then(result => {
          if (result.details) {
            // there was an error...
            const error = result.details
              .map(detail => detail.message)
              .join(". ");
            this.error = error;
          } else {
            this.error = "";
            this.showMessageForm = false;
            this.messages.push(result);
          }
        });
    }
  }
}
</script>
