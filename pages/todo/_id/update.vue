<template>
  <div>
    <h1>Editar Agenda</h1>
    <todo-form :todo-id="$route.params.id" type="update" />
  </div>
</template>

<script>
export default {
  name: 'UpdateTodo',
  layout: 'action',
  middleware: 'auth',
}
</script>

<style scoped>
.box-card {
  width: 750px;
  padding: 10;
  margin-bottom: 10px;
}

.center {
  text-align: center;
}
</style>