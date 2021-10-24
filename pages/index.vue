<template>
  <div>
    <div v-for="todo in todos" :key="todo.id">
      {{ todo.title }}
    </div>
  </div>
</template>

<script>
export default {
  middleware: 'auth',
  async asyncData({ $axios }) {
    const todos = await $axios.$get('http://localhost:3333/todos')
    return { todos }
  },
  data: () => ({
    todos: [],
  }),
}
</script>
