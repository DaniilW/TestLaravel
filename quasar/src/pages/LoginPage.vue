<template>
  <form @submit.prevent="onLogin">
    {{ user }}
    <div class="q-pa-md">
      <div class="q-gutter-md" style="max-width: 300px">
        <q-input v-model="Form.email" label="Почта" type="email" />
        <q-input v-model="Form.password" label="Пароль" type="password" />
        <button class="" type="submit">Войти</button>
      </div>
    </div>
  </form>
</template>

<script setup lang="ts">
  import { ref } from 'vue';
  import axios from 'axios';

  axios.defaults.withCredentials = true;

  const Form = ref({
    email: null,
    password: null
  });

  const user = ref();

  // function formSumbit() {
  //   const data = {
  //     email: Form.value.email,
  //     password: Form.value.password
  //   }
  //
  //   axios.get('http://localhost:8000/sanctum/csrf-cookie').then( async () => {
  //     axios.post('http://localhost:8000/api/home').then((response) => {
  //       console.log(response)
  //     })
  //   })
  // }

  async function onLogin() {
    await axios.get('http://localhost:8000/sanctum/csrf-cookie');
    await axios.post('http://localhost:8000/login', {
      email: Form.value.email,
      password: Form.value.password
    }).then((response) => {
      console.log(response);
    });

    let {data} = await axios.get('http://localhost:8000/api/user');
    console.log(data);
    user.value = data;
  }
</script>

