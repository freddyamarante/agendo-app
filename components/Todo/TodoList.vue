<template>
  <div>
    <el-empty 
      v-if="todos.length === 0"
      description="No tienes contactos añadidos"
    >
    </el-empty>
    <todo 
      v-for="todo in todos" 
      v-else-if="todos.length !== 0"
      :key="todo.id"
      :todo="todo"
      @delete="$emit('delete', $event)"
    />
    <el-button 
      type="primary" 
      icon="el-icon-plus" 
      circle
      @click="$router.push('/todo/create')"
      ></el-button>
  </div>
</template>

<script >
export default {
  name: 'TodoList',
  props: {
    todos: {
      type: Array,
      required: true
    }
  }
}
</script>
