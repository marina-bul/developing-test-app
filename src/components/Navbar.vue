<template>
  <v-app-bar class="indigo darken-3">
    <v-spacer></v-spacer>
    <v-btn @click="$router.push('/')">Главная</v-btn>
  </v-app-bar>
</template>

<script>
export default {
  name: "navbar-header",
};
</script>
