<template>
  <router-view />
</template>

<script setup lang="ts">

import axios from 'axios';

axios.defaults.withCredentials = true;

</script>
