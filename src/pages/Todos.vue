<template>
  <q-page>
    <h1>Todos</h1>
    <q-list>
      <q-item v-for="todo in todos" :key="todo.id">
        <q-item-section>{{ todo.title }}</q-item-section>
        <q-item-section>
          <q-checkbox v-model="todo.completed" label="Completed" />
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { ref, onMounted } from 'vue';
import axios from 'axios';

export default {
  name: 'Todos',
  setup() {
    const todos = ref([]);

    const fetchTodos = async () => {
      const response = await axios.get('https://jsonplaceholder.typicode.com/todos');
      todos.value = response.data;
    };

    onMounted(fetchTodos);

    return {
      todos,
    };
  },
};
</script>
