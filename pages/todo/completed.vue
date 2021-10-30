<template>
  <el-container>
    <el-main>
      <h1>Agendas Completadas</h1>
      <todo-list :todos="todos" type="completed"/>
    </el-main> 
  </el-container>
</template>

<script>
export default{
  name: 'CompletedTodos',
  layout: 'default',
  middleware: 'auth',
  async asyncData({ $axios }) {
      const todos = await $axios.$get('http://localhost:3333/todos/?completed=1')
      return { todos }
    }
}
</script>