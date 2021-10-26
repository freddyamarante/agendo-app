<template>
  <div>
    <todo 
      v-for="todo in todos" 
      :key="todo.id"
      :todo="todo"
    />
  </div>
</template>

<script >
export default {
  name: 'TodoList',
  props: {
    todos: {
      type: Object,
      required: true
    }
  }
}
</script>
