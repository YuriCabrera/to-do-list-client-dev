<template>
  <div>
    <h2>Lista de Tarefas</h2>
    <q-list bordered>
      <q-item v-for="tarefa in tarefas" :key="tarefa.id">
        <q-item-section>
          <q-item-label>{{ tarefa.titulo }}</q-item-label>
          <q-item-label caption>{{ tarefa.descricao }}</q-item-label>
        </q-item-section>
        <q-item-section side>
          <q-btn @click="deleteTarefa(tarefa.id)" color="negative" icon="delete" flat />
        </q-item-section>
      </q-item>
    </q-list>
    <q-btn @click="showForm = !showForm" label="Adicionar Tarefa" color="primary" />
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      tarefas: [],
      showForm: false,
    };
  },
  mounted() {
    this.getTarefas();
  },
  methods: {
    getTarefas() {
      axios.get('http://localhost:8000/api/tarefas') // Substitua pela URL da sua API Laravel
        .then(response => {
          this.tarefas = response.data;
        })
        .catch(error => {
          console.error("Erro ao obter tarefas:", error);
        });
    },
    deleteTarefa(id) {
      axios.delete(`http://localhost:8000/api/tarefas/${id}`)
        .then(() => {
          this.getTarefas(); // Atualiza a lista após a exclusão
        })
        .catch(error => {
          console.error("Erro ao excluir tarefa:", error);
        });
    },
  },
};
</script>
