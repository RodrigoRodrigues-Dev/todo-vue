<script setup>
    const props = defineProps(['cadastrarNovaTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastrarNovaTarefa">
        <div class="row">
            <div class="col">
                <input type="text" required :value="props.tarefaTemp" @change="props.editaTarefaTemp" placeholder="Digite aqui a descrição da tarefa." class="form-control">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">Cadastrar</button>
            </div>
            <div class="col-md-3">
                <select @change="props.trocarFiltro" class="form-control text-center">
                <option value="todas">Todas tarefas</option>
                <option value="pedentes">Pedentes</option>
                <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
  </form>
</template>