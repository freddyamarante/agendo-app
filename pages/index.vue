<template>
  <el-container>
    <el-row :gutter="20">
      <el-col :span="12">
        <h1>Agendas</h1>
        <todo-list :todos="todos" @delete="deleteTodo($event)"/>
      </el-col>
      <el-col :span="12">
        <h1>Contactos</h1>
        <contact-list :contacts="contacts" @delete="deleteContact($event)" />
      </el-col>
    </el-row>
  </el-container>
</template>

<script>
export default {
  middleware: 'auth',
  async asyncData({ $axios }) {
    const todos = await $axios.$get('http://localhost:3333/todos/?completed=0')
    const contacts = await $axios.$get('http://localhost:3333/contacts')
    return { todos, contacts }
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },

    deleteContact(id) {
      this.contacts = this.contacts.filter(contact => contact.id !== id)
    }
  }
}
</script>

