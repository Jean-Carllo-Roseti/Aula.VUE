<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: []
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada);
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada);
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp, 
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
  }
  
</script>

<template>
<div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
        <p>
          Você possui {{ getTarefasPendentes().length }} tarefas pendentes.
        </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input @change="evento => estado.tarefaTemp = evento.target.value" required class="form-control" type="text" placeholder="digita a tarefa!!">
        </div>
          <div class="col-md-2">
            <button type="submit" class="btn btn-primary">Cadastar</button>
          </div>
          <div class="col-md-2">
            <select @change="evento => estado.filtro = evento.target.value" class="form-control">
              <option value="todas">todas tarefas</option>
              <option value="pendentes"> pendentes</option>
              <option value="finalizadas"> finalizadas</option>
            </select>
          </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox" @change="evento => tarefa.finalizada = evento.target.checked">
        <label :class="{ done: tarefa.finalizada }" class="ms-1" :for="tarefa.titulo" >
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
</div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}

</style>
