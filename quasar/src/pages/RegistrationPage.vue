<template>
  <form>
    {{ user }}
    <div class="q-pa-md">
      <div class="q-gutter-md" style="max-width: 300px">
        <q-input v-model="Form.name" label="Имя" type="text" />
        <q-input v-model="Form.email" label="Почта" type="email" />
        <q-input v-model="Form.password" label="Пароль" type="password" />
        <q-btn color="primary" label="Зарегистрироваться" @click="onRegister" />
      </div>
    </div>
  </form>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';

const Form = ref({
  name: null,
  email: null,
  password: null
});

const user = ref();

async function onRegister() {
  await axios.post('http://localhost:8000/register', {
    name: Form.value.name,
    email: Form.value.email,
    password: Form.value.password
  });
}
</script>

