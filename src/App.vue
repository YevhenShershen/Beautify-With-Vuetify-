<template>
  <v-app>
<v-card width="400" class="mt-5 mx-auto">
  <v-card-title>
    <h1 class="display-1">Login</h1>
  </v-card-title>
  <v-card-text>
    <v-form>
      <v-text-field
      label="Username"
      prepend-icon="mdi-account-circle"></v-text-field>
      <v-text-field
      type="password"
      label="Password"
      prepend-icon="mdi-lock"
      append-icon="mdi-eye-off"></v-text-field>
    </v-form>
  </v-card-text>
  <v-card-action>
    <v-btn color ="success">Register</v-btn>
    <v-btn color="info">Login</v-btn>
  </v-card-action>
</v-card>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "App",

  data: () => ({
    //
  }),
});
</script>
