<template>
  <div>
    <el-card class="row-bg box-card" shadow="hover" :body-style="{ padding: '0px' }">
        <el-descriptions :column="2" border>
          <el-descriptions-item>
            <template slot="label">
              <i class="el-icon-user"></i>
              Nombre
            </template>
            {{ contact.name }}
          </el-descriptions-item>
          <el-descriptions-item>
            <template slot="label">
              Apellido
            </template>
            {{ contact.lastname }}
          </el-descriptions-item>
          <el-descriptions-item>
            <template slot="label">
              <i class="el-icon-phone-outline"></i>
              Teléfono
            </template>
            {{ contact.phone }}
          </el-descriptions-item>
          <el-descriptions-item>
            <template slot="label">
              <i class="el-icon-message"></i>
              Correo
            </template>
            {{contact.email}}
          </el-descriptions-item>
          <el-descriptions-item :content-style="{'text-align': 'center'}">
            <template slot="label">
              <i class="el-icon-finished"></i>
              Acciones
            </template>
              <el-button type="primary" icon="el-icon-edit" circle @click="$router.push(`/contact/${contact.id}/update`)"></el-button>
              <el-button type="danger" icon="el-icon-delete" circle @click="deleteContact()"></el-button>
          </el-descriptions-item>
        </el-descriptions>
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'Contact',
  props: {
    contact: {
      type: Object,
      required: true,
    },
  },
  methods: {
    deleteContact() {
      this.$confirm('¿Estás seguro que deseas eliminar este contacto?', 'Warning', {
        confirmButtonText: 'Si',
        cancelButtonText: 'No',
        type: 'error',
      }).then(() => {
        this.$axios.$delete(`http://localhost:3333/contacts/${this.contact.id}`)
          .then(() => {
            this.$message({
              type: 'success',
              message: 'Se ha eliminado correctamente',
            })
            this.$emit('delete', this.contact.id)
          })
      })
    }
  }
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