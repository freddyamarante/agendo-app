<template>
  <el-card
    v-loading="loading"
    class="row-bg box-card"
    shadow="hover"
    :body-style="{ padding: '0px' }"
  >
    <el-form ref="form" :model="form">
      <el-descriptions border>
        <el-descriptions-item :span="3">
          <template slot="label">
            <i class="el-icon-user"></i>
            Nombre
          </template>
          <el-input v-model="form.name" clearable> </el-input>
        </el-descriptions-item>
        <el-descriptions-item :span="3">
          <template slot="label">
            <i class="el-icon-user"></i>
            Apellido
          </template>
          <el-input v-model="form.lastname" clearable> </el-input>
        </el-descriptions-item>
        <el-descriptions-item :span="3">
          <template slot="label">
            <i class="el-icon-phone-outline"></i>
            Teléfono
          </template>
          <el-input v-model="form.phone" clearable> </el-input>
        </el-descriptions-item>
        <el-descriptions-item :span="3">
          <template slot="label">
            <i class="el-icon-message"></i>
            Correo
          </template>
          <el-input v-model="form.email" type="email" clearable> </el-input>
        </el-descriptions-item>
        
      </el-descriptions>
      <el-form-item>
        <el-button v-if="type === 'create'" type="primary" @click="addContact()"
          >Añadir Contacto</el-button>
        <el-button v-if="type === 'update'" type="primary" @click="updateContact()"
          >Editar Contacto</el-button
        >
      </el-form-item>
    </el-form>
  </el-card>
</template>

<script>
export default {
  name:'ContactForm',
  props: {
    contactId: {
      type: String,
      default: null,
      },
    type: {
      type: String,
      default: 'create'
    }
  },
  data() {
    return {
      form: {
        name: '',
        lastname: '',
        phone: '',
        email: '',
      },
      loading: false
    }
  },
  mounted() {
    if (this.contactId) {
      this.getContactById()
    }
  },
  methods: {
    async addContact() {
      this.loading = true
      const data = this.form
      await this.$axios.$post('http://localhost:3333/contacts', data)
      this.loading = false
      await this.$router.push('/')
      this.$notify({
        title: 'Contacto añadido',
        message: '',
        type: 'success'
      })
    },

    async updateContact() {
      const data = this.form
      await this.$axios.$put('http://localhost:3333/contacts', data)
      await this.$router.push('/')
      this.$notify({
        title: 'Contacto editado',
        message: '',
        type: 'success'
      })
    },

    async getContactById() {
      this.form = await this.$axios.$get(`http://localhost:3333/contacts/${this.contactId}`)
    }
  }
}
</script>
