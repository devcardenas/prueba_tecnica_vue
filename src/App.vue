<script setup>
import { RouterView } from 'vue-router'
</script>

<template>
  <header>
    <v-card>
      <v-tabs v-model="tab" align-tabs="center" color="deep-purple-accent-4">
        <v-tab to="/">Consulta</v-tab>
        <v-tab to="/create">Alta</v-tab>
      </v-tabs>
    </v-card>
  </header>

  <RouterView />
</template>

<style scoped></style>