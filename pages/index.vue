<template>
  <el-container>
    <el-main>
      <h1>Agendas</h1>
      <todo-list :todos="todos" @delete="removeTodo($event)" @completed="removeTodo($event)" />
    </el-main>
    <el-main>
      <h1>Contactos</h1>
      <contact-list :contacts="contacts" @delete="deleteContact($event)" />
    </el-main>    
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
    removeTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id)
    },

    deleteContact(id) {
      this.contacts = this.contacts.filter((contact) => contact.id !== id)
    },
  },
}
</script>

<style scoped>
  .el-main {
    text-align: center;
    padding: 0;
  }
</style>