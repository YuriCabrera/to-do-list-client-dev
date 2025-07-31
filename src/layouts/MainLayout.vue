<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-transparent">
      <q-toolbar>
        <q-toolbar-title> </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup></script>

<style scoped>
.q-header {
  background-color: transparent;
}

.q-toolbar {
  background-color: transparent;
}
</style>
