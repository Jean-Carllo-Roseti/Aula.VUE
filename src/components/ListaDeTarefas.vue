<script setup>
    console.log('a lista esta sendo renderizada.');
    const props = defineProps (['tarefas']);
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox"
                @change="evento => tarefa.finalizada = evento.target.checked">
            <label :class="{ done: tarefa.finalizada }" class="ms-1" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>