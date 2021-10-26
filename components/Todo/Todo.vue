<template>
  <div>
    <el-card class="row-bg box-card" shadow="hover" :body-style="{ padding: '0px' }">
        <el-descriptions :column="3" :size="size" border>
          <el-descriptions-item :span="3">
            <template slot="label">
              <i class="el-icon-postcard"></i>
              Título
            </template>
            {{ todo.title }}
          </el-descriptions-item>
          <el-descriptions-item :span="3">
            <template slot="label">
              <i class="el-icon-document"></i>
              Descripción
            </template>
            {{ todo.description }}
          </el-descriptions-item>
          <el-descriptions-item>
            <template slot="label">
              <i class="el-icon-location-outline"></i>
              Lugar
            </template>
            {{ todo.location }}
          </el-descriptions-item>
          <el-descriptions-item>
            <template slot="label">
              <i class="el-icon-user"></i>
              Contacto
            </template>
            <div v-if="todo.contact">
              {{ todo.contact.name }}
            </div>
            <div v-else-if="!todo.contact">Ninguno</div>
          </el-descriptions-item>
          <el-descriptions-item>
            <template slot="label">
              <i class="el-icon-date"></i>
              Fecha
            </template>
            {{ todo.date }}
          </el-descriptions-item>
          <el-descriptions-item :content-style="{'text-align': 'center'}">
            <template slot="label">
              <i class="el-icon-finished"></i>
              Acciones
            </template>
              <el-button type="success" round>Completado</el-button>
              <el-button type="primary" icon="el-icon-edit" circle></el-button>
              <el-button type="info" icon="el-icon-message" circle></el-button>
              <el-button type="danger" icon="el-icon-delete" circle></el-button>
          </el-descriptions-item>
        </el-descriptions>
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
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