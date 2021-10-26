<template>
  <div>
    <h1>Añadir contacto</h1>
  </div>
</template>

<script>
  export default {
    name: 'CreateContact',
    layout: 'action',
    middleware: 'auth'
  }
</script>