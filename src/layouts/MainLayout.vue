<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-transparent">
      <q-toolbar>
        <!-- Título vazio ou personalizado -->
        <q-toolbar-title> </q-toolbar-title> 

        <!-- Removido a exibição da versão -->
        <!-- <div>Quasar v{{ $q.version }}</div> -->
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
// Nenhuma alteração necessária no script
</script>

<style scoped>
/* Remover a cor de fundo do cabeçalho ou personalizar */
.q-header {
  background-color: transparent; /* Torna o cabeçalho transparente */
}

.q-toolbar {
  background-color: transparent; /* Torna a barra de ferramentas também transparente */
}
</style>
