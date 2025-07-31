<template>
  <q-page>
    <TarefasList @tarefa-adicionada="getTarefas" />
    <TarefaForm />
  </q-page>
</template>

<script>
import TarefasList from 'src/components/TarefasList.vue'
import TarefaForm from 'src/components/TarefaForm.vue'

export default {
  components: {
    TarefasList,
    TarefaForm,
  },
  methods: {
    getTarefas() {
      // Chama a função do Tarefas para pegar as tarefas atualizadas
    },
  },
}
</script>
