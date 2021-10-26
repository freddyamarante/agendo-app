<template>
  <el-container>
    <el-row :gutter="12">
      <el-col :span="12">
      <todo-list :todos="todos"/>
      </el-col>
    </el-row>
  </el-container>
</template>

<script>
export default {
  middleware: 'auth',
  async asyncData({ $axios }) {
    const todos = await $axios.$get('http://localhost:3333/todos')
    return { todos }
  },
  data: () => ({
    todos: {},
  }),
}
</script>
