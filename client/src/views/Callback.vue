<template>
    <div>
        Authenticating...
    </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "Callback.vue",
  mounted() {
      const query = new URLSearchParams(window.location.search);
      const code = query.get('code');
      const state = query.get('state');

      if (!this.matchState(state)) {
        return this.$router.push('login');
      }

      const data = new FormData();
      data.append('grant_type', 'authorization_code');
      data.append('client_id', 3);
      data.append('redirect_uri', 'http://localhost:8080/callback');
      data.append('code', code);
      data.append('code_verifier', localStorage.getItem('login-code-verifier'));

      axios.post('http://localhost:8000/oauth/token', data)
          .then((resp) => {
              console.log(resp.data);
          });
  },
  methods: {
    matchState(state) {
      const localState = localStorage.getItem('login-state');
      return localState && state === localState;
    }
  }
}
</script>
