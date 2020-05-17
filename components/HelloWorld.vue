<template>
  <div id="app">
    <div class="row" v-if="message" v-html="message"></div>
    <div class="row">
      <input type="text" v-model="hello">
    </div>
    <div class="row" v-html="hello"></div>
    <div class="row">
      <b-button @click="login()">
        login
      </b-button>
    </div>
    <div class="row">
      <b-button @click="getCars()">
        autod
      </b-button>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: "HelloWorld",
    data() {
      return {
        message: 'Hello world',
        hello: 'jomees'
      };
    },
    methods: {
      login() {
        axios({
          method: 'post',
          url: 'https://bron.back.dev.advertis.ee/api/login',
          data: {
            email: 'paan@paan.ee',
            password: 'tegelane'
          }
        }).then(answer => {
          if(answer?.data?.access_token){
            console.log('answer', answer);
            axios.defaults.headers.common.Authorization = `Bearer ${answer.data.access_token}`;
          }
        });
      },
      getCars() {
          axios({
            method: 'get',
            url: 'https://bron.back.dev.advertis.ee/api/cars'
          }).then(answer => {
            console.log('answer', answer);
          });
      }
    }
  }
</script>

<style scoped>

</style>
