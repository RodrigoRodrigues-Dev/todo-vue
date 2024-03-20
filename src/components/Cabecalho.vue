<script setup>
    const props = defineProps(['tarefasPedentes'])
</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p v-if="!tarefasPedentes <= 0">
        Você possui {{ props.tarefasPedentes }} tarefas pedentes
      </p>
      <p v-else>
        Você não possui tarefas pedentes
      </p>
    </header>
</template>