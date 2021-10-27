<template>
  <div>
    <h1>Editar Contacto</h1>
    <contact-form :contact-id="$route.params.id" type="update" />
  </div>
</template>

<script>
export default {
  name: 'UpdateContact',
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