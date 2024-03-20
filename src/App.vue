<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

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

  const getTarefasFiltradas = () => {
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
    <Cabecalho :tarefas-pedentes="getTarefasPedentes().length"/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastrar-nova-tarefa="cadastrarNovaTarefa"/>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
  </div>
</template>


