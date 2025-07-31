<template>
  <div>
    <q-dialog v-model="show">
      <q-card>
        <q-card-section>
          <div class="text-h6">Nova Tarefa</div>
        </q-card-section>

        <q-card-section>
          <q-input v-model="titulo" label="Título" />
          <q-input v-model="descricao" label="Descrição" />
        </q-card-section>

        <q-card-actions>
          <q-btn @click="saveTarefa" label="Salvar" color="primary" />
          <q-btn @click="show = false" label="Cancelar" color="negative" />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      show: false,
      titulo: '',
      descricao: '',
    };
  },
  methods: {
    saveTarefa() {
      axios.post('http://localhost:8000/api/tarefas', {
        titulo: this.titulo,
        descricao: this.descricao,
      })
      .then(() => {
        this.$emit('tarefa-adicionada');
        this.show = false;
        this.titulo = '';
        this.descricao = '';
      })
      .catch(error => {
        console.error("Erro ao salvar tarefa:", error);
      });
    },
  },
};
</script>
