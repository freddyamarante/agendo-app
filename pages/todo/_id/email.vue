<template>
  <todo-email :todo-id="$route.params.id"/>
</template>

<script>
export default {
  name: 'Email',
  layout: 'action',
  middleware: 'auth',
}
</script>
