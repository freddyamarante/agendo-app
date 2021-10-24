<template>
  <div>
    <todo-list
     :todos="todos"/>
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
