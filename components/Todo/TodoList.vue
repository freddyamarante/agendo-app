<template>
  <div>
    <el-empty 
      v-if="todos.length === 0"
      description="No tienes agendas añadidas"
    >
    </el-empty>
    <todo 
      v-for="todo in todos" 
      v-else-if="todos.length !== 0"
      class="el-button-center"
      :key="todo.id"
      :todo="todo"
      @delete="$emit('delete', $event)"
      @completed="$emit('completed', $event)"
    />
    <el-button 
      v-if="type === 'all'"
      class="el-button-center"
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
    },
    type: {
      type: String,
      default: 'all'
    }
  }
}
</script>

<style scoped>
.el-button-center {
  margin: 0 auto;
  display: block;
}
</style>