<template>
  <div>
    <el-tabs v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="Crear Agenda" name="first">Crear Agenda</el-tab-pane>
      <el-tab-pane label="Crear Contacto" name="second">Crear Contacto</el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        activeName: 'first',
      }
    },
    methods: {
      handleClick(tab, event) {
        console.log(tab, event)
      },
    },
  }
</script>
