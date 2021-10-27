<template>
  <div>
    <h1>Añadir contacto</h1>
    <contact-form />
  </div>
</template>

<script>
  export default {
    name: 'CreateContact',
    layout: 'action',
    middleware: 'auth'
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