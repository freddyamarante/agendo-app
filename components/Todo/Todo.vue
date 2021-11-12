<template>
  <div>
    <el-card
      class="row-bg box-card"
      shadow="hover"
      :body-style="{ padding: '0px' }"
    >
      <el-descriptions :column="3" border>
        <el-descriptions-item  :span="3">
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
            {{  todo.contact.lastname }}
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
        <el-descriptions-item v-if="todo.completed === 0" :content-style="{'text-align': 'center'}">
          <template slot="label">
            <i class="el-icon-finished"></i>
            Acciones
          </template>
          <el-button type="success" round @click="setTodoAsCompleted()">Completado</el-button>
          <el-button type="primary"
           icon="el-icon-edit" 
           circle
           @click="$router.push(`/todo/${todo.id}/update`)"></el-button>
          <el-button 
            type="info" 
            icon="el-icon-message" 
            circle
            @click="$router.push(`/todo/${todo.id}/email`)">
          </el-button>
          <el-button
            type="danger"
            icon="el-icon-delete"
            circle
            @click="deleteTodo()"
          ></el-button>
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
  methods: {
    deleteTodo() {
      this.$confirm('¿Estás seguro que deseas eliminar esta agenda?', 'Warning', {
        confirmButtonText: 'Si',
        cancelButtonText: 'No',
        type: 'error',
      }).then(() => {
        this.$axios.$delete(`http://localhost:3333/todos/${this.todo.id}`)
          .then(() => {
            this.$message({
              type: 'success',
              message: 'Se ha eliminado correctamente',
            })
            this.$emit('delete', this.todo.id)
          })
      })
    },

    setTodoAsCompleted() {
      this.$axios.$put(`http://localhost:3333/todos`, {
        id: this.todo.id,
        completed: true
      })
        .then(() => {
          this.$emit('completed', this.todo.id)
        })
    }
  },
}
</script>

<style scoped>
.box-card {
  width: 750px;
  margin-bottom: 10px;
}

.center {
  text-align: center;
}

.label {
  background: #E1F3D8
}
</style>