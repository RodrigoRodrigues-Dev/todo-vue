<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false      
      },
      {
        titulo: 'Estudar SASS',
        finalizada: false      
      },
      {
        titulo: 'Ir para a academia',
        finalizada: true      
      }
    ]
  })

  const getTarefasPedentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasPedentesFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const tarefasFiltradas = () => {
    const {filtro} = estado;

    switch (filtro) {
      case 'pedentes':
        return getTarefasPedentes();
      case 'finalizadas':
        return getTarefasPedentesFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastrarNovaTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false   
    }

    estado.tarefas.push(tarefaNova)
    estado.tarefaTemp = '';
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{ getTarefasPedentes().length }} tarefas pedentes
      </p>
    </header>
    <form @submit.prevent="cadastrarNovaTarefa()">
    <div class="row">
      <div class="col">
        <input type="text" required :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" placeholder="Digite aqui a descrição da tarefa." class="form-control">
      </div>
      <div class="col-md-2">
        <button class="btn btn-primary" type="submit">Cadastrar</button>
      </div>
      <div class="col-md-3">
        <select @change="evento => estado.filtro = evento.target.value" class="form-control text-center">
          <option value="todas">Todas tarefas</option>
          <option value="pedentes">Pedentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in tarefasFiltradas()">
      <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
      <label :class="{ done: tarefa.finalizada === true }" :for="tarefa.titulo" class="ms-3">
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
  </div>
</template>

<style scoped>
  .done {
    color: green;
    text-decoration: line-through;
  }
</style>
