<template>
  <div class="login">
    <h1>Login</h1>

    <button @click.prevent="login">Login</button>
  </div>
</template>

<script>
import sha256 from 'sha256';

export default {
  name: 'login',
  data() {
    return {
      form: {
        email: '',
        password: '',
      },
    };
  },
  methods: {
    login() {
      const codeVerifier = this.generateString();
      const state = this.generateString(36);

      localStorage.setItem('login-code-verifier', codeVerifier);
      localStorage.setItem('login-state', state);

      window.location = 'http://localhost:8000/oauth/authorize?'+
              'client_id=3&'+
              `redirect_uri=http://localhost:8080/callback&`+
              `response_type=code&`+
              `scope=&`+
              `state=${state}&`+
              `code_challenge=${codeVerifier}&`+
              `code_challenge_method=plain`;
    },
    generateString(length = 128) {
      let random_string = '';
      let random_ascii;
      for(let i = 0; i < length; i++) {
        random_ascii = Math.floor((Math.random() * 25) + 97);
        random_string += String.fromCharCode(random_ascii)
      }
      return random_string
    }
}
}
</script>
