<template>
  <div>
    <todo 
      v-for="todo in todos" 
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
