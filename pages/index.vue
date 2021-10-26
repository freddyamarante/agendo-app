<template>
  <el-container>
    <el-row :gutter="20">
      <el-col :span="12">
        <h1>Agendas</h1>
        <todo-list :todos="todos" />
      </el-col>
      <el-col :span="12">
        <h1>Contactos</h1>
        <contact-list :contacts="contacts" />
      </el-col>
    </el-row>
  </el-container>
</template>

<script>
export default {
  middleware: 'auth',
  async asyncData({ $axios }) {
    const todos = await $axios.$get('http://localhost:3333/todos')
    const contacts = await $axios.$get('http://localhost:3333/contacts')
    return { todos, contacts }
  },
  data: () => ({
    todos: {},
    contacts: {},
  }),
}
</script>

