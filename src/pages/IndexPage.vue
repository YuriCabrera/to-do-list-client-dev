<template>
  <q-page class="bg-black flex flex-center">
    <div class="bg-white q-pa-lg shadow-2xl rounded-xl" style="width: 100%; max-width: 600px">
      <h4 class="text-center q-mb-md">📋 Lista de Tarefas</h4>

      <!-- Formulário -->
      <q-form @submit="criarTarefa" class="q-gutter-sm">
        <q-input v-model="novaTarefa.titulo" label="Título" outlined dense />
        <q-input v-model="novaTarefa.descricao" label="Descrição" outlined dense />
        <q-btn type="submit" label="Adicionar" color="primary" />
      </q-form>

      <q-separator class="q-my-md" />

      <!-- Lista de Tarefas -->
      <div v-if="tarefas.length > 0">
        <q-list bordered separator>
          <q-item v-for="tarefa in tarefas" :key="tarefa.id">
            <q-item-section>
              <div :class="{ 'text-strike': tarefa.concluida }">
                <strong>{{ tarefa.titulo }}</strong>
                <div class="text-caption">{{ tarefa.descricao }}</div>
              </div>
            </q-item-section>
            <q-item-section side>
              <q-btn dense flat icon="check" color="green" @click="concluirTarefa(tarefa.id)" />
              <q-btn dense flat icon="delete" color="red" @click="excluirTarefa(tarefa.id)" />
            </q-item-section>
          </q-item>
        </q-list>
      </div>
      <div v-else class="text-center text-grey q-mt-md">Nenhuma tarefa cadastrada.</div>
    </div>
  </q-page>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const novaTarefa = ref({
  titulo: '',
  descricao: '',
})

const tarefas = ref([])

const API_URL = 'http://127.0.0.1:8000/api/tarefa' // ajuste se necessário

const carregarTarefas = async () => {
  const resposta = await axios.get(API_URL)
  tarefas.value = resposta.data
}

const criarTarefa = async () => {
  await axios.post(API_URL, novaTarefa.value)
  novaTarefa.value = { titulo: '', descricao: '' }
  carregarTarefas()
}

const concluirTarefa = async (id) => {
  const tarefa = tarefas.value.find((t) => t.id === id)
  if (!tarefa) return

  await axios.put(`${API_URL}/${id}`, {
    ...tarefa,
    concluida: true,
  })
  carregarTarefas()
}

const excluirTarefa = async (id) => {
  await axios.delete(`${API_URL}/${id}`)
  carregarTarefas()
}

onMounted(carregarTarefas)
</script>

<style>
.text-strike {
  text-decoration: line-through;
}
</style>
